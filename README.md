# Ansible Installation & Usage Guide

## Introduction
Ansible is an open-source automation tool that can help you with configuration management, application deployment, task automation, and even IT orchestration.

## Installation

### Prerequisites
- A Linux-based system (e.g., Ubuntu, CentOS)
- Python installed (Ansible is written in Python)

### Installation Steps

#### Ubuntu
```bash
sudo apt update
sudo apt install software-properties-common
sudo apt-add-repository --yes --update ppa:ansible/ansible
sudo apt install ansible
```

#### CentOS
```bash
sudo yum install epel-release
sudo yum install ansible
```

# Basic Usage

1. Inventory File: Before you can use Ansible, you need to have an inventory file. This file lists all the hosts you want to manage with Ansible. Create a file named hosts.ini and add your servers:

```ini
[server]
192.168.1.10
192.168.1.11

[db]
192.168.1.20
```

2. Ping All Hosts: To check if Ansible can communicate with all the servers listed in the inventory file, use the ansible command:
```bash
ansible -i hosts.ini all -m ping
```

3. Ad-hoc Commands: You can run commands on your servers without writing a playbook. For example, to check the disk space on all web servers:
```bash
ansible -i hosts.ini web -m shell -a 'df -h'
```

4. Playbooks: Playbooks are the heart of Ansible. They are written in YAML and describe the tasks you want Ansible to execute. Here's a simple playbook to ensure the latest version of Apache is installed:
```yaml
---
- hosts: web
  tasks:
    - name: Ensure Apache is installed
      apt:
        name: apache2
        state: latest
```

To run the playbook:
```bash
ansible-playbook -i hosts.ini playbook.yaml
```