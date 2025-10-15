<!-- HEADER -->
<p align="center">
  <img src="https://capsule-render.vercel.app/api?type=waving&color=0:0A192F,100:1E90FF&height=200&section=header&text=🪟%20Ansible%20Windows%20Playbook%20(20%20Modules%20%2B%20Notifies%20%26%20Handlers)&fontSize=28&fontColor=ffffff&animation=twinkling"/>
</p>

<p align="center">
  <img src="https://readme-typing-svg.herokuapp.com?duration=3600&pause=800&color=1E90FF&center=true&vCenter=true&width=980&lines=One+Windows+Playbook+Using+20+Modules;Includes+Notify+Triggers+and+Handlers+(IIS+restart)"/>
</p>

---

## 🧠 Overview
This guide provides a **single Windows playbook** that demonstrates **20 essential Ansible Windows modules** with **notify/handler** examples so learners see how a configuration change (template update) triggers a **Restart IIS** handler.

**Modules covered (20):**  
`win_ping`, `win_command`, `win_shell`, `win_copy`, `win_template`, `win_file`, `win_service`, `win_feature`, `win_user`, `win_group`, `win_package`, `win_updates`, `win_reboot`, `win_registry`, `win_environment`, `win_firewall_rule`, `win_hostname`, `win_disk_facts`, `win_stat`, `win_chocolatey`

> ℹ️ For demo purposes only — adjust package URLs, passwords, and policies for your environment.

---

## 📦 Inventory (WinRM example)
```ini
[windows]
winhost ansible_host=192.0.2.25 ansible_user=Administrator ansible_password=ChangeMe!123
         ansible_connection=winrm ansible_winrm_transport=basic
         ansible_winrm_server_cert_validation=ignore
```

---

## 🧾 Playbook: `windows_20_modules_demo.yml`
```yaml
---
- name: Windows 20 Modules Demo (with notifies + handlers)
  hosts: windows
  gather_facts: false

  vars:
    demo_dir: 'C:\Temp\ansible_demo'
    webroot: 'C:\inetpub\wwwroot'
    index_html: '{{ webroot }}\index.html'
    readme_txt: '{{ webroot }}\readme.txt'
    demo_user: 'webuser'
    demo_user_password: 'ChangeMe!123'     # 👉 Demo only. Use Vault in real envs.
    choco_pkg: 'git'                       # Requires Chocolatey installed
    reboot_now: false

  pre_tasks:
    # (6) win_file — ensure a temp directory exists
    - name: (06) Ensure temp directory exists
      ansible.windows.win_file:
        path: '{{ demo_dir }}'
        state: directory

  tasks:
    # (1) win_ping — connectivity check
    - name: (01) Test WinRM connectivity
      ansible.windows.win_ping:

    # (2) win_command — simple command
    - name: (02) Show Windows version (command)
      ansible.windows.win_command: cmd.exe /c ver
      register: win_ver
      changed_when: false

    # (3) win_shell — PowerShell query
    - name: (03) Get basic computer info (PowerShell)
      ansible.windows.win_shell: |
        Get-ComputerInfo | Select-Object OsName,OsVersion,WindowsProductName | ConvertTo-Json
      register: comp_info
      changed_when: false

    # (8) win_feature — Install IIS
    - name: (08) Install IIS (Web-Server) feature
      ansible.windows.win_feature:
        name: Web-Server
        state: present
        include_sub_features: true
        include_management_tools: true

    # (7) win_service — Ensure IIS service running
    - name: (07) Ensure IIS (W3SVC) is running
      ansible.windows.win_service:
        name: W3SVC
        state: started
        start_mode: auto

    # (4) win_copy — drop a readme file
    - name: (04) Copy readme to web root
      ansible.windows.win_copy:
        content: |
          Welcome to the Ansible Windows Demo!
          Managed by Ansible.
        dest: '{{ readme_txt }}'

    # (5) win_template — render index.html (notify restart)
    - name: (05) Render templated index.html
      ansible.windows.win_template:
        src: index.html.j2
        dest: '{{ index_html }}'
      notify: Restart IIS

    # (6) win_file — ensure a logs directory
    - name: (06b) Ensure logs directory exists
      ansible.windows.win_file:
        path: 'C:\logs'
        state: directory

    # (9) win_user — create demo user
    - name: (09) Ensure local user exists
      ansible.windows.win_user:
        name: '{{ demo_user }}'
        password: '{{ demo_user_password }}'
        state: present
        update_password: on_create
        groups:
          - Users

    # (10) win_group — ensure custom group and add member
    - name: (10) Ensure 'webadmins' group exists and includes user
      ansible.windows.win_group:
        name: webadmins
        state: present
        members:
          - '{{ demo_user }}'
        keep_members: yes

    # (14) win_registry — set a demo registry key
    - name: (14) Set demo registry value
      ansible.windows.win_registry:
        path: HKLM:\Software\AnsibleDemo
        name: InstallPath
        data: '{{ webroot }}'
        type: string
        state: present

    # (15) win_environment — set machine-level env var
    - name: (15) Ensure WEB_ENV environment variable
      ansible.windows.win_environment:
        state: present
        name: WEB_ENV
        value: Production
        level: Machine

    # (16) win_firewall_rule — open HTTP port
    - name: (16) Allow inbound HTTP (80)
      ansible.windows.win_firewall_rule:
        name: Allow_HTTP_80
        localport: 80
        action: allow
        direction: in
        protocol: TCP
        state: present

    # (11) win_package — install 7-Zip via MSI (silent)
    - name: (11) Install 7-Zip (example MSI)
      ansible.windows.win_package:
        path: https://www.7-zip.org/a/7z1900-x64.msi
        product_id: '{23170F69-40C1-2702-1900-000001000000}'
        arguments: /qn
        state: present

    # (20) win_chocolatey — install a package via Chocolatey
    - name: (20) Install Git via Chocolatey (requires Chocolatey)
      ansible.windows.win_chocolatey:
        name: '{{ choco_pkg }}'
        state: present
      register: choco_result
      failed_when: false   # In case Chocolatey isn't installed yet

    # (12) win_updates — install security updates
    - name: (12) Install available Security updates
      ansible.windows.win_updates:
        category_names:
          - SecurityUpdates
        state: installed
      register: updates_result

    # (19) win_stat — get info about index.html
    - name: (19) Stat index.html
      ansible.windows.win_stat:
        path: '{{ index_html }}'
      register: index_stat

    # (18) win_disk_facts — gather disk facts
    - name: (18) Gather disk facts
      ansible.windows.win_disk_facts:
      register: diskfacts
      changed_when: false

    # (17) win_hostname — ensure hostname suffix
    - name: (17) Ensure hostname contains '-ansible-demo'
      ansible.windows.win_hostname:
        name: >-
          {{ ansible_hostname if (ansible_hostname is search('-ansible-demo'))
             else (ansible_hostname ~ '-ansible-demo') }}

    # (13) win_reboot — optional reboot
    - name: (13) Reboot if requested
      ansible.windows.win_reboot:
        msg: 'Reboot triggered by Ansible Windows demo'
        reboot_timeout: 1200
      when: reboot_now | bool

    # Show some results
    - name: (XX) Debug info
      ansible.builtin.debug:
        msg:
          - "Windows Version: {{ win_ver.stdout | default('n/a') }}"
          - "Index exists: {{ index_stat.stat.exists | default(false) }}"
          - "Updates installed: {{ updates_result.updates | default([]) | length }}"
          - "Disks: {{ (diskfacts.disks | default([])) | length }}"
          - "Chocolatey result changed: {{ choco_result.changed | default(false) }}"

  handlers:
    - name: Restart IIS
      ansible.windows.win_service:
        name: W3SVC
        state: restarted
```

> **Template file required**: create `index.html.j2` next to the playbook:
```html
<!-- Managed by Ansible -->
<!doctype html>
<html>
  <head><title>Windows Ansible Demo</title></head>
  <body style="font-family: Arial, sans-serif;">
    <h1>It works! 🎉</h1>
    <p>WEB_ENV = {{ lookup('ansible.builtin.env', 'WEB_ENV') | default('unset') }}</p>
    <p>Served from {{ webroot }}</p>
  </body>
</html>
```

---

## ▶️ How to Run
```bash
# Save inventory as 'inventory.ini'
# Save playbook as 'windows_20_modules_demo.yml' and the template as 'index.html.j2'

# Dry-run (some tasks may be skipped in check mode)
ansible-playbook -i inventory.ini windows_20_modules_demo.yml --check

# Apply changes
ansible-playbook -i inventory.ini windows_20_modules_demo.yml
```

---

## ✅ What Learners See
- **Notify/Handler flow**: template update ➜ **Restart IIS**
- Installing IIS with **win_feature**, ensuring **W3SVC** is running
- Managing files with **win_copy**, **win_template**, **win_file**
- Local users & groups with **win_user**, **win_group**
- **Security updates**, **firewall rules**, and **environment vars**
- Packages via **win_package** and **Chocolatey**
- Facts and status with **win_disk_facts**, **win_stat**, **debug**
- Optional **reboot** controlled by a variable

---

<p align="center">
  <img src="https://capsule-render.vercel.app/api?type=waving&color=0:1E90FF,100:0A192F&height=140&section=footer"/>
</p>
