# 🚀 Automated Web Cluster with Ansible & Docker

![Ansible](https://img.shields.io/badge/Ansible-E03231?style=for-the-badge&logo=ansible&logoColor=white)
![Docker](https://img.shields.io/badge/Docker-2496ED?style=for-the-badge&logo=docker&logoColor=white)
![Nginx](https://img.shields.io/badge/Nginx-009639?style=for-the-badge&logo=nginx&logoColor=white)

## 📋 Project Overview
This project demonstrates **Infrastructure as Code (IaC)** by automating the provisioning and configuration of a load-balanced web server cluster. It uses **Docker** to simulate the infrastructure nodes and **Ansible** to configure Nginx web servers and a Load Balancer, ensuring high availability and seamless request routing.

## 🏗️ System Architecture

```mermaid
graph TD
    Client([🌐 Client]) -->|HTTP Port 9090| LB[⚖️ Load Balancer - lb01]
    LB -->|Round Robin| W1[📄 Web Server - web01]
    LB -->|Round Robin| W2[📄 Web Server - web02]
    
    A{{🤖 Ansible Control Node}} -.->|SSH Port 2233| LB
    A -.->|SSH Port 2221| W1
    A -.->|SSH Port 2222| W2
```
📂 Directory Structure
ansible-web-cluster/
├── docker-compose.yml     # Infrastructure setup (web01, web02, lb01)
├── inventory/
│   └── hosts.ini          # Node definitions and SSH ports
├── playbooks/
│   ├── site.yml           # Master Playbook
│   ├── deploy-web.yml     # Web server config & Nginx setup
│   └── setup-lb.yml       # Load balancer config
├── templates/
│   └── index.html.j2      # Dynamic Jinja2 web template
└── ansible.cfg            # Ansible configurations

🚀 Getting Started
1. Prerequisites
Docker & Docker Compose (with WSL2 integration enabled)

Ansible installed on the control node (WSL/Ubuntu)

2. Provision Infrastructure
Spin up the target nodes (containers) in the background:
docker-compose up -d --build

3. Deploy Configuration
Run the master playbook to configure all servers automatically:
ansible-playbook -i inventory/hosts.ini playbooks/site.yml

🧪 Testing the Cluster
Access the Load Balancer from your browser or terminal:
curl http://localhost:9090

Refresh the page multiple times to see the Load Balancer distribute traffic between web01 and web02 dynamically.

Author: Natthapon | System Integration Engineer