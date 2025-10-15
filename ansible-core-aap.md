<!-- HEADER -->
<p align="center">
  <img src="https://capsule-render.vercel.app/api?type=waving&color=0:101820,100:1E90FF&height=200&section=header&text=⚙️%20Ansible%20vs%20Ansible%20Core%20%7C%20Versions%20%26%20Usage&fontSize=34&fontColor=ffffff&animation=twinkling"/>
</p>

<p align="center">
  <img src="https://readme-typing-svg.herokuapp.com?duration=3500&pause=800&color=1E90FF&center=true&vCenter=true&width=900&lines=What+is+Ansible%3F;What+is+Ansible+Core%3F;Version+Timeline%2C+When+to+Use+Which%2C+and+Key+Commands"/>
</p>

---

## 🌍 What is **Ansible**?
**Ansible** is an open‑source IT automation tool for **configuration management**, **application deployment**, and **orchestration**. It’s **agentless** (SSH for Linux, WinRM for Windows) and uses **YAML** playbooks.

---

## ⚙️ What is **Ansible Core**?
**Ansible Core** is the **lightweight engine** (CLI + essential modules + plugin system). It does not bundle community collections. Think of it as the runtime that the full Ansible distribution builds on.

| Component | Description |
|---|---|
| **Ansible Core** | Minimal automation engine (fast, small footprint) |
| **Ansible (Community Distribution)** | Core + curated collections/modules from Galaxy |
| **Ansible Automation Platform** | Red Hat enterprise suite (Controller/Tower, Hub, Mesh) |

---

## 🧩 Differences: **Ansible** vs **Ansible Core**
| Feature | **Ansible Core** | **Ansible (Community)** |
|---|---|---|
| Content | Built‑in modules/plugins only | Includes Core + community collections |
| Size | Small (good for containers) | Larger, batteries‑included |
| Ideal for | Minimal installs, custom collection dev | Full cloud/K8s/Windows automation out of the box |
| Install | `pip install ansible-core` | `pip install ansible` |

---

## 🧾 Version Timeline (quick view)
### Ansible (Community)
- **1.x → 2.0** (2013–2016): initial releases, agentless SSH
- **2.1 → 2.9** (2016–2019): Windows support matures, Vault improvements
- **3.x → 5.x** (2020–2021): content split into collections
- **6.x → 9.x** (2022–2025): Python 3, modern cloud/k8s integrations

### Ansible Core
- **2.9 (legacy)** → **2.10–2.14**: move to collections
- **2.15–2.17 (current era)**: stable, Python 3 only

> 🔎 Exact latest numbers vary by distro; check locally with the commands below.

---

## 🔍 How to Check **Ansible** & **Ansible Core** Info

### Show versions (which config file is in use, Python, paths)
```bash
ansible --version
ansible-core --version     # if installed separately
```

### Show full effective configuration (all defaults + overrides)
```bash
ansible-config dump
```

### Show where config comes from (paths & precedence)
```bash
ansible-config view
```

### List installed **collections** and **roles**
```bash
ansible-galaxy collection list
ansible-galaxy list
```

### List all available **modules** and read docs
```bash
ansible-doc -l                 # list modules
ansible-doc ansible.builtin.copy
ansible-doc -s ansible.builtin.copy   # parameter skeleton
```

### Inspect inventory
```bash
ansible-inventory --list -i inventory.ini
ansible-inventory --graph -i inventory.ini
```

---

## 🧰 Basic Day‑1 Commands (Cheat‑Sheet)
| Goal | Command |
|---|---|
| Ping all hosts | `ansible all -i inventory.ini -m ping` |
| Gather facts | `ansible all -i inventory.ini -m setup` |
| Run ad‑hoc package install | `ansible web -m package -a "name=nginx state=present" --become` |
| Run a playbook | `ansible-playbook -i inventory.ini site.yml` |
| Validate playbook syntax | `ansible-playbook --syntax-check site.yml` |
| Dry‑run (check mode) | `ansible-playbook --check site.yml` |
| Limit to a host/group | `ansible-playbook site.yml -l web01` |
| Run only tagged tasks | `ansible-playbook site.yml --tags web` |
| Pass extra vars | `ansible-playbook site.yml -e "env=prod version=1.2.3"` |

---

## 💡 When to Use Which?
| Scenario | Recommendation |
|---|---|
| Lightweight automation in containers/AMIs | **Ansible Core** |
| Teaching/learning with many ready modules | **Ansible (Community)** |
| Need AWS/Azure/GCP/K8s modules quickly | **Ansible (Community)** |
| Building/testing your own collections | **Ansible Core** |
| Enterprise RBAC, GUI, approvals, SSO | **Ansible Automation Platform** |

---

## 🚀 Install Examples

### Ubuntu / Debian
```bash
sudo apt update
sudo apt install -y ansible            # community distribution
# or minimal
sudo apt install -y python3-pip
pip3 install ansible-core
```

### Amazon Linux 2 / 2023
```bash
# Amazon Linux 2
sudo amazon-linux-extras install ansible2 -y   # community package
# or minimal
sudo yum install -y python3-pip && pip3 install ansible-core

# Amazon Linux 2023 (dnf)
sudo dnf install -y python3-pip && pip3 install ansible   # or ansible-core
```

### Python (pip) pinned versions
```bash
pip install "ansible==9.*"       # Community
pip install "ansible-core==2.17.*"
```

---

## ✅ Quick Examples to Prove It Works

### Ad‑hoc Ping (Linux)
```bash
ansible all -i inventory.ini -m ping
```

### Ad‑hoc WinRM Ping (Windows)
```bash
ansible windows -i inventory_windows.ini -m ansible.windows.win_ping
```

### Minimal Playbook and Run
```yaml
# site.yml
- hosts: web
  become: yes
  tasks:
    - name: Ensure nginx present
      ansible.builtin.package:
        name: nginx
        state: present
```
```bash
ansible-playbook -i inventory.ini site.yml
```

---

## 📝 Notes
- **`ansible`** package includes **Core + community content** (collections).  
- **`ansible-core`** is **smaller**; you’ll usually add collections you need:
  ```bash
  ansible-galaxy collection install community.general ansible.windows amazon.aws
  ```

---

<p align="center">
  <img src="https://capsule-render.vercel.app/api?type=waving&color=0:1E90FF,100:0A192F&height=140&section=footer"/>
</p>
