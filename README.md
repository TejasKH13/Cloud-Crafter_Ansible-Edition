# 🚀 Cloud-Crafter_Ansible-Edition

## 📌 Project Overview

This project demonstrates how to automate the configuration and management of AWS EC2 instances using **Ansible** from a local **Mac (Control Node)**.

The goal of this project is to:

* Establish secure SSH communication between a control node and managed nodes
* Automate server setup using Ansible playbooks and roles
* Deploy and configure a web server (NGINX)
* Showcase Infrastructure Automation skills relevant to **DevOps/SRE roles**

---

## 🎯 Project Goals

* Automate EC2 configuration using Ansible
* Implement inventory management and SSH-based communication
* Use Ansible modules, tasks, and roles effectively
* Deploy a working web server and verify output
* Build a portfolio-ready DevOps automation project

---

## 🏗️ Architecture

```
           ┌────────────────────────────┐
           │       Mac (Control Node)   │
           │  - Ansible Installed       │
           │  - SSH Key Configured      │
           └────────────┬───────────────┘
                        │ SSH
                        ▼
        ┌────────────────────────────────────┐
        │        AWS EC2 Instances (2)       │
        │                                    │
        │  - Managed Nodes                   │
        │  - NGINX Installed via Ansible     │
        │  - Configured using Playbooks      │
        └────────────────────────────────────┘
```

---

## 🛠️ Tech Stack

* **Ansible** – Configuration Management & Automation
* **AWS EC2** – Cloud Infrastructure
* **SSH** – Secure Communication
* **YAML** – Playbook Configuration
* **Linux (Amazon Linux/Ubuntu)** – Target OS
* **Git & GitHub** – Version Control

---

## 📋 Prerequisites

Before running this project, ensure you have:

* Mac/Linux system (Control Node)
* Python installed
* Ansible installed
* AWS account
* AWS CLI configured
* SSH key pair created

---

## ⚙️ Setup Instructions

### 1️⃣ Prepare Control Node (Mac)

```bash
# Install Ansible
brew install ansible

# Generate SSH key
ssh-keygen -t ed25519 -f ~/.ssh/ec2_teja -C "ansible_key" -N ""

# Set permissions
chmod 600 ~/.ssh/ec2_teja.pem
```

---

### 2️⃣ Create EC2 Instances

* Launch 2 EC2 instances in AWS
* Use Amazon Linux 2 or Ubuntu
* Attach your SSH key
* Allow port **22 (SSH)** in Security Group

---

### 3️⃣ Verify SSH Connectivity

```bash
ssh -i ~/.ssh/ec2_teja.pem ec2-user@<PUBLIC_IP>
```

---

### 4️⃣ Create Ansible Project Structure

```
ansible-project/
├── ansible.cfg
├── hosts.ini
├── playbook.yml
└── roles/
    └── webserver/
        ├── tasks/main.yml
        ├── handlers/main.yml
        └── templates/index.html.j2
```

---

## 📂 Configuration Files

### 🔹 ansible.cfg

```ini
[defaults]
inventory = ./hosts.ini
host_key_checking = False
retry_files_enabled = False
deprecation_warnings = False
```

---

### 🔹 hosts.ini

```ini
[ec2]
<EC2_PUBLIC_IP> ansible_user=ec2-user ansible_ssh_private_key_file=~/.ssh/ec2_teja.pem
```

---

## ▶️ Running the Playbook

```bash
cd ansible-project
ansible all -m ping
ansible-playbook playbook.yml
```

---

## ⚡ What the Playbook Does

* Creates a demo directory on EC2
* Installs **NGINX**
* Starts and enables the service
* Deploys a custom HTML page using templates

---

## 🌐 Verification

### ✅ SSH Verification

```bash
ssh -i ~/.ssh/ec2_teja.pem ec2-user@<PUBLIC_IP>
nginx -v
```

### ✅ Service Check

```bash
sudo systemctl status nginx
```

### ✅ Browser Check

```
http://<PUBLIC_IP>
```

---

## 📜 Key Ansible Concepts Used

| Concept   | Description                                      |
| --------- | ------------------------------------------------ |
| Inventory | Defines target EC2 instances                     |
| Playbook  | YAML file defining automation steps              |
| Roles     | Organized structure for tasks                    |
| Modules   | Built-in tools like `file`, `package`, `service` |
| Templates | Dynamic HTML deployment                          |
| Handlers  | Triggered actions (e.g., restart nginx)          |

---

## 🧪 Troubleshooting

### ❌ Permission denied (SSH)

* Check key permissions:

```bash
chmod 600 ~/.ssh/ec2_teja.pem
```

* Verify correct username (`ec2-user` or `ubuntu`)

---

### ❌ Host unreachable

* Check Security Group (port 22 open)
* Verify public IP address

---

### ❌ No hosts matched

* Ensure `hosts.ini` matches `hosts:` in playbook
* Check `ansible.cfg` inventory path

---

## 🔮 Future Enhancements

* Automate EC2 provisioning using Python (boto3)
* Use dynamic inventory instead of static `hosts.ini`
* Integrate with CI/CD (GitHub Actions)
* Add monitoring setup (Prometheus + Grafana)
* Use Ansible Vault for secrets management
* Convert infrastructure setup to Terraform

---

## 📌 Conclusion

This project demonstrates a complete **end-to-end automation workflow** using Ansible and AWS.
It highlights real-world DevOps practices such as configuration management, infrastructure automation, and remote server provisioning.

---

## 👨‍💻 Author

**Tejas K H**

---

## ⭐ If you found this useful

Feel free to ⭐ the repo and share!
