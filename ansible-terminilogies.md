<!-- Header -->
<p align="center">
  <img src="https://capsule-render.vercel.app/api?type=waving&color=0:101820,100:EE3124&height=200&section=header&text=⚙️%20Ansible%20Terminologies%20Cheat%20Sheet&fontSize=38&fontColor=ffffff&animation=twinkling"/>
</p>

<p align="center">
  <img src="https://readme-typing-svg.herokuapp.com?duration=3000&pause=850&color=EE3124&center=true&vCenter=true&width=850&lines=Automation+%7C+Configuration+Management+%7C+Orchestration;By+Binnbash+Academy;Learn+Playbooks%2C+Roles%2C+Vault%2C+Inventory%2C+and+More!"/>
</p>

<p align="center">
  <img alt="Ansible" height="48" src="https://raw.githubusercontent.com/devicons/devicon/master/icons/ansible/ansible-original.svg" />
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Automation-Ansible-EE3124?style=for-the-badge&logo=ansible&logoColor=white"/>
  <img src="https://img.shields.io/badge/Language-YAML-6A9FB5?style=for-the-badge"/>
  <img src="https://img.shields.io/badge/Platform-DevOps-0B3D91?style=for-the-badge&logo=githubactions&logoColor=white"/>
</p>

---

## 📚 Table of Contents
- [🧠 Core Terminologies](#-core-terminologies)
- [⚙️ Configuration & Files](#️-configuration--files)
- [🧰 Advanced Concepts](#-advanced-concepts)
- [🚀 Execution & Management](#-execution--management)
- [📎 Credits](#-credits)

---

## 🧠 Core Terminologies

| Term | Description |
|------|-------------|
| **Ansible** | An open-source IT automation tool used for configuration management, application deployment, and orchestration. |
| **Controller Node / Control Machine** | The machine where Ansible is installed and from which all tasks are executed. |
| **Managed Node / Target Node** | The remote systems that Ansible manages and automates. |
| **Inventory** | A file (usually `hosts` file) that lists all managed nodes with their IPs, hostnames, and groups. |
| **Groups** | Logical collections of hosts within the inventory file (e.g., `[webservers]`, `[dbservers]`). |
| **Modules** | The building blocks of Ansible—small programs (like `copy`, `yum`, `apt`, `service`, etc.) that perform specific actions on nodes. |
| **Tasks** | Individual units of work (e.g., install a package, start a service) defined in a playbook. |
| **Play** | A mapping of a group of hosts to a set of tasks (one “play” = one scenario of automation). |
| **Playbook** | A YAML file that contains one or more plays defining automation steps. |
| **Ad-hoc Commands** | One-line Ansible commands used for quick tasks (e.g., `ansible all -m ping`). |

---

## ⚙️ Configuration & Files

| Term | Description |
|------|-------------|
| **ansible.cfg** | Configuration file defining settings such as inventory location, privilege escalation, connection type, etc. |
| **Facts** | System information automatically gathered by Ansible (e.g., IP, OS type, CPU count). |
| **Gather Facts** | A step in a playbook that collects system information before running tasks. |
| **Handlers** | Special tasks triggered by other tasks (usually after a change), e.g., restart a service. |
| **Templates** | Files (usually `.j2` Jinja2 templates) where variables are dynamically replaced during deployment. |
| **Variables** | Custom values stored and used inside playbooks or templates to make them dynamic. |
| **Conditionals** | Statements that make task execution depend on conditions (e.g., `when: ansible_os_family == 'RedHat'`). |
| **Loops** | Repeat a task multiple times using items (e.g., `with_items` or `loop`). |

---

## 🧰 Advanced Concepts

| Term | Description |
|------|-------------|
| **Roles** | A structured way to organize playbooks—includes tasks, templates, files, handlers, and variables. |
| **Collections** | A distribution format for Ansible content (roles, plugins, modules) maintained by the community. |
| **Galaxy** | Ansible’s public repository to download roles and collections (`ansible-galaxy install`). |
| **Vault** | A security feature that encrypts sensitive data like passwords or keys in playbooks. |
| **Tags** | Labels assigned to tasks so you can run specific sections of a playbook. |
| **Delegation** | Running a task on a different host than the target (`delegate_to:`). |
| **Lookup Plugins** | Fetch external data sources during playbook execution. |
| **Filters** | Used to manipulate or format variables and data in templates. |
| **Callbacks** | Customize how output is displayed during playbook execution. |

---

## 🚀 Execution & Management

| Term | Description |
|------|-------------|
| **Idempotence** | Ansible ensures that repeating a playbook doesn’t make further changes if the system is already in the desired state. |
| **Check Mode / Dry Run** | Run playbooks with `--check` to preview changes without applying them. |
| **Become / Privilege Escalation** | Runs tasks as another user (like root) using `become: yes`. |
| **Inventory Plugins** | Extend inventory sources (e.g., AWS EC2, GCP, Azure, dynamic inventories). |

---

<p align="center">
  <img src="https://capsule-render.vercel.app/api?type=waving&color=0:EE3124,100:101820&height=140&section=footer"/>
</p>

## 📎 Credits
Made with ❤️ by **Binnbash Academy** — Empowering learners in DevOps, Cloud, and Automation.
