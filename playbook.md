<!-- HEADER -->
<p align="center">
  <img src="https://capsule-render.vercel.app/api?type=waving&color=0:0A192F,100:1E90FF&height=200&section=header&text=📘%20Ansible%20Playbook%20Explained&fontSize=32&fontColor=ffffff&animation=twinkling"/>
</p>

<p align="center">
  <img src="https://readme-typing-svg.herokuapp.com?duration=3500&pause=800&color=1E90FF&center=true&vCenter=true&width=850&lines=Understanding+Ansible+Playbooks;Structure%2C+Syntax%2C+and+Key+Components"/>
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Automation-Ansible-blue?style=for-the-badge&logo=ansible&logoColor=white"/>
  <img src="https://img.shields.io/badge/Language-YAML-1572B6?style=for-the-badge&logo=yaml&logoColor=white"/>
</p>

---

## ⚙️ **What is an Ansible Playbook?**

> 🧠 **Definition:**  
> An **Ansible Playbook** is a YAML file that defines **automation instructions** for configuring systems, deploying applications, or managing IT infrastructure.  
> It describes *what* needs to be done and *on which hosts* — in a simple, human-readable format.

---

## 🧩 **Purpose**

- Acts as the **blueprint for automation** in Ansible.  
- Contains a **set of tasks** executed on specified servers.  
- Supports **conditional logic, loops, handlers, roles, and variables**.  
- Enables **repeatable and idempotent** operations across environments.

---

## 📂 **Playbook Structure**

An Ansible playbook is organized into **plays**, and each play maps:
> ✅ A set of hosts ➡️ to ➡️ a series of tasks.

📘 **Example:**
```yaml
- name: Install and configure web server
  hosts: web
  become: yes

  vars:
    http_port: 80

  tasks:
    - name: Install Nginx
      apt:
        name: nginx
        state: present

    - name: Start Nginx
      service:
        name: nginx
        state: started
        enabled: true

  handlers:
    - name: Restart Nginx
      service:
        name: nginx
        state: restarted
