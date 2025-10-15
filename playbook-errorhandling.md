<!-- HEADER -->
<p align="center">
  <img src="https://capsule-render.vercel.app/api?type=waving&color=0:0A192F,100:1E90FF&height=200&section=header&text=📘%20Ansible%20Playbook%20Deep%20Dive&fontSize=32&fontColor=ffffff&animation=twinkling"/>
</p>

<p align="center">
  <img src="https://readme-typing-svg.herokuapp.com?duration=3500&pause=800&color=1E90FF&center=true&vCenter=true&width=980&lines=Includes%2C+Tasks%2C+Conditions%2C+Loops%2C+Tags%2C+Vars%2C+Extra+Vars%2C+Error+Handling"/>
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Automation-Ansible-blue?style=for-the-badge&logo=ansible&logoColor=white"/>
  <img src="https://img.shields.io/badge/Language-YAML-1572B6?style=for-the-badge&logo=yaml&logoColor=white"/>
</p>

---

## 🎯 Goal
A practical, GitHub-ready reference showing **how to**:
- Call **one playbook from another**
- Include **task files** inside playbooks
- Use **conditions**, **loops**, **tags**
- Work with **variables**, **vars_files**, **extra vars**
- Do **error handling** (`block`, `rescue`, `always`, `failed_when`, `ignore_errors`)
- Structure a **complete variables playbook** (with `group_vars/` & `host_vars/`)

---

## 🔗 1) Call One Playbook from Another
### A) Static include (parsed at start): `import_playbook`
```yaml
# site.yml (master playbook)
- import_playbook: plays/common.yml
- import_playbook: plays/web.yml
- import_playbook: plays/db.yml
```
> ✅ Best when composition is predictable and always included.

### B) Dynamic include (decided at runtime): `include_role` / `include_tasks`
Inside a play you can include task files or roles conditionally (see §2, §3).

---

## 📥 2) Include Task Files from a Play
Use **import_tasks** (static) or **include_tasks** (dynamic).

```yaml
- hosts: all
  gather_facts: false
  tasks:
    - import_tasks: tasks/prechecks.yml      # parsed at start
    - include_tasks: tasks/conditional.yml   # evaluated at runtime
      when: run_conditional | default(false)
```
**Tip:** Prefer `import_tasks` for fixed flows (faster & simpler). Use `include_tasks` when you need `when`, `loop`, or `tags` on the include.

---

## 🧠 3) Conditions (`when`) + Facts + Filters
```yaml
- name: Install web server on Debian only
  apt:
    name: nginx
    state: present
  when:
    - ansible_os_family == "Debian"
    - (web_enabled | default(true)) | bool

- name: Use default if var missing
  debug:
    msg: "Port is {{ http_port | default(80) }}"
```

---

## 🔁 4) Loops (modern `loop`, with controls)
```yaml
- name: Create app users
  user:
    name: "{{ item.name }}"
    state: present
    groups: "{{ item.groups }}"
  loop:
    - { name: "alice", groups: "dev" }
    - { name: "bob",   groups: "ops" }
  loop_control:
    label: "{{ item.name }}"
```
> ☝️ Use `loop` + `loop_control`. Older `with_items` still works but is legacy.

---

## 🏷️ 5) Tags (run parts of a playbook)
```yaml
- name: Install nginx
  apt:
    name: nginx
    state: present
  tags: ["install", "web"]

- name: Deploy config
  template:
    src: nginx.conf.j2
    dest: /etc/nginx/nginx.conf
  notify: Restart nginx
  tags: ["config"]
```
Run selectively:
```bash
ansible-playbook site.yml --tags install
ansible-playbook site.yml --skip-tags config
```

---

## 🧰 6) Variables (vars, vars_files, set_fact, precedence)
### A) Define vars in the play
```yaml
- hosts: web
  vars:
    http_port: 80
  tasks: ...
```

### B) Load from files
```yaml
- hosts: web
  vars_files:
    - vars/common.yml
    - vars/{{ env }}.yml
  tasks: ...
```

### C) Compute at runtime
```yaml
- set_fact:
    app_root: "/opt/{{ app_name }}-{{ app_version }}"
```

### D) Precedence (simplified)
`extra vars` > `task vars/set_fact` > `vars_files / play vars` > `inventory vars` > `role defaults`  

> 🔐 Keep secrets in **Ansible Vault**; load via `vars_files`.

---

## ➕ 7) Extra Vars (CLI overrides)
Pass values from CLI:
```bash
ansible-playbook site.yml -e env=prod -e "http_port=8080"
ansible-playbook site.yml -e @vars/override.yml
```
Inside playbooks, use them like normal vars: `{{ env }}`, `{{ http_port }}`.

---

## 🚨 8) Error Handling (`block/rescue/always`, `failed_when`, etc.)
```yaml
- hosts: all
  tasks:
    - block:
        - name: Try risky command
          command: "curl -sSf http://{{ backend }}/health"
          register: health
          changed_when: false
          failed_when: health.rc != 0 or ('UP' not in health.stdout)

        - name: Deploy if healthy
          debug: msg="Proceeding with deploy"
      rescue:
        - name: Fallback or alert
          debug: msg="Backend unhealthy — notify and stop"
      always:
        - name: Always run cleanup
          file:
            path: /tmp/deploy.lock
            state: absent

    - name: Ignore non-critical error
      command: "false"
      ignore_errors: true
```
**Notes**
- `failed_when` lets you define your own failure conditions
- `changed_when: false` is useful for read-only checks
- `ignore_errors: true` continues the play even if a task fails

---

## 🧩 9) Complete Variables Playbook (with `group_vars/` & `host_vars/`)
**Folder Layout**
```
inventory/
  hosts.ini
group_vars/
  all.yml             # globals
  web.yml             # vars for [web] group
host_vars/
  web1.yml            # vars for specific host
plays/
  site.yml
vars/
  prod.yml
```

**inventory/hosts.ini**
```ini
[web]
web1 ansible_host=10.0.0.10
web2 ansible_host=10.0.0.11

[db]
db1 ansible_host=10.0.0.20
```

**group_vars/all.yml**
```yaml
env: dev
http_port: 80
app_name: demoapp
```

**group_vars/web.yml**
```yaml
web_enabled: true
packages:
  - nginx
  - curl
```

**host_vars/web1.yml**
```yaml
http_port: 8081   # overrides group var for this host only
```

**plays/site.yml**
```yaml
- name: Web stack
  hosts: web
  become: yes
  vars_files:
    - ../vars/{{ env }}.yml   # picks vars/prod.yml when -e env=prod
  tasks:
    - name: Install packages
      apt:
        name: "{{ packages }}"
        state: present
      tags: install

    - name: Render index
      template:
        src: index.html.j2
        dest: /var/www/html/index.html
      vars:
        page_title: "{{ app_name | upper }} on port {{ http_port }}"

    - name: Health check
      uri:
        url: "http://localhost:{{ http_port }}"
        return_content: yes
      register: hc
      changed_when: false
      failed_when: "'200' not in hc.status | string"
```

Run with **extra vars**:
```bash
ansible-playbook -i inventory/hosts.ini plays/site.yml -e env=prod
```

---

## 🧪 10) Include One Playbook’s Tasks Inside Another (composition)
Sometimes you want a single entrypoint that composes plays and task files.

```yaml
# master.yml
- import_playbook: plays/prechecks.yml
- import_playbook: plays/site.yml
- import_playbook: plays/postchecks.yml
```
Inside `plays/site.yml`, you can further include tasks:
```yaml
- hosts: web
  tasks:
    - import_tasks: tasks/packages.yml
    - import_tasks: tasks/config.yml
    - include_tasks: tasks/conditional.yml
      when: feature_flag | default(false)
```

---

## ✅ Quick Cheats
- **Static**: `import_playbook`, `import_tasks`, `import_role` (parsed early)
- **Dynamic**: `include_tasks`, `include_role` (evaluated at runtime)
- **Error Handling**: `block` / `rescue` / `always`, `failed_when`, `ignore_errors`
- **Vars**: prefer `vars_files`, `group_vars/`, `host_vars/`; override with **extra vars**

---

<p align="center">
  <img src="https://capsule-render.vercel.app/api?type=waving&color=0:1E90FF,100:0A192F&height=140&section=footer"/>
</p>
