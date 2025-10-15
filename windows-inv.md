<!-- HEADER -->
<p align="center">
  <img src="https://capsule-render.vercel.app/api?type=waving&color=0:0A192F,100:1E90FF&height=200&section=header&text=🪟%20Windows%20Inventory%20+%20Ansible%20Config%20+%20Galaxy%20%26%20Doc%20Commands&fontSize=30&fontColor=ffffff&animation=twinkling"/>
</p>

<p align="center">
  <img src="https://readme-typing-svg.herokuapp.com?duration=3500&pause=800&color=1E90FF&center=true&vCenter=true&width=900&lines=Windows+Inventory+Configuration;Ansible.cfg+Settings;Galaxy+Roles+%26+Collections;Ansible-Doc+Usage"/>
</p>

---

## 🪟 **Windows Inventory File**
Windows hosts connect via **WinRM (Windows Remote Management)** instead of SSH.  
You can manage Windows systems directly from your Linux control node.

### ✅ Example: `inventory_windows.ini`
```ini
[windows]
winhost1 ansible_host=192.168.1.100 ansible_user=Administrator ansible_password='StrongP@ss123'
           ansible_connection=winrm
           ansible_winrm_transport=basic
           ansible_winrm_server_cert_validation=ignore

winhost2 ansible_host=192.168.1.101 ansible_user=Administrator ansible_password='StrongP@ss123'
           ansible_connection=winrm
           ansible_winrm_transport=ntlm
           ansible_winrm_server_cert_validation=ignore
```

🧠 **Key WinRM Parameters:**
| Parameter | Description |
|------------|-------------|
| `ansible_connection=winrm` | Enables WinRM communication |
| `ansible_winrm_transport` | Options: `basic`, `ntlm`, `kerberos`, `credssp` |
| `ansible_winrm_server_cert_validation=ignore` | Skips SSL validation (useful for self-signed certs) |
| `ansible_port` | Optional, defaults to 5985 (HTTP) or 5986 (HTTPS) |
| `ansible_user` / `ansible_password` | Windows admin credentials |

---

## 🧩 **Alternate Minimal Windows Inventory Example**
```ini
[windows]
win1 ansible_host=10.0.0.25

[windows:vars]
ansible_connection=winrm
ansible_port=5985                 # 5986 if HTTPS
ansible_winrm_transport=basic     # or ntlm / credssp / kerberos
ansible_user=Administrator
ansible_password=ReplaceMe123!
ansible_winrm_server_cert_validation=ignore  # only if using self-signed over HTTPS
```

---

## ⚙️ **Ansible Configuration File (`ansible.cfg`)**
The **`ansible.cfg`** file defines default settings for all your playbooks and CLI operations.

### ✅ Default search order
Ansible reads configs in this order (first match wins):
1. `ANSIBLE_CONFIG` (environment variable)
2. `./ansible.cfg` (in current directory)
3. `~/.ansible.cfg` (in user home)
4. `/etc/ansible/ansible.cfg` (system default)

---

### 📄 Example: `ansible.cfg`
```ini
[defaults]
inventory = ./inventory_windows.ini
remote_user = Administrator
host_key_checking = False
deprecation_warnings = False
timeout = 45
forks = 10
roles_path = ./roles
collections_paths = ./collections
log_path = ./ansible.log
nocows = True

[privilege_escalation]
become = False

[ssh_connection]
pipelining = True
retries = 3
```

### 🧠 **Important Parameters**
| Section | Key | Description |
|----------|-----|-------------|
| `[defaults]` | `inventory` | Sets default inventory path |
|  | `roles_path` | Where roles are stored |
|  | `collections_paths` | Location for downloaded collections |
|  | `log_path` | File where Ansible logs its actions |
| `[privilege_escalation]` | `become` | Enables sudo (for Linux) |
| `[ssh_connection]` | `pipelining` | Speeds up SSH execution |
| `[defaults]` | `host_key_checking` | Disables host fingerprint prompts |

💡 **Command to check active config:**
```bash
ansible --version
```
(Shows which `ansible.cfg` is being used)

---

## 🌍 **Ansible Galaxy Commands**
**Ansible Galaxy** is the official hub for sharing and downloading **roles** and **collections**.

### ✅ **Roles Management**
| Command | Description |
|----------|-------------|
| `ansible-galaxy init myrole` | Create a new role structure |
| `ansible-galaxy install geerlingguy.nginx` | Download a role from Galaxy |
| `ansible-galaxy list` | List installed roles |
| `ansible-galaxy remove geerlingguy.nginx` | Remove a role |
| `ansible-galaxy search nginx` | Search for roles on Galaxy |

📁 Installed role structure:
```
roles/
 └── geerlingguy.mysql/
      ├── tasks/
      ├── templates/
      ├── handlers/
      ├── vars/
      ├── defaults/
      ├── meta/
      └── README.md
```

---

### ✅ **Collections Management**
Collections are bundles of roles, modules, and plugins.

| Command | Description |
|----------|-------------|
| `ansible-galaxy collection install community.windows` | Install a Windows collection |
| `ansible-galaxy collection list` | Show installed collections |
| `ansible-galaxy collection install -r requirements.yml` | Install multiple collections |
| `ansible-galaxy collection init my_namespace.my_collection` | Create a new collection |
| `ansible-galaxy collection build` | Package your collection |

**Example:**
```bash
ansible-galaxy collection install ansible.windows
```

**requirements.yml example:**
```yaml
collections:
  - name: ansible.windows
  - name: community.general
```

---

## 📘 **Ansible Doc Commands**
Use `ansible-doc` to explore **modules, options, and examples** directly from the CLI.

| Command | Purpose |
|----------|----------|
| `ansible-doc -l` | List all available modules |
| `ansible-doc <module_name>` | View documentation for a module |
| `ansible-doc -s <module_name>` | Show only parameter skeleton |
| `ansible-doc -t lookup -l` | List all lookup plugins |
| `ansible-doc -t connection -l` | List all connection plugins |
| `ansible-doc -t become -l` | List privilege escalation methods |

**Examples:**
```bash
ansible-doc win_service
ansible-doc ansible.builtin.copy
ansible-doc -s ansible.windows.win_user
```

---

## 🧰 **Useful Diagnostic Commands**
| Command | Description |
|----------|-------------|
| `ansible-inventory --graph` | View hierarchical group tree |
| `ansible all -m ping` | Test all hosts from inventory |
| `ansible-playbook --syntax-check playbook.yml` | Validate playbook syntax |
| `ansible-playbook --check playbook.yml` | Perform a dry run |
| `ansible-config list` | List all config options |
| `ansible-config dump` | View current configuration |
| `ansible-console` | Open interactive Ansible shell |

---

## 🧱 **Example Folder Structure**
```
project/
 ├── ansible.cfg
 ├── inventory_windows.ini
 ├── playbooks/
 │    ├── site.yml
 │    └── windows_iis.yml
 ├── roles/
 │    └── geerlingguy.nginx/
 ├── collections/
 │    └── ansible_collections/
 └── logs/
      └── ansible.log
```

---

## ✅ **Summary**
| Category | Key Usage |
|-----------|------------|
| **Inventory** | Defines hosts and connection details |
| **ansible.cfg** | Global configuration and defaults |
| **Galaxy Roles** | Download and reuse community content |
| **Galaxy Collections** | Use extended modules/plugins |
| **ansible-doc** | Learn and explore modules in CLI |
| **Diagnostics** | Validate syntax, configs, and connectivity |

---

<p align="center">
  <img src="https://capsule-render.vercel.app/api?type=waving&color=0:1E90FF,100:0A192F&height=140&section=footer"/>
</p>
