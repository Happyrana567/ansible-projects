✅ STEP 2 — YE POORA CONTENT PASTE KAR DO
# Ansible Project 1 – Adhoc Commands & Inventory (Beginner Level)

## 1. Project Objective

The goal of this project was to understand the **core fundamentals of Ansible**
from a DevOps engineer’s point of view.

This project focuses on:
- Understanding what a control node and managed node are
- Using inventory files
- Practicing most commonly used Ansible adhoc commands
- Learning real-world workflow step by step
- Avoiding shortcuts and understanding *why* each step is done

This project is intentionally kept **simple and beginner-friendly**.


---

## 2. Initial Setup

### Control Node
- AWS EC2 (Ubuntu)
- Ansible installed
- Acts as the machine from which all Ansible commands are executed

### Managed Node
- AWS EC2 (Ubuntu)
- Target server managed by Ansible

Both EC2 instances are created in the **same VPC**, so private IP communication is used.

---

## 3. Inventory Setup

An inventory file was created to tell Ansible which servers it needs to manage.

**File:** `inventory.ini`

```ini
[all]
ubuntu@<MANAGED_NODE_PRIVATE_IP>


This helped understand:

Inventory is the heart of Ansible

Ansible does nothing unless hosts are defined in inventory

User and IP both are required

4. Authentication Method (Project-1 Decision)

For Project-1, the AWS .pem key method was used intentionally.

Reason:

Keep things simple for the first project

Avoid ssh-keygen complexity initially

Focus on learning Ansible concepts first

Later projects will use ssh-keygen and proper passwordless authentication.

5. Major Challenges Faced & Learnings
Challenge 1: Understanding where commands are executed

Initially it was confusing:

From where Ansible runs

Which machine is control node

Which machine is managed node

Learning:
All Ansible commands always run from the control node.

Challenge 2: Inventory vs direct SSH

At first, direct SSH felt easier.

Learning:
Ansible does not work like normal SSH.
Inventory is mandatory for automation.

Challenge 3: Understanding -m and -a

Confusion existed about:

When to use -a

When not to use -a

Learning:

-m is the module

-a is used only when the module needs arguments

Some modules like ping do not require -a

Challenge 4: Understanding src and dest

It was unclear from where files are copied.

Learning:

src always refers to control node

dest always refers to managed node

This is a very important real-world concept.

Challenge 5: Git & GitHub integration

Confusion existed around:

SSH vs HTTPS

Tokens vs SSH keys

Old Kubuntu SSH keys vs new Ubuntu Server keys

Learning:

GitHub SSH keys are independent of AWS keys

Each OS/machine should have its own SSH key

SSH is preferred for long-term DevOps work

6. Adhoc Commands Practiced (Most Used)

The following most commonly used real-world adhoc commands were practiced:

Connectivity check (ping)

OS information

Kernel version

Hostname

Disk usage

Memory usage

Logged-in users

Package update

Package install/remove (nginx)

Service start/stop/restart

File creation

Directory creation

File copy from control node to managed node

These commands cover 90% of daily DevOps adhoc usage.

7. Folder Structure Used
ansible/
└── project1/
    ├── inventory.ini
    └── project1-explanation.md


This structure keeps learning projects clean and scalable.

8. Git & Security Practices

.gitignore is used at root level

AWS .pem files are never pushed

SSH keys and credentials are excluded

One GitHub repo is used for all Ansible projects

9. Project Outcome

By completing Project-1:

Core Ansible concepts became clear

Real DevOps workflow was understood

Foundation is ready for advanced Ansible topics

10. Next Step

Project-2 will focus on:

ssh-keygen

Proper passwordless authentication

Multiple managed nodes

Playbooks (YAML)

Real production-style Ansible usage
