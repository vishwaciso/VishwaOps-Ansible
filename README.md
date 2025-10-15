<!-- HEADER -->
<p align="center">
  <img src="https://capsule-render.vercel.app/api?type=waving&color=0:0A192F,100:1E90FF&height=200&section=header&text=🚀%20DevOps%20Automation%20Express%20(Ansible%20+%20GitHub%20Actions)&fontSize=32&fontColor=ffffff&animation=twinkling"/>
</p>

<p align="center">
  <img src="https://readme-typing-svg.herokuapp.com?duration=3500&pause=800&color=1E90FF&center=true&vCenter=true&width=850&lines=Trainer+Guide+|+Binnbash+Academy;Complete+Workshop+Topics+and+Flow;YAML+→+Ansible+→+Roles+→+Vault+→+GitHub+Actions+Integration"/>
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Automation-Ansible-blue?style=for-the-badge&logo=ansible&logoColor=white"/>
  <img src="https://img.shields.io/badge/CI/CD-GitHub%20Actions-0078D7?style=for-the-badge&logo=githubactions&logoColor=white"/>
  <img src="https://img.shields.io/badge/Markup-YAML-1572B6?style=for-the-badge&logo=yaml&logoColor=white"/>
</p>

---

## 🧭 **Workshop Topics Overview**

| Section | Topics Covered |
|----------|----------------|
| **Workshop Goal** | Teach end-to-end DevOps automation using YAML → Ansible → Roles → Vault → GitHub Actions. |
| **Session 1: YAML + Ansible Essentials** | YAML syntax, Ansible basics, playbooks, modules, handlers, inventory, roles, and vault encryption. |
| **Session 2: GitHub Actions Integration** | CI/CD workflows, YAML structure, secrets management, live deployment automation, recap. |
| **Bonus & Tips** | Slack notifications, AWS inventory, Ansible Tower, vault integration, and trainer guidance. |

---

## 🎯 **Workshop Overview**

**Audience:** DevOps / Infrastructure / Developers (Beginner–Intermediate)  
**Mode:** Live demo + slides (optional)  
**Goal:** YAML → Ansible (Linux + Windows) → Roles + Vault → GitHub Actions integration  

---

## 🧩 **Session 1: YAML + Ansible Essentials**

### 1️⃣ Introduction
- Overview of the complete automation pipeline  
- Key objective: connect YAML → Ansible → GitHub Actions  
- Demo flow: Linux + Windows automation using a single playbook  

### 2️⃣ YAML Primer (YAML Basics)
📘 **Concepts:**
- YAML syntax and indentation (2 spaces)  
- Key-value pairs, lists, and nesting  
- Avoid tabs — use spaces only  
- YAML validation with [yamlchecker.com](https://yamlchecker.com)  
- Practical example (`app.yaml`) showing ports and environment variables  

💡 **Trainer Tip:** Ask students to explain what `ports` and `env.debug` represent.  

### 3️⃣ What is Ansible?
⚙️ **Concept & Architecture**
- Agentless automation tool connecting via SSH (Linux) / WinRM (Windows)  
- Components: Inventory, Modules, Playbooks, Handlers, Roles  
- Analogy: “Ansible is a remote control for servers.”  

📊 **Architecture Diagram:**
```
Control Node (Ansible)
 ├── Linux Host (SSH)
 └── Windows Host (WinRM)
```

### 4️⃣ Hands-On: First Ansible Playbook
🧱 **Steps**
1. Install Ansible (`apt install -y ansible`)  
2. Create `inventory.ini` with Linux & Windows hosts  
3. Write `site.yml` playbook with Nginx (Linux) + IIS (Windows)  
4. Run: `ansible-playbook -i inventory.ini site.yml`  
5. Verify installation on both systems  

🎯 **Outcome:** One YAML playbook automates both platforms.  

### 5️⃣ Roles and Vault
#### 🧱 Ansible Roles
- Purpose: organize reusable automation logic  
- Structure: `tasks/`, `handlers/`, `templates/`, `vars/`  
- Command: `ansible-galaxy init roles/webserver`  
- Example: Using roles in playbook for modular design  

#### 🔐 Ansible Vault
- Purpose: encrypt secrets, passwords, and tokens  
- Command: `ansible-vault create secrets.yml`  
- Execution: `ansible-playbook -i inventory.ini site.yml --ask-vault-pass`  
- Benefit: secure automation with encrypted credentials  

---

## ⚙️ **Session 2: GitHub Actions + Ansible Integration**

### 6️⃣ GitHub Actions Overview
💡 **Concept:** GitHub’s native CI/CD engine.  
🧩 **Core Components:**
- **Workflows:** YAML-based automation pipelines (`.github/workflows/`)  
- **Jobs:** logical task groupings (build, test, deploy)  
- **Steps:** shell commands or pre-built actions  
- **Runners:** execution environments  

📘 **Example Workflow**
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

### 7️⃣ Demo: Ansible + GitHub Actions
🚀 **Goal:** Automate Ansible playbook execution directly from GitHub.  

📁 **Workflow File:** `.github/workflows/deploy.yml`
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
🔐 **Add Secrets in GitHub:**  
`SSH_KEY`, `ANSIBLE_USER`, `VAULT_PASS`  
```yaml
env:
  ANSIBLE_VAULT_PASSWORD_FILE: ${{ secrets.VAULT_PASS }}
```

✅ **Result:** Push → GitHub Actions → Automated Ansible run → Deployed servers.  

---

## 💻 **Live Demo + Recap**
- Push code → workflow triggers automatically  
- Watch logs in Actions tab  
- Validate deployment (Nginx or IIS accessible)  
- Recap table summarizing key tools and benefits  

| Concept | Tool | Benefit |
|----------|------|----------|
| YAML | Ansible + GitHub Actions | Universal automation syntax |
| Roles | Ansible | Modular, reusable automation |
| Vault | Ansible | Secure secrets management |
| GitHub Actions | GitHub | Automated CI/CD pipeline |
| Integration | Both | End-to-end DevOps workflow |

💬 **Key Takeaway:** Cross-platform automation with YAML-based workflows, reusable roles, vault encryption, and integrated CI/CD pipelines.

---

## 🎁 **Optional Add-ons (If Time Allows)**
- Slack notification integration in GitHub Actions  
- Dynamic AWS inventory configuration  
- Ansible Tower (AWX) introduction  
- Vault secret injection via GitHub Secrets  

---

## ✅ **Trainer Tips**
⚡ Keep demos short and focused (use local or simple IPs)  
🧾 Prepare `inventory.ini` and playbooks in advance  
💡 Show both Linux + Windows setups for impact  
🎬 End with live GitHub Actions demo to impress managers  

---

<p align="center">
  <img src="https://capsule-render.vercel.app/api?type=waving&color=0:1E90FF,100:0A192F&height=140&section=footer"/>
</p>
