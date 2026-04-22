# Infrastructure Automation — Ansible

![Ansible](https://img.shields.io/badge/Automation-Ansible-EE0000?style=flat&logo=ansible)
![Linux](https://img.shields.io/badge/OS-Linux-FCC624?style=flat&logo=linux)
![AWS](https://img.shields.io/badge/Cloud-AWS_EC2-FF9900?style=flat&logo=amazonaws)

## What This Project Does

Automates server configuration and application setup across multiple Linux environments using Ansible playbooks — eliminating manual setup, reducing configuration drift, and cutting provisioning time by ~60%.

## What Gets Automated

| Playbook | What It Does |
|---|---|
| install_docker.yml | Installs Docker + Docker Compose on EC2 |
| install_jenkins.yml | Installs Java 11 + Jenkins, prints initial password |
| configure_nginx.yml | Installs NGINX as reverse proxy for the app |
| system_hardening.yml | SSH hardening, fail2ban, firewall, package updates |

## Project Structure

```
5_ansible-automation/
├── ansible.cfg                        # Default config (inventory, SSH key, user)
├── inventory/
│   ├── dev                            # Dev server IPs
│   ├── staging                        # Staging server IPs
│   └── prod                           # Prod server IPs
├── playbooks/
│   ├── install_docker.yml             # Docker + Docker Compose setup
│   ├── install_jenkins.yml            # Jenkins server setup
│   ├── configure_nginx.yml            # NGINX reverse proxy config
│   └── system_hardening.yml           # Security hardening
└── roles/
    ├── common/tasks/                  # Shared tasks across playbooks
    ├── docker/tasks/                  # Docker-specific role
    └── jenkins/tasks/                 # Jenkins-specific role
```

## Key Results

- **~60% reduction** in manual server setup time
- **Zero configuration drift** — idempotent playbooks safe to run multiple times
- **Consistent environments** — same playbooks run across dev, staging, prod
- **Security hardened** — SSH key-only, root login disabled, fail2ban enabled

## How to Run

### Prerequisites
- Ansible installed: `pip install ansible`
- AWS EC2 instances running (Amazon Linux 2)
- SSH key configured (`~/.ssh/id_rsa`)

### Install Ansible

```bash
pip install ansible
ansible --version
```

### Update Inventory

Edit `inventory/dev` and replace `YOUR_EC2_IP` with your actual EC2 IP:

```ini
[webservers]
web1 ansible_host=13.233.xx.xx ansible_user=ec2-user
```

### Test Connectivity

```bash
ansible all -i inventory/dev -m ping
```

### Run Playbooks

```bash
# Install Docker on all web servers
ansible-playbook -i inventory/dev playbooks/install_docker.yml

# Install Jenkins
ansible-playbook -i inventory/dev playbooks/install_jenkins.yml

# Configure NGINX reverse proxy
ansible-playbook -i inventory/dev playbooks/configure_nginx.yml

# Harden all servers
ansible-playbook -i inventory/dev playbooks/system_hardening.yml
```

### Dry Run (check mode — no changes made)

```bash
ansible-playbook -i inventory/dev playbooks/install_docker.yml --check
```

### Run with Verbose Output

```bash
ansible-playbook -i inventory/dev playbooks/install_docker.yml -v
```

### Run on Specific Host

```bash
ansible-playbook -i inventory/dev playbooks/install_docker.yml --limit web1
```

## Connect

**Trinadh Basva** — DevOps Engineer (Fresher)
- GitHub: [github.com/Trinadh345](https://github.com/Trinadh345)
- LinkedIn: [linkedin.com/in/trinadh-basva-9015203b4](https://linkedin.com/in/trinadh-basva-9015203b4)
- Email: trinadhabasva48@gmail.com
