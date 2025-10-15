<!-- HEADER -->
<p align="center">
  <img src="https://capsule-render.vercel.app/api?type=waving&color=0:0A192F,100:1E90FF&height=200&section=header&text=⚙️%20Ansible%20Installation%20+%20Core%20Commands%20Guide&fontSize=32&fontColor=ffffff&animation=twinkling"/>
</p>

<p align="center">
  <img src="https://readme-typing-svg.herokuapp.com?duration=3500&pause=800&color=1E90FF&center=true&vCenter=true&width=900&lines=Ansible+Setup+on+Amazon+Linux+and+Ubuntu;Core+Commands%2C+Modules%2C+Variables%2C+and+Playbook+Validation"/>
</p>

---

## 🧠 **What is Ansible?**
**Ansible** is an **open-source automation tool** by Red Hat used for **configuration management**, **application deployment**, and **infrastructure orchestration**.  
It is **agentless**, using **SSH (Linux)** or **WinRM (Windows)** to manage remote systems.

---

## 🧩 **Installation on Different OS**

### 🟦 Amazon Linux 2
```bash
sudo yum update -y
sudo amazon-linux-extras install ansible2 -y
```
OR (using pip if extras not available):
```bash
sudo yum install python3-pip -y
pip3 install ansible
```

---

### 🟦 Amazon Linux 2023
```bash
sudo dnf install python3-pip -y
pip3 install ansible
```
(Optional latest community version):
```bash
pip3 install ansible-core --upgrade
```

---

### 🟩 Ubuntu / Debian
```bash
sudo apt update -y
sudo apt install -y ansible
```
OR via pip:
```bash
sudo apt install -y python3-pip
pip3 install ansible
```

---

## 🧾 **Check Ansible Version**
```bash
ansible --version
```
🧩 Output example:
```
ansible [core 2.16.4]
  python version = 3.9.16
  config file = /etc/ansible/ansible.cfg
```

---

## ⚙️ **Common Ansible Commands**

| Command | Description |
|----------|-------------|
| `ansible --version` | Show installed Ansible version |
| `ansible all -m ping` | Test connectivity to all hosts |
| `ansible-inventory --list` | Show inventory file in JSON |
| `ansible -m setup all` | Gather system facts |
| `ansible-playbook site.yml` | Run playbook |
| `ansible-playbook --syntax-check site.yml` | Validate YAML syntax |
| `ansible-playbook --check site.yml` | Dry run (no changes applied) |
| `ansible-doc -l` | List all available modules |
| `ansible-config list` | List all Ansible configuration options |
| `ansible localhost -m debug -a "var=ansible_facts"` | Show variables |
| `ansible-playbook -e "var=value"` | Pass extra variables dynamically |
| `ansible-galaxy list` | List installed roles |
| `ansible-config view` | View default Ansible configuration |

---

## 🧱 **Playbook Syntax Check & Dry Run**

### ✅ Syntax Check
```bash
ansible-playbook site.yml --syntax-check
```
Ensures your playbook YAML format is valid.

### 🧪 Dry Run (Check Mode)
```bash
ansible-playbook site.yml --check
```
Simulates playbook run **without making any changes** to servers.

---

## 🧩 **What are Ansible Modules?**
**Modules** are small programs that Ansible runs on target systems to perform specific actions.

🧱 **Examples of Common Modules:**

| Module | Purpose |
|---------|----------|
| `ping` | Test connection |
| `command` | Run a command |
| `shell` | Execute shell commands |
| `copy` | Copy files to target |
| `template` | Use Jinja2 templates |
| `yum` / `apt` | Manage packages |
| `service` | Manage services |
| `user` | Manage user accounts |
| `file` | Manage file permissions and attributes |
| `git` | Clone repositories |
| `reboot` | Reboot remote machines |

### 🔍 List All Modules
```bash
ansible-doc -l
```

### 📖 View Module Documentation
```bash
ansible-doc <module_name>
```
Example:
```bash
ansible-doc yum
```

---

## 🧠 **What are Ansible Variables (Vars)?**
**Variables (vars)** allow dynamic values in playbooks, templates, and roles.

### 🔹 Types of Variables

| Type | Description |
|-------|-------------|
| **Playbook vars** | Defined inside a playbook under `vars:` |
| **Host vars / Group vars** | Defined in `host_vars/` or `group_vars/` directories |
| **Facts** | Auto-collected system data |
| **Extra vars** | Passed dynamically via CLI |
| **Registered vars** | Store results from tasks |

---

### 📄 Example Playbook Using Vars
```yaml
- name: Install package using variables
  hosts: web
  become: yes
  vars:
    pkg_name: nginx
  tasks:
    - name: Install web package
      apt:
        name: "{{ pkg_name }}"
        state: present
```

---

### 🔍 List Available Variables
```bash
ansible all -m setup
```
OR for a single host:
```bash
ansible hostname -m setup
```
To display a specific variable:
```bash
ansible localhost -m debug -a "var=ansible_distribution"
```

---

## 🧾 **List of Useful Ansible CLI Commands**

| Command | Usage |
|----------|--------|
| `ansible` | Run ad-hoc commands |
| `ansible-config` | Manage Ansible configuration |
| `ansible-console` | Interactive shell mode |
| `ansible-doc` | Module documentation |
| `ansible-galaxy` | Manage roles and collections |
| `ansible-inventory` | Display or verify inventory |
| `ansible-playbook` | Execute playbooks |
| `ansible-pull` | Pull mode (nodes pull from SCM) |
| `ansible-vault` | Encrypt/decrypt sensitive files |

---

## 🔐 **Bonus: Ansible Vault Example**
Encrypt a secrets file:
```bash
ansible-vault create secrets.yml
```
Decrypt for editing:
```bash
ansible-vault edit secrets.yml
```
Use in playbook:
```bash
ansible-playbook site.yml --ask-vault-pass
```

---

## 🧰 **Troubleshooting & Validation**

| Task | Command |
|------|----------|
| Validate inventory | `ansible-inventory --list -y` |
| Check configuration path | `ansible --version` |
| Show current config | `ansible-config dump` |
| View environment variables | `env | grep ANSIBLE` |

---

## 💬 **In Summary**
> “Ansible makes automation simple — no agents, no complexity.  
> Install it, write your YAML playbook, and automate your servers with confidence.”  

---

<p align="center">
  <img src="https://capsule-render.vercel.app/api?type=waving&color=0:1E90FF,100:0A192F&height=140&section=footer"/>
</p>
