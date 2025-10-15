<!-- HEADER -->
<p align="center">
  <img src="https://capsule-render.vercel.app/api?type=waving&color=0:0A192F,100:1E90FF&height=200&section=header&text=🧩%20Ansible%2020%20Modules%20Playbook%20(With%20Notifies%20%2B%20Handlers)&fontSize=30&fontColor=ffffff&animation=twinkling"/>
</p>

<p align="center">
  <img src="https://readme-typing-svg.herokuapp.com?duration=3500&pause=800&color=1E90FF&center=true&vCenter=true&width=980&lines=One+Playbook+Demonstrating+20+Linux+Modules;Includes+Notify+Triggers+and+Handlers"/>
</p>

---

## 🧠 Overview

This guide provides a **single, production-style playbook** that demonstrates **20 core Ansible modules** on Linux, with **notify/handler** examples so learners understand how configuration changes trigger service restarts/reloads.

**Modules covered (20):**

`ping`, `command`, `shell`, `copy`, `template`, `file`, `yum`, `apt`, `service`, `systemd`, `user`, `group`, `cron`, `lineinfile`, `blockinfile`, `hostname`, `reboot`, `setup`, `git`, `unarchive`

---

## 📦 Inventory (example)

```ini
[linux]
your_linux_host ansible_host=192.0.2.10 ansible_user=ubuntu
```

---

## 🧾 Playbook: `linux_20_modules_demo.yml`

```yaml
---
- name: Linux 20 Modules Demo (with notifies + handlers)
  hosts: linux
  become: yes
  gather_facts: true

  vars:
    http_port: 80
    banner_file: /etc/motd
    tmp_dir: /tmp/ansible_demo
    demo_repo: "https://github.com/githubtraining/hellogitworld.git"
    demo_repo_dest: "/opt/hellogitworld"
    nginx_pkg_debian: nginx
    nginx_pkg_redhat: nginx
    reboot_now: false
    motd_block_marker: "ANSIBLE DEMO BLOCK"
    web_user: "webapp"
    web_group: "webapp"

  pre_tasks:
    # (18) setup — limit subsets to speed up
    - name: (18) Gather minimal facts
      ansible.builtin.setup:
        gather_subset:
          - network
          - hardware

    # (6) file — prepare temp dir
    - name: (06) Ensure temp directory exists
      ansible.builtin.file:
        path: "{{ tmp_dir }}"
        state: directory
        owner: "{{ ansible_user | default('root') }}"
        mode: "0755"

  tasks:
    # (1) ping
    - name: (01) Test connectivity (ping)
      ansible.builtin.ping:

    # (2) command
    - name: (02) Show kernel version (command)
      ansible.builtin.command: uname -r
      register: kernel_ver
      changed_when: false

    # (3) shell
    - name: (03) Check free rootfs space (shell)
      ansible.builtin.shell: df -h | awk 'NR==1 || /\/$/'
      register: df_out
      changed_when: false

    # (7/8) yum/apt — install nginx based on OS family
    - name: (07) Install nginx on Debian/Ubuntu (apt)
      ansible.builtin.apt:
        name: "{{ nginx_pkg_debian }}"
        state: present
        update_cache: true
      when: ansible_os_family == "Debian"

    - name: (08) Install nginx on RedHat/CentOS (yum)
      ansible.builtin.yum:
        name: "{{ nginx_pkg_redhat }}"
        state: present
      when: ansible_os_family == "RedHat"

    # (11) user
    - name: (11) Ensure app user exists
      ansible.builtin.user:
        name: "{{ web_user }}"
        state: present
        shell: /bin/bash

    # (12) group
    - name: (12) Ensure app group exists
      ansible.builtin.group:
        name: "{{ web_group }}"
        state: present

    # (6) file — ensure web root
    - name: (06b) Ensure web root exists
      ansible.builtin.file:
        path: /var/www/html
        state: directory
        owner: "{{ web_user }}"
        group: "{{ web_group }}"
        mode: "0755"

    # (4) copy — banner file (will not restart nginx)
    - name: (04) Copy login banner (MOTD)
      ansible.builtin.copy:
        content: |
          #########################################
          #  Welcome to the Ansible Demo Host     #
          #  Managed by Automation                #
          #########################################
        dest: "{{ banner_file }}"
        owner: root
        group: root
        mode: "0644"

    # (14) lineinfile — set alias, notify nothing
    - name: (14) Ensure 'll' alias is defined
      ansible.builtin.lineinfile:
        path: /etc/profile
        line: "alias ll='ls -alF'"
        create: yes

    # (15) blockinfile — add block to MOTD
    - name: (15) Insert information block in MOTD
      ansible.builtin.blockinfile:
        path: "{{ banner_file }}"
        marker: "# {mark} {{ motd_block_marker }}"
        block: |
          This host is managed by Ansible.
          Owner: {{ web_user }}

    # (5) template — nginx vhost, notify restart
    - name: (05) Render nginx vhost from template
      ansible.builtin.template:
        src: nginx.conf.j2
        dest: /etc/nginx/conf.d/ansible_demo.conf
        mode: "0644"
      notify: Restart nginx

    # (9) service — ensure nginx running and enabled
    - name: (09) Ensure nginx service is running
      ansible.builtin.service:
        name: nginx
        state: started
        enabled: true

    # (10) systemd — if units changed, reload daemon
    - name: (10) Systemd daemon-reload (when systemd)
      ansible.builtin.systemd:
        daemon_reload: true
      when: ansible_service_mgr == "systemd"
      notify: Reload systemd

    # (13) cron — health check every 15 min
    - name: (13) Install cron health-check for nginx
      ansible.builtin.cron:
        name: "nginx health"
        user: root
        minute: "*/15"
        job: "curl -fsS http://localhost:{{ http_port }} >/dev/null || systemctl restart nginx"

    # (19) git — clone demo repo
    - name: (19) Clone demo repository
      ansible.builtin.git:
        repo: "{{ demo_repo }}"
        dest: "{{ demo_repo_dest }}"
        version: HEAD

    # (20) unarchive — extract remote tarball
    - name: (20) Extract jq source tarball to tmp
      ansible.builtin.unarchive:
        src: "https://github.com/stedolan/jq/archive/refs/tags/jq-1.6.tar.gz"
        dest: "{{ tmp_dir }}"
        remote_src: true

    # (16) hostname — append suffix if missing
    - name: (16) Ensure hostname contains '-ansible-demo'
      ansible.builtin.hostname:
        name: >-
          {{ ansible_hostname if (ansible_hostname is search('-ansible-demo'))
             else (ansible_hostname ~ '-ansible-demo') }}

    # (17) reboot — optional toggle via var/extra-var
    - name: (17) Reboot if requested
      ansible.builtin.reboot:
        msg: "Reboot triggered by Ansible demo"
        reboot_timeout: 600
      when: reboot_now | bool

    # (8) setup usage — show a fact via debug
    - name: (08b) Show OS info (from gathered facts)
      ansible.builtin.debug:
        msg: "Running on {{ ansible_distribution }} {{ ansible_distribution_version }} (kernel {{ kernel_ver.stdout }})"

  handlers:
    - name: Restart nginx
      ansible.builtin.service:
        name: nginx
        state: restarted

    - name: Reload systemd
      ansible.builtin.systemd:
        daemon_reload: true
```

> **Template file required**: create `nginx.conf.j2` next to the playbook:
```jinja2
# Managed by Ansible
server {
  listen {{ http_port }};
  server_name _;
  root /var/www/html;
  location / {
    try_files $uri $uri/ =404;
  }
}
```

---

## ▶️ How to Run

```bash
# 1) Save the inventory from above as 'inventory.ini'
# 2) Save the playbook as 'linux_20_modules_demo.yml' and the template as 'nginx.conf.j2'

# Dry-run first
ansible-playbook -i inventory.ini linux_20_modules_demo.yml --check

# Apply changes
ansible-playbook -i inventory.ini linux_20_modules_demo.yml
```

---

## ✅ What Learners See

- How **notify/handler** chains work (template change → **Restart nginx**)  
- Cross-distro package handling (**apt** vs **yum**)  
- Files, blocks, and lines managed safely (**copy**, **file**, **blockinfile**, **lineinfile**)  
- Periodic health checks via **cron**  
- Optional **reboot** gated by a variable (`reboot_now`)  
- Using **facts** and **debug** to print runtime information

---

<p align="center">
  <img src="https://capsule-render.vercel.app/api?type=waving&color=0:1E90FF,100:0A192F&height=140&section=footer"/>
</p>
