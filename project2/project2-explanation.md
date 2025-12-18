# Ansible Project 2 – Passwordless SSH, Multiple Nodes & Playbooks

---

## 1. Project Objective

The objective of Project-2 was to move from basic Ansible ad-hoc usage to a
**real-world Ansible automation setup**.

This project focuses on:
- Bastion host based architecture
- Passwordless SSH authentication
- Managing multiple managed nodes
- Writing and executing Ansible playbooks
- Understanding idempotency
- Following industry-standard DevOps practices

---

## 2. Architecture Overview

### Bastion Host
- Ubuntu Server running in Oracle VirtualBox (on Windows 10)
- Acts as a jump host
- Contains AWS `devops.pem` key
- Used only for initial access

### Control Node
- AWS EC2 (Ubuntu)
- Ansible installed
- Generates its own RSA SSH key
- Executes all Ansible commands and playbooks

### Managed Nodes
- 3 AWS EC2 instances (Ubuntu)
- Accessed using private IPs from control node
- Passwordless SSH configured from control node

---

## 3. SSH Authentication Setup

### SSH Key Generation (on Control Node)

```bash
ssh-keygen -t rsa -b 4096
RSA chosen for wide industry support

No passphrase for automation

Passwordless SSH Configuration
Public key from control node was added to each managed node:

bash
Copy code
~/.ssh/authorized_keys
Permissions ensured:

bash
Copy code
chmod 700 ~/.ssh
chmod 600 ~/.ssh/authorized_keys
Verification:

bash
Copy code
ssh ubuntu@<managed-node-private-ip>
4. Inventory Configuration
inventory.ini
ini
Copy code
[webservers]
ubuntu@172.31.18.221
ubuntu@172.31.16.55
ubuntu@172.31.24.118

[all:vars]
ansible_python_interpreter=/usr/bin/python3
Private IPs used

Inventory grouped using webservers

5. Ad-hoc Command Verification
Connectivity check:

bash
Copy code
ansible -i inventory.ini all -m ping
Result:

All nodes returned pong

6. Playbooks Used
ping.yml
yaml
Copy code
- name: Verify connectivity to all managed nodes
  hosts: all
  tasks:
    - name: Ping nodes
      ping:
Execution:

bash
Copy code
ansible-playbook -i inventory.ini ping.yml
nginx.yml
yaml
Copy code
- name: Install and start nginx on webservers
  hosts: webservers
  become: yes

  tasks:
    - name: Update apt cache
      apt:
        update_cache: yes
        cache_valid_time: 3600

    - name: Install nginx
      apt:
        name: nginx
        state: present

    - name: Start and enable nginx
      service:
        name: nginx
        state: started
        enabled: yes
Execution:

bash
Copy code
ansible-playbook -i inventory.ini nginx.yml
7. Idempotency Validation
Playbook executed multiple times:

bash
Copy code
ansible-playbook -i inventory.ini nginx.yml
Result:

changed=0 on subsequent runs

Confirms idempotent behavior

8. Folder Structure
text
Copy code
ansible/
└── project2/
    ├── inventory.ini
    ├── ping.yml
    ├── nginx.yml
    └── project2-explanation.md
9. Security Practices Followed
.pem key never committed

SSH private keys excluded

Inventory uses private IPs

Bastion host used for access control

10. Project Outcome
By completing Project-2:

Passwordless automation achieved

Multiple nodes managed together

Playbooks understood clearly

Real-world Ansible workflow implemented

Foundation prepared for advanced Ansible concepts


