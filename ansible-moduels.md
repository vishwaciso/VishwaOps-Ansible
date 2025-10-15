<!-- HEADER -->
<p align="center">
  <img src="https://capsule-render.vercel.app/api?type=waving&color=0:0A192F,100:1E90FF&height=200&section=header&text=🧩%20Ansible%20Modules%20for%20Linux%20%26%20Windows&fontSize=32&fontColor=ffffff&animation=twinkling"/>
</p>

<p align="center">
  <img src="https://readme-typing-svg.herokuapp.com?duration=3500&pause=800&color=1E90FF&center=true&vCenter=true&width=900&lines=Comprehensive+List+of+Linux+and+Windows+Modules;For+Configuration%2C+Deployment%2C+and+Automation"/>
</p>

---

## 🐧 **Top 20 Ansible Modules for Linux**

| No | Module | Description |
|----|---------|--------------|
| 1️⃣ | **ping** | Test connectivity between controller and managed node |
| 2️⃣ | **command** | Run simple commands on remote host (no shell) |
| 3️⃣ | **shell** | Execute shell commands (supports pipes, redirection) |
| 4️⃣ | **copy** | Copy files from controller to target system |
| 5️⃣ | **template** | Manage Jinja2 templates and variable substitution |
| 6️⃣ | **file** | Manage file attributes (permissions, owner, mode) |
| 7️⃣ | **yum** | Install, remove, or update packages on RedHat/CentOS |
| 8️⃣ | **apt** | Install, remove, or update packages on Debian/Ubuntu |
| 9️⃣ | **service** | Manage system services (start, stop, restart) |
| 🔟 | **systemd** | Control services and system targets on systemd systems |
| 11 | **user** | Create or manage Linux user accounts |
| 12 | **group** | Manage user groups |
| 13 | **cron** | Schedule tasks using cron jobs |
| 14 | **lineinfile** | Ensure specific lines exist or are removed in files |
| 15 | **blockinfile** | Insert multi-line text blocks in files |
| 16 | **hostname** | Set or update the system hostname |
| 17 | **reboot** | Reboot the system and wait for it to come back online |
| 18 | **setup** | Gather system facts (hardware, OS, IPs) |
| 19 | **git** | Clone or manage Git repositories |
| 20 | **unarchive** | Extract tar/zip archives on remote servers |

📘 **Usage Example:**
```bash
ansible all -m yum -a "name=httpd state=present" --become
```

---

## 🪟 **Top 20 Ansible Modules for Windows**

| No | Module | Description |
|----|---------|--------------|
| 1️⃣ | **win_ping** | Check connectivity between controller and Windows host |
| 2️⃣ | **win_command** | Run a command on Windows (non-interactive) |
| 3️⃣ | **win_shell** | Execute PowerShell or cmd commands |
| 4️⃣ | **win_copy** | Copy files to Windows targets |
| 5️⃣ | **win_template** | Manage templated files (Jinja2) |
| 6️⃣ | **win_file** | Manage file attributes and state |
| 7️⃣ | **win_service** | Start, stop, restart, or enable Windows services |
| 8️⃣ | **win_feature** | Install or remove Windows features (IIS, .NET, etc.) |
| 9️⃣ | **win_user** | Create, modify, or remove Windows users |
| 🔟 | **win_group** | Manage user groups |
| 11 | **win_package** | Install or remove MSI/exe packages |
| 12 | **win_updates** | Manage Windows updates |
| 13 | **win_reboot** | Restart Windows host after changes |
| 14 | **win_registry** | Add, update, or delete Windows Registry keys |
| 15 | **win_environment** | Manage environment variables |
| 16 | **win_firewall_rule** | Configure Windows Firewall rules |
| 17 | **win_hostname** | Change computer name or join domain |
| 18 | **win_disk_facts** | Gather disk and partition information |
| 19 | **win_stat** | Get file information (size, attributes) |
| 20 | **win_chocolatey** | Install software using Chocolatey package manager |

📘 **Usage Example:**
```bash
ansible windows -m win_feature -a "name=Web-Server state=present"
```

---

## ⚙️ **List All Available Modules**
Use this command on any system where Ansible is installed:
```bash
ansible-doc -l
```
📘 Output:
```
ansible.builtin.ping          → Try to connect to host and test connectivity
ansible.builtin.copy          → Copy files to remote locations
ansible.windows.win_feature   → Install or remove Windows features
```

---

## 💡 **Check Documentation of a Specific Module**
```bash
ansible-doc <module_name>
```
Example:
```bash
ansible-doc win_service
```

---

## 🧠 **Quick Comparison: Linux vs Windows Modules**

| Area | Linux Modules | Windows Modules |
|------|----------------|-----------------|
| Connectivity | `ping` | `win_ping` |
| Commands | `command`, `shell` | `win_command`, `win_shell` |
| Packages | `apt`, `yum` | `win_package`, `win_chocolatey` |
| Services | `service`, `systemd` | `win_service` |
| Users | `user`, `group` | `win_user`, `win_group` |
| Files | `copy`, `file`, `template` | `win_copy`, `win_file`, `win_template` |
| Reboot | `reboot` | `win_reboot` |

---

<p align="center">
  <img src="https://capsule-render.vercel.app/api?type=waving&color=0:1E90FF,100:0A192F&height=140&section=footer"/>
</p>
