<!-- HEADER -->
<p align="center">
  <img src="https://capsule-render.vercel.app/api?type=waving&color=0:0A192F,100:1E90FF&height=200&section=header&text=📘%20Ansible%20Inventory%20%26%20Groups%20Explained&fontSize=34&fontColor=ffffff&animation=twinkling"/>
</p>

<p align="center">
  <img src="https://readme-typing-svg.herokuapp.com?duration=3500&pause=800&color=1E90FF&center=true&vCenter=true&width=900&lines=Inventory+|+Groups+|+Parent+%2B+Child+|+Group+Vars+|+Host+Vars+|+Dynamic+Inventory"/>
</p>

---

## 🧠 **What is an Ansible Inventory?**
**Ansible Inventory** is a file (default: `/etc/ansible/hosts`) that defines **which servers** Ansible manages and how they are grouped or accessed.  
It contains information such as:
- Hostnames / IPs of servers  
- SSH credentials (user, port, private key)
- Groupings (e.g., web, db, dev)
- Variables (group_vars, host_vars)

📘 **Purpose:**  
Inventory tells Ansible *where* to run automation — the playbooks define *what* to do.

---

## 🧩 **Types of Inventories**
| Type | Description | Example |
|------|--------------|----------|
| **Static Inventory** | Defined manually in `.ini` or `.yaml` files | `/etc/ansible/hosts` |
| **Dynamic Inventory** | Generated dynamically from cloud providers (AWS, Azure, GCP, etc.) | AWS EC2 plugin |
| **Combined Inventory** | Merge static and dynamic sources | `/etc/ansible/hosts` + AWS plugin |

---

## 🗂️ **Example: Static Inventory**

### INI Format
```ini
[webservers]
web01 ansible_host=192.168.1.10 ansible_user=ubuntu
web02 ansible_host=192.168.1.11 ansible_user=ubuntu

[dbservers]
db01 ansible_host=192.168.1.20 ansible_user=ec2-user

[loadbalancers]
lb01 ansible_host=192.168.1.5 ansible_user=admin

[production:children]
webservers
dbservers
loadbalancers
```

### YAML Format
```yaml
all:
  children:
    webservers:
      hosts:
        web01:
          ansible_host: 192.168.1.10
          ansible_user: ubuntu
        web02:
          ansible_host: 192.168.1.11
          ansible_user: ubuntu
    dbservers:
      hosts:
        db01:
          ansible_host: 192.168.1.20
          ansible_user: ec2-user
    loadbalancers:
      hosts:
        lb01:
          ansible_host: 192.168.1.5
          ansible_user: admin
    production:
      children:
        - webservers
        - dbservers
        - loadbalancers
```

---

## 🧩 **Parent Group and Child Group**
Ansible supports **nested groups** using the `:children` keyword.  
✅ Parent group → contains other groups  
✅ Child group → actual groups or hosts

Example:
```ini
[frontend]
web01
web02

[backend]
db01
db02

[production:children]
frontend
backend
```

---

## 🧾 **Group Variables (`group_vars/`)**
Group variables apply to all hosts in that group.

📁 Directory structure:
```
inventory/
 ├── group_vars/
 │   ├── webservers.yml
 │   └── dbservers.yml
 ├── host_vars/
 │   ├── web01.yml
 │   └── db01.yml
 └── inventory.ini
```

### Example: `group_vars/webservers.yml`
```yaml
---
http_port: 80
doc_root: /var/www/html
```

### Example: `host_vars/web01.yml`
```yaml
---
ansible_host: 192.168.1.10
custom_hostname: web01-prod
```

---

## 🧱 **Task Example: Using Inventory & Group Vars**
```yaml
---
- name: Ansible Inventory & Groups Demo
  hosts: all
  become: yes

  tasks:
    - name: Print host info
      ansible.builtin.debug:
        msg: "Host: {{ inventory_hostname }} | IP: {{ ansible_host }} | Group: {{ group_names }}"

    - name: Install Nginx on web servers
      ansible.builtin.package:
        name: nginx
        state: present
      when: "'webservers' in group_names"

    - name: Install MariaDB on DB servers
      ansible.builtin.package:
        name: mariadb-server
        state: present
      when: "'dbservers' in group_names"

    - name: Create index page
      ansible.builtin.copy:
        content: "Welcome to {{ inventory_hostname }} on port {{ http_port }}"
        dest: "{{ doc_root }}/index.html"
      when: "'webservers' in group_names"
      notify: Restart Nginx

  handlers:
    - name: Restart Nginx
      ansible.builtin.service:
        name: nginx
        state: restarted
```

---

## 🧰 **Dynamic Inventory Example (AWS EC2)**
```yaml
plugin: amazon.aws.ec2
regions:
  - ap-south-1
keyed_groups:
  - key: tags.Name
    prefix: tag
```

Command:
```bash
ansible-inventory -i aws_ec2.yml --graph
```

---

## 🧠 **Common Inventory Commands**
| Command | Purpose |
|----------|----------|
| `ansible-inventory -i inventory.ini --list` | Display full inventory in JSON |
| `ansible-inventory -i inventory.ini --graph` | Show hierarchy tree |
| `ansible all --list-hosts` | List all managed hosts |
| `ansible webservers --list-hosts` | Show only webservers |
| `ansible webservers -m ping` | Test connectivity to that group |
| `ansible-playbook -i inventory.ini site.yml` | Run playbook on defined inventory |

---

## ⚙️ **When to Use Inventory Variables**
| Type | Scope | Example |
|------|--------|----------|
| **host_vars** | Host-specific | Database credentials, custom hostname |
| **group_vars** | Group-wide | Common ports, directory paths |
| **extra_vars** | Command line vars | `-e "var=value"` |
| **playbook vars** | Defined in YAML playbook | `vars:` block |

---

## ✅ **Summary**
| Concept | Meaning |
|----------|----------|
| **Inventory** | List of hosts & groups |
| **Static Inventory** | Manually defined file |
| **Dynamic Inventory** | Auto-generated (cloud or script) |
| **Group Vars** | Variables shared across a group |
| **Host Vars** | Variables for specific host |
| **Parent Group** | Contains multiple child groups |
| **Child Group** | Contains actual hosts |
| **Inventory Variables** | Values Ansible uses for configuration |

---

<p align="center">
  <img src="https://capsule-render.vercel.app/api?type=waving&color=0:1E90FF,100:0A192F&height=140&section=footer"/>
</p>
