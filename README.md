<!-- HEADER -->
<p align="center">
  <img src="https://capsule-render.vercel.app/api?type=waving&color=0:0A192F,100:1E90FF&height=200&section=header&text=🚀%20DevOps%20Automation%20Express%20(Ansible%20+%20GitHub%20Actions)&fontSize=32&fontColor=ffffff&animation=twinkling"/>
</p>

<p align="center">
  <img src="https://readme-typing-svg.herokuapp.com?duration=3500&pause=800&color=1E90FF&center=true&vCenter=true&width=850&lines=Trainer+Guide+|+Binnbash+Academy;YAML+→+Ansible+→+Roles+→+Vault+→+GitHub+Actions+Integration"/>
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Automation-Ansible-blue?style=for-the-badge&logo=ansible&logoColor=white"/>
  <img src="https://img.shields.io/badge/CI/CD-GitHub%20Actions-0078D7?style=for-the-badge&logo=githubactions&logoColor=white"/>
  <img src="https://img.shields.io/badge/Markup-YAML-1572B6?style=for-the-badge&logo=yaml&logoColor=white"/>
</p>

---

## 📘 **Table of Contents**
- [🎯 Workshop Overview](#-workshop-overview)
- [🧩 Session 1: YAML + Ansible Essentials](#-session-1-yaml--ansible-essentials)
- [⚙️ Session 2: GitHub Actions + Ansible Integration](#️-session-2-github-actions--ansible-integration)
- [🎁 Optional Add-ons](#-optional-add-ons-if-time-allows)
- [✅ Trainer Tips](#-trainer-tips)

---

## 🎯 **Workshop Overview**

**Audience:** DevOps / Infrastructure / Developers (Beginner–Intermediate)  
**Mode:** Live demo + slides (optional)  
**Goal:** Teach YAML → Ansible (Linux + Windows) → Roles + Vault → GitHub Actions integration

---

## 🧩 **Session 1: YAML + Ansible Essentials**

### 🧭 Welcome & Objective
> ✨ _“Welcome to our DevOps Automation Express!”_  
> Overview of session goals: YAML → Ansible → GitHub Actions → Cross-platform automation

### 🧠 YAML Primer
📘 **Concepts Covered:**
- YAML syntax and indentation (2 spaces only)
- Key-value pairs, lists, and nesting
- Real-world example configuration block  
- [yamlchecker.com](https://yamlchecker.com) for syntax validation

💡 **Trainer Tip:** Ask participants to explain what `ports` or `env.debug` means.

### ⚙️ What is Ansible?
🔹 **Definition:** Agentless automation via SSH (Linux) or WinRM (Windows).  
🔹 **Core Components:**
- **Inventory** → list of servers
- **Modules** → automation functions (apt, win_feature)
- **Playbooks** → YAML automation scripts
- **Handlers** → trigger-based actions
- **Roles** → reusable code structures

📊 **Architecture:**
```
Control Node (Ansible)
 ├── Linux Host (SSH)
 └── Windows Host (WinRM)
```

### 🧱 Hands-On: First Ansible Playbook
```bash
sudo apt update
sudo apt install -y ansible
```
📄 Create **inventory.ini** and **site.yml**  
Run: `ansible-playbook -i inventory.ini site.yml`  
🎯 One YAML file — two OS platforms automated!

### 🧩 Roles + Vault
#### 🧱 Roles
📁 Folder structure:
```
roles/
  webserver/
    tasks/main.yml
    handlers/main.yml
    templates/index.html.j2
    vars/main.yml
```
Command: `ansible-galaxy init roles/webserver`

#### 🔐 Vault
```bash
ansible-vault create secrets.yml
ansible-playbook -i inventory.ini site.yml --ask-vault-pass
```
🔒 Secure sensitive credentials and tokens

---

## ⚙️ **Session 2: GitHub Actions + Ansible Integration**

### 🧭 Overview
💡 GitHub Actions = GitHub’s native **CI/CD engine**  
- Workflows → `.github/workflows/`  
- Jobs → group of steps  
- Steps → actions or shell commands  
- Runners → where workflows execute

```yaml
name: Demo CI
on: [push]
jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - run: echo "Hello DevOps!"
```

### 🧱 Demo: Ansible + GitHub Actions
📂 **Workflow:** `.github/workflows/deploy.yml`
```yaml
name: Deploy with Ansible
on:
  push:
    branches: [ "main" ]

jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout repository
        uses: actions/checkout@v4

      - name: Install Ansible
        run: |
          sudo apt update
          sudo apt install -y ansible python3-pip
          pip install pywinrm

      - name: Run Ansible Playbook
        env:
          ANSIBLE_HOST_KEY_CHECKING: False
        run: |
          ansible-playbook -i inventory.ini site.yml --ask-vault-pass
```

🔑 Add GitHub Secrets:  
`SSH_KEY`, `ANSIBLE_USER`, `VAULT_PASS`

```yaml
env:
  ANSIBLE_VAULT_PASSWORD_FILE: ${{ secrets.VAULT_PASS }}
```

🧩 **Result:** Push → Action triggers → Servers configured automatically.

---

## 💻 **Live Demo + Recap**
- Push → Workflow → Auto-deployment  
- Review logs in Actions tab  
- Validate on browser (Nginx / IIS)  
✅ Cross-platform DevOps automation achieved!

| Concept | Tool | Benefit |
|----------|------|----------|
| YAML | Ansible + GitHub Actions | Common automation language |
| Roles | Ansible | Reusable structure |
| Vault | Ansible | Secrets encryption |
| GitHub Actions | GitHub | CI/CD automation |
| Integration | Both | End-to-end deployment pipeline |

> 💬 “Cross-platform DevOps automation — YAML-based workflows, structured roles, secured vaults, and GitHub-powered CI/CD.”

---

## 🎁 **Optional Add-ons (If Time Allows)**
🪄 Slack notifications via GitHub Actions  
☁️ Dynamic AWS inventory integration  
🏢 Ansible Tower (AWX) overview  
🔑 Vault password management using GitHub Secrets

---

## ✅ **Trainer Tips**
⚡ Keep demos short & clean (use localhost or simple IPs)  
🧾 Pre-create `inventory.ini`  
💡 Demo both Linux + Windows automation  
🎬 End with a **live GitHub Action run** for maximum impact!

---

<p align="center">
  <img src="https://capsule-render.vercel.app/api?type=waving&color=0:1E90FF,100:0A192F&height=140&section=footer"/>
</p>
