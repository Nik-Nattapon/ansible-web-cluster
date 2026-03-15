# 🚀 Automated Web Cluster with Ansible & Docker

![Ansible](https://img.shields.io/badge/Ansible-EE0000?style=for-the-badge&logo=ansible&logoColor=white)
![Docker](https://img.shields.io/badge/Docker-2496ED?style=for-the-badge&logo=docker&logoColor=white)
![Nginx](https://img.shields.io/badge/Nginx-009639?style=for-the-badge&logo=nginx&logoColor=white)

---

## 📋 Project Overview

This project demonstrates **Infrastructure as Code (IaC)** by automating the provisioning and configuration of a load-balanced web server cluster.

- Uses **Docker** to simulate the infrastructure nodes
- Uses **Ansible** to configure Nginx web servers and a Load Balancer
- Ensures **high availability** and seamless request routing

---

## 🏗️ System Architecture

```
                ┌──────────┐         ┌─────────────────────┐
                │  Client  │         │  Ansible Control Node│
                └────┬─────┘         └──────────┬──────────┘
                     │                           │
              HTTP Port 9090           SSH Port 2233
                     │                           │
                     ▼                           ▼
              ┌──────────────────────────────────────┐
              │         Load Balancer - lb01          │
              └────────────────┬─────────────────────┘
                               │
              SSH Port 2221    │    SSH Port 2222
           ┌──────────────────┤├──────────────────┐
           │   Round Robin    ││   Round Robin     │
           ▼                  ▼▼                   ▼
  ┌─────────────────┐              ┌─────────────────┐
  │  Web Server     │              │  Web Server     │
  │    web01        │              │    web02        │
  └─────────────────┘              └─────────────────┘
```

---

## 📁 Directory Structure

```
ansible-web-cluster/
├── docker-compose.yml          # Infrastructure setup (web01, web02, lb01)
├── inventory/
│   └── hosts.ini               # Node definitions and SSH ports
├── playbooks/
│   ├── site.yml                # Master Playbook
│   ├── deploy-web.yml          # Web server config & Nginx setup
│   └── setup-lb.yml            # Load balancer config
├── templates/
│   └── index.html.j2           # Dynamic Jinja2 web template
└── ansible.cfg                 # Ansible configurations
```

---

## 🚀 Getting Started

### Prerequisites

- Docker & Docker Compose (with WSL2 integration enabled)
- Ansible installed on the control node (WSL/Ubuntu)

### Steps

**1. Provision Infrastructure**

Spin up the target nodes (containers) in the background:

```bash
docker-compose up -d --build
```

**2. Deploy Configuration**

Run the master playbook to configure all servers automatically:

```bash
ansible-playbook -i inventory/hosts.ini playbooks/site.yml
```

**3. Test the Cluster**

Access the Load Balancer from your browser or terminal:

```bash
curl http://localhost:9090
```

> 💡 Refresh the page multiple times to see the Load Balancer distribute traffic between **web01** and **web02** dynamically.

---

## 👤 Author

**Natthapon** | System Integration Engineer
