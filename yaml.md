<!-- HEADER -->
<p align="center">
  <img src="https://capsule-render.vercel.app/api?type=waving&color=0:0A192F,100:1E90FF&height=200&section=header&text=📘%20YAML%20Complete%20Guide&fontSize=34&fontColor=ffffff&animation=twinkling"/>
</p>

<p align="center">
  <img src="https://readme-typing-svg.herokuapp.com?duration=4000&pause=800&color=1E90FF&center=true&vCenter=true&width=950&lines=Understanding+YAML;Why+We+Use+It+in+DevOps+and+Automation;Syntax%2C+Rules%2C+and+Real+Examples"/>
</p>

---

## 🧠 What is YAML?
**YAML** (YAML Ain’t Markup Language) is a **human‑friendly data format** for configuration and data exchange. It’s widely used in DevOps tools like **Ansible, Docker, Kubernetes, GitHub Actions, Terraform**, and more.

---

## 🎯 Why YAML?
- ✅ Human‑readable and clean
- ✅ Perfect for configs and automation (declarative)
- ✅ Language‑agnostic (works with Python, Go, Java, etc.)
- ✅ Supports lists, maps, nesting, anchors, and multi‑line strings

---

## 🧩 Core Syntax (Cheat Sheet)
| Concept | Example | Notes |
|---|---|---|
| Key‑Value | `name: Esha` | Colon + space after key |
| List | `- AWS` `- Azure` | Use `-` for each item |
| Map (object) | `person: {name: Esha, role: DevOps}` | Inline or multi‑line |
| Nesting | 2 spaces | ❌ No tabs |
| Comment | `# this is a comment` | Ignored by parser |
| Strings | `'text'` / `"text"` / `text` | Quotes optional |
| Boolean | `true` / `false` | Lowercase |
| Null | `null` or `~` | Empty value |
| Multi‑line | `|` (literal) / `>` (folded) | Keep vs. fold newlines |
| Anchors | `&name` and `*name` | Reuse values |

---

## 🧾 Full YAML Example — **Person Profile** (Complete Syntax Demo)

> This example includes: **name**, **phone numbers**, **age**, **address**, **job**, **location**, **designation**, and more (lists, maps, anchors, multi‑line strings, booleans, nulls).  
> Copy‑paste into a YAML linter to explore.

```yaml
# person.yaml
person:
  name:
    first: Arjun
    last: Mehta
    full: &fullname "Arjun Mehta"        # anchor for reuse

  contact:
    phones:
      - type: mobile
        number: "+91-98765-43210"
      - type: work
        number: "+91-22-4000-1234"
    email: arjun.mehta@example.com

  age: 29
  birth_date: 1996-07-14                 # ISO date as string
  active: true

  address:
    line1: "201, Sunrise Apartments"
    line2: "MG Road"
    city: Mumbai
    state: MH
    postcode: "400001"
    country: India
    coordinates: { lat: 19.076, lon: 72.8777 }

  employment:
    designation: Senior DevOps Engineer
    department: Platform Engineering
    company: Binnbash Technologies
    location: Mumbai
    start_date: 2022-02-01
    salary_in_inr: 2400000
    remote: hybrid                      # enum-like field
    skills: [Ansible, Docker, Kubernetes, AWS, Terraform, Linux]
    certifications:
      - name: AWS Solutions Architect Associate
        year: 2024
      - name: CKAD
        year: 2023

  social:
    linkedin: "https://linkedin.com/in/arjunmehta"
    github: "https://github.com/arjunmehta"

  emergency_contacts:
    - name: "Meera Mehta"
      relation: Mother
      phone: "+91-98111-22222"
    - name: "Rohit Mehta"
      relation: Brother
      phone: "+91-98222-33333"

  notes: |
    This is a multi-line block.
    Newlines are preserved exactly.
    Great for README text or certificates.

  bio: >
    Arjun is a hands-on DevOps engineer with
    strong experience in automation and cloud.
    This text uses folded style, so newlines
    become spaces when parsed.

  aliases:
    - *fullname                         # alias reusing anchor value
    - "A. Mehta"

  preferences:
    newsletter: false
    languages:
      - en
      - hi

  vehicles: []                           # empty list
  spouse: null                           # explicit null
```

---

## 🧪 Mini Examples by Tool

### 🅰️ Ansible (Install & Start Nginx)
```yaml
- name: Install and start web server
  hosts: web
  become: yes
  tasks:
    - name: Install nginx
      apt:
        name: nginx
        state: present
    - name: Start service
      service:
        name: nginx
        state: started
```

### 🐳 Docker Compose
```yaml
version: '3'
services:
  web:
    image: nginx:latest
    ports:
      - "8080:80"
```

### ☸️ Kubernetes Deployment
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: web-app
spec:
  replicas: 2
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
        - name: nginx
          image: nginx:latest
          ports:
            - containerPort: 80
```

### ⚙️ GitHub Actions
```yaml
name: CI Pipeline
on: [push]
jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - run: echo "Build OK"
```

---

## ✅ Tips
- Use **2 spaces** for indentation (never tabs)
- Validate with an online linter (e.g., *YAML Checker*)
- Quote strings containing special chars (`:`, `#`, `@`, `*`)
- Keep data consistent (e.g., ISO dates as strings)

---

<p align="center">
  <img src="https://capsule-render.vercel.app/api?type=waving&color=0:1E90FF,100:0A192F&height=140&section=footer"/>
</p>
