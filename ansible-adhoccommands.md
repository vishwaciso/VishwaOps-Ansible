<!-- HEADER -->
<p align="center">
  <img src="https://capsule-render.vercel.app/api?type=waving&color=0:0A192F,100:1E90FF&height=200&section=header&text=⚡%20Ansible%20Ad-Hoc%20Commands&fontSize=32&fontColor=ffffff&animation=twinkling"/>
</p>

<p align="center">
  <img src="https://readme-typing-svg.herokuapp.com?duration=3500&pause=800&color=1E90FF&center=true&vCenter=true&width=900&lines=Instant+Automation+with+Ansible+Ad-Hoc+Commands;Quick+One-Line+Actions+on+Your+Servers"/>
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Automation-Ansible-blue?style=for-the-badge&logo=ansible&logoColor=white"/>
  <img src="https://img.shields.io/badge/Mode-Ad--Hoc-1E90FF?style=for-the-badge"/>
</p>

---

## ⚙️ **What Are Ansible Ad-Hoc Commands?**

> 🧠 **Definition:**  
> An **Ansible Ad-Hoc Command** is a **one-line command** used to perform a **quick task** across multiple remote systems — **without writing a playbook**.  
> It’s ideal for simple, one-time jobs such as package installation, service restarts, or checking connectivity.

---

## 🎯 **Why Use Ad-Hoc Commands?**

| Purpose | Example |
|----------|----------|
| 🚀 Quick task execution | Restart a service, copy a file, check uptime |
| 🧪 Testing connectivity or privileges | Verify SSH or sudo access |
| ⚡ Run-once actions | Apply updates, reboot servers |
| 🔍 Troubleshooting | Check configurations or system facts |

---

## 💡 **Syntax**

```bash
ansible <pattern> -m <module> -a "<arguments>"
```

| Parameter | Description |
|------------|-------------|
| `<pattern>` | Which hosts or group to target (from your inventory) |
| `-m <module>` | The module to run (like `ping`, `command`, `yum`, etc.) |
| `-a "<arguments>"` | Arguments passed to that module |

✅ **Example:**
```bash
ansible all -m ping
```
> Checks connectivity to all hosts in inventory.

---

## 🔧 **Common Ad-Hoc Examples**

### 🧭 1. Check Connectivity
```bash
ansible all -m ping
```
🔹 Uses the built-in **ping** module to test communication via SSH.

---

### 📦 2. Install a Package (Linux)
```bash
ansible web -m apt -a "name=nginx state=present" --become
```
🔹 Installs Nginx on all hosts in the `web` group.

---

### 🔁 3. Start or Restart a Service
```bash
ansible web -m service -a "name=nginx state=restarted" --become
```
🔹 Restarts Nginx across all `web` servers.

---

### 📋 4. Run Shell or Command
```bash
ansible db -m shell -a "df -h"
ansible all -m command -a "uptime"
```
🔹 Runs arbitrary shell/command on target hosts.

---

### 📁 5. Copy Files
```bash
ansible web -m copy -a "src=/etc/hosts dest=/tmp/hosts.bak"
```
🔹 Copies a local file from controller to remote servers.

---

### 🔥 6. Reboot Servers
```bash
ansible all -m reboot --become
```
🔹 Reboots all managed nodes safely with elevated privileges.

---

### 🧩 7. Gather Facts
```bash
ansible all -m setup
```
🔹 Displays system information like OS, IP, memory, CPU.

---

## 🧠 **When to Use Ad-Hoc Commands**

| Situation | Use Ad-Hoc? | Reason |
|------------|-------------|--------|
| One-time quick check or fix | ✅ Yes | No need for playbook |
| Repetitive configuration management | ❌ No | Use playbooks instead |
| Testing inventory connection or privilege escalation | ✅ Yes | Fast and simple |
| Deployment or multi-step logic | ❌ No | Playbooks are better |

---

## ⚙️ **Authentication & Privileges**

Add `--become` (or `-b`) to run with sudo privileges:
```bash
ansible all -m yum -a "name=httpd state=latest" -b
```
Specify SSH user or key:
```bash
ansible all -m ping -u ubuntu --private-key ~/.ssh/id_rsa
```

---

## 🧩 **Real-World Example**

```bash
ansible web -m shell -a "systemctl status nginx | grep Active"
```
🔹 Checks if Nginx is running on all web servers.

```bash
ansible db -m shell -a "ps aux | grep mysql"
```
🔹 Verifies MySQL processes on database hosts.

---

## 📘 **Comparison: Ad-Hoc vs Playbook**

| Feature | Ad-Hoc | Playbook |
|----------|---------|----------|
| Type | One-line command | YAML file |
| Best for | Quick fixes | Full automation |
| Reusability | ❌ No | ✅ Yes |
| Complexity | Simple | Advanced |
| Logging | Minimal | Detailed |
| Version control | Hard | Easy |

---

## 💬 **In Short**

> “Ad-Hoc commands are your DevOps Swiss-army knife —  
> perfect for **instant automation** and quick control,  
> while playbooks handle **long-term, structured workflows**.”

---

<p align="center">
  <img src="https://capsule-render.vercel.app/api?type=waving&color=0:1E90FF,100:0A192F&height=140&section=footer"/>
</p>
