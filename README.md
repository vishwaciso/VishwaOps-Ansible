# VishwaOps-Ansible

<!-- Header -->
<p align="center">
  <img src="https://capsule-render.vercel.app/api?type=waving&color=0:101820,100:EE3124&height=200&section=header&text=🚀%20DevOps%20Automation%20Express%20(Ansible%20+%20GitHub%20Actions)&fontSize=34&fontColor=ffffff&animation=twinkling"/>
</p>

<p align="center">
  <img src="https://readme-typing-svg.herokuapp.com?duration=3000&pause=800&color=EE3124&center=true&vCenter=true&width=850&lines=Trainer+Guide+|+Binnbash+Academy;DevOps+Automation+Express+Workshop;YAML+→+Ansible+→+Roles+→+Vault+→+GitHub+Actions+Integration"/>
</p>

---

## 🎯 **Workshop Overview**

**Audience:** DevOps / Infrastructure / Developers (Beginner–Intermediate)  
**Mode:** Live demo + slides (optional)  
**Goal:** Teach YAML → Ansible (Linux + Windows) → Roles + Vault → GitHub Actions integration

---

## 🧩 **Session 1: YAML + Ansible Essentials**

### 🧭 Welcome & Objective
- Introduction to DevOps Automation Express
- Overview of session goals (YAML → Ansible → GitHub Actions)
- Quick demo preview (Linux + Windows automation)

### 🧠 YAML Primer
- Introduction to YAML syntax and structure
- Key-value pairs, lists, indentation (2 spaces), and nesting
- No tabs allowed — use spaces only
- Example: YAML configuration for an application
- Trainer tip: Use [yamlchecker.com](https://yamlchecker.com) for syntax validation
- Interactive question: Explain meaning of ports or env.debug

### ⚙️ What is Ansible?
- Ansible is agentless — connects via SSH (Linux) or WinRM (Windows)
- Core Concepts:
  - **Inventory** — List of servers
  - **Modules** — Built-in automation components
  - **Playbooks** — YAML automation scripts
  - **Handlers** — Trigger-based actions
  - **Roles** — Reusable automation structures
- Architecture Diagram:
  ```
  Control Node (Ansible)
     ├── Linux Host (SSH)
     └── Windows Host (WinRM)
  ```
- Trainer analogy: “Ansible is a remote control for servers.”

### 🧱 Hands-On: First Ansible Playbook
- Install Ansible (`apt install -y ansible`)
- Create `inventory.ini` for Linux and Windows hosts
- Write `site.yml` playbook for Nginx (Linux) and IIS (Windows)
- Run the playbook: `ansible-playbook -i inventory.ini site.yml`
- Result: Automated installation on both OS types
- Key takeaway: One YAML file, two platforms!

### 🧩 Roles + Vault (Concept + Demo)
#### 🧱 Ansible Roles
- Definition: Structured automation similar to reusable functions
- Folder structure:
  ```
  roles/
    webserver/
      tasks/main.yml
      handlers/main.yml
      templates/index.html.j2
      vars/main.yml
  ```
- Command: `ansible-galaxy init roles/webserver`
- Playbook integration example with roles

#### 🔐 Ansible Vault
- Purpose: Encrypt sensitive data (passwords, tokens, keys)
- Command: `ansible-vault create secrets.yml`
- Run with: `ansible-playbook -i inventory.ini site.yml --ask-vault-pass`
- Tip: “Vault = Security. No secrets in plain text.”

---

## ⚙️ **Session 2: GitHub Actions + Ansible Integration**

### 🧭 GitHub Actions Overview
- Introduction to GitHub’s CI/CD platform
- Workflow structure:
  - **Workflows**: YAML-based pipelines in `.github/workflows/`
  - **Jobs**: Logical task groups (build, deploy, etc.)
  - **Steps**: Commands or actions
  - **Runners**: Environments executing workflows
- Example CI workflow:
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
- Goal: Automate Ansible playbook execution via GitHub
- Create workflow: `.github/workflows/deploy.yml`
- Workflow stages:
  1. Checkout repository  
  2. Install Ansible and dependencies  
  3. Run playbook (`ansible-playbook -i inventory.ini site.yml`)
- Add GitHub Secrets:
  - `SSH_KEY`, `ANSIBLE_USER`, `VAULT_PASS`
- Reference secrets in YAML:
  ```yaml
  env:
    ANSIBLE_VAULT_PASSWORD_FILE: ${{ secrets.VAULT_PASS }}
  ```
- Result: Push → GitHub Action triggers → Ansible runs on servers automatically

### 💻 Live Demo + Recap
- Git push → Action triggers → Deployment starts
- Walkthrough of each workflow step
- Verify on browser (Nginx or IIS endpoint)
- Key result: Fully automated cross-platform deployment

### 🏁 Wrap-Up
- Recap: YAML → Ansible → Roles → Vault → GitHub Actions
- Summary Table:

| Concept | Tool | Benefit |
|----------|------|----------|
| **YAML** | Ansible + GitHub Actions | Common automation language |
| **Roles** | Ansible | Reusable structure |
| **Vault** | Ansible | Secrets encryption |
| **GitHub Actions** | GitHub | CI/CD automation |
| **Integration** | Both | End-to-end deployment pipeline |

### 💬 Manager Impression Line
> “We achieved cross-platform DevOps automation — YAML-based workflows, roles for structure, vaults for security, and GitHub Actions for CI/CD.”

---

## 🎁 **Optional Add-ons (If Time Allows)**
- Slack notification integration in GitHub Actions  
- Dynamic AWS inventory integration  
- Ansible Tower (AWX) overview  
- Vault password integration with GitHub Secrets  

---

## ✅ **Trainer Tips**
- Keep demos short and clean — use localhost or simple IPs  
- Prepare `inventory.ini` in advance  
- Demonstrate both Linux + Windows automation for impact  
- End with a live GitHub Actions run (manager wow factor)  

---

<p align="center">
  <img src="https://capsule-render.vercel.app/api?type=waving&color=0:EE3124,100:101820&height=140&section=footer"/>
</p>
