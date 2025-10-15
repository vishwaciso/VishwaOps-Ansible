<div align="center">

# ⚙️ **Ansible Terminologies Cheat Sheet**
### 🏫 _By Binnbash Academy_

<img src="https://img.shields.io/badge/Automation-Ansible-blue?style=for-the-badge&logo=ansible&logoColor=white"/> 
<img src="https://img.shields.io/badge/Platform-DevOps-orange?style=for-the-badge&logo=githubactions&logoColor=white"/>
<img src="https://img.shields.io/badge/Language-YAML-yellow?style=for-the-badge"/>

---

</div>

## 🧠 CORE TERMINOLOGIES
> 💡 _Foundational concepts every Ansible engineer must know._

| 🧩 Term | 📘 Description |
|:---------------------------|:-------------------------------------------------------------|
| **Ansible** | 🧰 Open-source IT automation tool used for configuration, deployment, and orchestration. |
| **Controller Node** | 🖥️ The system where Ansible is installed and tasks are executed. |
| **Managed Node** | 💻 Remote machines that Ansible manages via SSH. |
| **Inventory** | 📋 File listing managed nodes (`hosts` file). |
| **Modules** | 🧱 Core components that perform actions (`yum`, `copy`, `service`). |
| **Playbook** | 📜 YAML file defining automation workflows. |
| **Tasks** | 🔧 Steps defined within a playbook. |
| **Ad-hoc Commands** | ⚡ One-line automation commands (`ansible all -m ping`). |

---

## ⚙️ CONFIGURATION & FILES
> 🗂️ _Defines how and where Ansible runs._

| ⚙️ Term | 📘 Description |
|:-------------------|:-------------------------------------------------------------|
| **ansible.cfg** | ⚙️ Central config file with inventory, privilege, and connection settings. |
| **Facts** | 🧠 Auto-collected system data like IP, OS, CPU, etc. |
| **Handlers** | 🔁 Triggered tasks after a change (e.g., restart service). |
| **Templates** | 🧾 Jinja2 files where variables are dynamically replaced. |
| **Variables** | 🪄 Dynamic placeholders for reusable code. |
| **Conditionals** | 🔍 Run tasks only if conditions match (`when:`). |
| **Loops** | 🔄 Repeat tasks over a list (`loop`, `with_items`). |

---

## 🚀 ADVANCED CONCEPTS
> 🧩 _Reusable, secure, and scalable automation._

| 🔧 Term | 📘 Description |
|:-----------------|:-------------------------------------------------------------|
| **Roles** | 🧱 Organized structure for playbooks (tasks, templates, vars). |
| **Collections** | 📦 Bundled content (roles, modules, plugins). |
| **Galaxy** | 🌍 Public hub to download Ansible content. |
| **Vault** | 🔐 Encrypts secrets and passwords. |
| **Tags** | 🏷️ Selectively run parts of playbooks. |
| **Delegation** | 📤 Run a task on a different host (`delegate_to:`). |
| **Lookup Plugins** | 🔎 Fetch external data dynamically. |
| **Filters** | 🧮 Format or manipulate variables. |
| **Callbacks** | 🗣️ Customize playbook output display. |

---

## 💻 EXECUTION & MANAGEMENT
> ⚡ _Optimize, secure, and manage automation at scale._

| ⚡ Term | 📘 Description |
|:-------------------|:-------------------------------------------------------------|
| **Idempotence** | ✅ Ensures no repeated changes if the system is already correct. |
| **Check Mode / Dry Run** | 🧪 Preview changes without applying (`--check`). |
| **Become / Privilege Escalation** | 🔐 Run tasks as root or other users (`become: yes`). |
| **Inventory Plugins** | ☁️ Dynamic inventories from AWS, Azure, GCP. |

---

<div align="center">

✨ _Crafted with ❤️ by_ **Binnbash Academy**  
🌐 [www.binnbash.com](https://www.binnbash.com)  
📚 _Empowering learners in DevOps, Cloud, and Automation._

</div>
