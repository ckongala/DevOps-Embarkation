<div align="center">

# 🎯 DevOps Prerequisites

### *Foundation Skills You Need Before Starting Your DevOps Journey*

[![Linux](https://img.shields.io/badge/Linux-FCC624?style=for-the-badge&logo=linux&logoColor=black)](https://linux.org)
[![Git](https://img.shields.io/badge/Git-F05032?style=for-the-badge&logo=git&logoColor=white)](https://git-scm.com)
[![Bash](https://img.shields.io/badge/Bash-4EAA25?style=for-the-badge&logo=gnu-bash&logoColor=white)](https://www.gnu.org/software/bash/)
[![Python](https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white)](https://python.org)
[![Networking](https://img.shields.io/badge/Networking-0078D4?style=for-the-badge&logo=cisco&logoColor=white)](https://www.cisco.com)

---

*Master these fundamentals to build a strong foundation for your DevOps career*

</div>

---

## 📑 Table of Contents

- [Overview](#-overview)
- [Linux Fundamentals](#-linux-fundamentals)
- [Networking Basics](#-networking-basics)
- [Version Control (Git)](#-version-control-git)
- [Scripting](#-scripting)
- [YAML & JSON](#-yaml--json)
- [Virtualization & Containers](#-virtualization--containers)
- [Cloud Basics](#-cloud-basics)
- [Security Fundamentals](#-security-fundamentals)
- [Learning Roadmap](#-learning-roadmap)

---

## 🎯 Overview

Before diving into DevOps tools like Kubernetes, Terraform, or CI/CD pipelines, you need a solid foundation in several key areas. This guide outlines the essential prerequisites that will make your DevOps journey smoother and more effective.

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                        DEVOPS PREREQUISITES PYRAMID                         │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│                            ┌─────────────┐                                  │
│                            │   DevOps    │                                  │
│                            │   Tools     │                                  │
│                            └──────┬──────┘                                  │
│                       ┌───────────┴───────────┐                             │
│                       │   Cloud & Containers  │                             │
│                       └───────────┬───────────┘                             │
│                  ┌────────────────┴────────────────┐                        │
│                  │   Scripting & Automation        │                        │
│                  └────────────────┬────────────────┘                        │
│             ┌─────────────────────┴─────────────────────┐                   │
│             │   Version Control (Git) & Collaboration   │                   │
│             └─────────────────────┬─────────────────────┘                   │
│        ┌──────────────────────────┴──────────────────────────┐              │
│        │            Networking & Security Basics              │              │
│        └──────────────────────────┬──────────────────────────┘              │
│   ┌───────────────────────────────┴───────────────────────────────┐         │
│   │                    LINUX FUNDAMENTALS                          │         │
│   └────────────────────────────────────────────────────────────────┘        │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘
```

---

## 🐧 Linux Fundamentals

> *Linux is the backbone of DevOps. Most servers, containers, and cloud instances run on Linux.*

### Why Linux?

- 🖥️ **90%+ of servers** run on Linux
- 🐳 **Docker containers** are Linux-based
- ☸️ **Kubernetes nodes** typically run Linux
- ☁️ **Cloud instances** predominantly use Linux

### Essential Skills

<table>
<tr>
<td width="50%">

**📁 File System & Navigation**

```bash
# Navigation
pwd                    # Print working directory
ls -la                 # List all files with details
cd /path/to/dir        # Change directory
tree                   # Directory tree structure

# File Operations
cp source dest         # Copy files
mv old new             # Move/rename files
rm -rf directory       # Remove recursively
mkdir -p path/to/dir   # Create nested directories
touch filename         # Create empty file

# Viewing Files
cat file               # Display file content
less file              # Page through file
head -n 20 file        # First 20 lines
tail -f logfile        # Follow log in real-time
```

</td>
<td width="50%">

**🔐 Permissions & Ownership**

```bash
# Understanding Permissions
# rwx rwx rwx
# │   │   └── Others
# │   └────── Group
# └────────── Owner

# Changing Permissions
chmod 755 file         # rwxr-xr-x
chmod +x script.sh     # Add execute permission
chmod -R 644 dir/      # Recursive permission

# Changing Ownership
chown user:group file  # Change owner and group
chown -R user dir/     # Recursive ownership

# Special Permissions
chmod u+s file         # SetUID
chmod g+s dir          # SetGID
chmod +t dir           # Sticky bit
```

</td>
</tr>
<tr>
<td>

**⚙️ Process Management**

```bash
# Viewing Processes
ps aux                 # All running processes
top                    # Real-time process monitor
htop                   # Interactive process viewer
pgrep processname      # Find process by name

# Managing Processes
kill PID               # Terminate process
kill -9 PID            # Force kill
killall processname    # Kill by name
nohup command &        # Run in background
jobs                   # List background jobs
fg %1                  # Bring job to foreground

# System Resources
free -h                # Memory usage
df -h                  # Disk usage
du -sh directory       # Directory size
```

</td>
<td>

**📦 Package Management**

```bash
# Debian/Ubuntu (APT)
apt update             # Update package list
apt upgrade            # Upgrade packages
apt install package    # Install package
apt remove package     # Remove package
apt search keyword     # Search packages

# RHEL/CentOS (YUM/DNF)
yum update             # Update packages
yum install package    # Install package
dnf install package    # DNF (newer)

# Check Package Info
dpkg -l                # List installed (Debian)
rpm -qa                # List installed (RHEL)
which command          # Find command location
```

</td>
</tr>
</table>

### Systemd & Services

```bash
# Service Management
sudo systemctl start service       # Start a service
sudo systemctl stop service        # Stop a service
sudo systemctl restart service     # Restart a service
sudo systemctl status service      # Check status
sudo systemctl enable service      # Enable at boot
sudo systemctl disable service     # Disable at boot

# Viewing Logs
journalctl -u service              # Logs for specific service
journalctl -f                      # Follow logs real-time
journalctl --since "1 hour ago"    # Recent logs
```

### Text Processing

```bash
# Search & Filter
grep "pattern" file                # Search in file
grep -r "pattern" dir/             # Recursive search
grep -i "pattern" file             # Case insensitive
grep -v "pattern" file             # Invert match

# Text Manipulation
sed 's/old/new/g' file             # Replace text
awk '{print $1}' file              # Print first column
cut -d',' -f1 file                 # Cut by delimiter
sort file                          # Sort lines
uniq                               # Remove duplicates
wc -l file                         # Count lines

# Pipes & Redirection
command > file                     # Redirect output (overwrite)
command >> file                    # Redirect output (append)
command 2>&1                       # Redirect stderr to stdout
command1 | command2                # Pipe output
```

---

## 🌐 Networking Basics

> *Understanding networking is crucial for configuring services, debugging issues, and managing infrastructure.*

### Key Concepts

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                              OSI MODEL                                      │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│   Layer 7 │ Application  │ HTTP, HTTPS, FTP, SSH, DNS                      │
│   Layer 6 │ Presentation │ SSL/TLS, Encryption                              │
│   Layer 5 │ Session      │ Sessions, Authentication                         │
│   Layer 4 │ Transport    │ TCP, UDP, Ports                                  │
│   Layer 3 │ Network      │ IP, Routing, ICMP                                │
│   Layer 2 │ Data Link    │ MAC Addresses, Switches                          │
│   Layer 1 │ Physical     │ Cables, Signals                                  │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘
```

### Essential Networking Commands

<table>
<tr>
<td width="50%">

**🔍 Network Information**

```bash
# IP Configuration
ip addr                    # Show IP addresses
ip route                   # Show routing table
ifconfig                   # Legacy IP info
hostname -I                # Show host IPs

# DNS
nslookup domain.com        # DNS lookup
dig domain.com             # Detailed DNS query
host domain.com            # Simple DNS lookup
cat /etc/resolv.conf       # DNS configuration

# Active Connections
netstat -tuln              # Listening ports
ss -tuln                   # Modern alternative
lsof -i :80                # Process using port 80
```

</td>
<td width="50%">

**🔗 Connectivity Testing**

```bash
# Ping & Traceroute
ping google.com            # Test connectivity
ping -c 4 google.com       # 4 packets only
traceroute google.com      # Trace packet route
mtr google.com             # Continuous traceroute

# Port Testing
telnet host 80             # Test port connectivity
nc -zv host 80             # Netcat port test
curl -v http://host        # HTTP request verbose

# Data Transfer
curl URL                   # Fetch URL content
wget URL                   # Download file
scp file user@host:/path   # Secure copy
rsync -avz src dest        # Sync directories
```

</td>
</tr>
</table>

### Important Ports to Know

| Port | Protocol | Service |
|:----:|:---------|:--------|
| 22 | TCP | SSH |
| 80 | TCP | HTTP |
| 443 | TCP | HTTPS |
| 53 | TCP/UDP | DNS |
| 25 | TCP | SMTP |
| 3306 | TCP | MySQL |
| 5432 | TCP | PostgreSQL |
| 6379 | TCP | Redis |
| 27017 | TCP | MongoDB |
| 8080 | TCP | HTTP (alternate) |
| 9090 | TCP | Prometheus |
| 3000 | TCP | Grafana |

### Firewall Basics

```bash
# UFW (Ubuntu)
sudo ufw status                    # Check status
sudo ufw enable                    # Enable firewall
sudo ufw allow 22                  # Allow SSH
sudo ufw allow 80/tcp              # Allow HTTP
sudo ufw deny 23                   # Deny telnet

# Firewalld (RHEL/CentOS)
sudo firewall-cmd --state          # Check status
sudo firewall-cmd --add-port=80/tcp --permanent
sudo firewall-cmd --reload

# iptables (Low-level)
sudo iptables -L                   # List rules
sudo iptables -A INPUT -p tcp --dport 80 -j ACCEPT
```

---

## 📚 Version Control (Git)

> *Git is essential for code management, collaboration, and GitOps workflows.*

### Git Workflow

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                              GIT WORKFLOW                                   │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│   Working       Staging        Local           Remote                       │
│   Directory     Area           Repository      Repository                   │
│      │            │               │               │                         │
│      │   add      │    commit     │     push      │                         │
│      │──────────▶ │ ────────────▶ │ ────────────▶ │                         │
│      │            │               │               │                         │
│      │◀────────── │ ◀──────────── │ ◀──────────── │                         │
│      │  checkout  │    reset      │     pull      │                         │
│      │            │               │               │                         │
└─────────────────────────────────────────────────────────────────────────────┘
```

### Essential Git Commands

<table>
<tr>
<td width="50%">

**🔧 Setup & Configuration**

```bash
# Configuration
git config --global user.name "Your Name"
git config --global user.email "email@example.com"
git config --list              # View all settings

# Repository Setup
git init                       # Initialize new repo
git clone URL                  # Clone repository
git remote add origin URL      # Add remote
git remote -v                  # View remotes
```

</td>
<td width="50%">

**📝 Basic Operations**

```bash
# Status & Changes
git status                     # Check status
git diff                       # View changes
git diff --staged              # Staged changes

# Staging & Committing
git add file                   # Stage file
git add .                      # Stage all
git commit -m "message"        # Commit
git commit -am "message"       # Add + Commit

# Push & Pull
git push origin main           # Push to remote
git pull origin main           # Pull from remote
git fetch                      # Fetch without merge
```

</td>
</tr>
<tr>
<td>

**🌿 Branching**

```bash
# Branch Operations
git branch                     # List branches
git branch feature             # Create branch
git checkout feature           # Switch branch
git checkout -b feature        # Create + Switch
git switch feature             # Modern switch

# Merging
git merge feature              # Merge branch
git merge --no-ff feature      # Merge with commit
git rebase main                # Rebase onto main

# Cleanup
git branch -d feature          # Delete merged
git branch -D feature          # Force delete
```

</td>
<td>

**🔄 Advanced Operations**

```bash
# Stashing
git stash                      # Stash changes
git stash list                 # List stashes
git stash pop                  # Apply + remove
git stash apply                # Apply keep

# History
git log --oneline              # Compact history
git log --graph                # Visual history
git blame file                 # Who changed what

# Undoing
git reset HEAD~1               # Undo last commit
git reset --hard HEAD~1        # Undo + discard
git revert commit              # Revert commit
git checkout -- file           # Discard changes
```

</td>
</tr>
</table>

### Branching Strategies

```
main ─────●─────────●─────────────●─────────────●─────▶
           \       /               \           /
develop ────●─────●─────●───────────●─────●───●───────▶
             \   /       \         /
feature ──────●─●         ●───────●
```

| Strategy | Description | Use Case |
|:---------|:------------|:---------|
| **Git Flow** | Feature, develop, release, hotfix branches | Scheduled releases |
| **GitHub Flow** | Simple: main + feature branches | Continuous deployment |
| **Trunk-Based** | Short-lived branches, frequent merges | CI/CD focused teams |

---

## 📜 Scripting

> *Automation is at the heart of DevOps. Scripting skills enable you to automate repetitive tasks.*

### Bash Scripting

```bash
#!/bin/bash
# Basic script structure

# Variables
NAME="DevOps"
COUNT=5

# User Input
read -p "Enter your name: " USER_NAME
echo "Hello, $USER_NAME!"

# Conditionals
if [ "$COUNT" -gt 3 ]; then
    echo "Count is greater than 3"
elif [ "$COUNT" -eq 3 ]; then
    echo "Count is 3"
else
    echo "Count is less than 3"
fi

# Loops
for i in {1..5}; do
    echo "Iteration $i"
done

# While Loop
while [ $COUNT -gt 0 ]; do
    echo "Countdown: $COUNT"
    ((COUNT--))
done

# Functions
greet() {
    local name=$1
    echo "Hello, $name!"
}
greet "World"

# Command Substitution
CURRENT_DATE=$(date +%Y-%m-%d)
echo "Today is $CURRENT_DATE"
```

### Python Basics for DevOps

```python
#!/usr/bin/env python3
"""Basic Python for DevOps tasks"""

import os
import subprocess
import json
import requests

# File Operations
with open('config.txt', 'r') as f:
    content = f.read()

# Environment Variables
api_key = os.environ.get('API_KEY', 'default')

# Running Shell Commands
result = subprocess.run(['ls', '-la'], capture_output=True, text=True)
print(result.stdout)

# Working with JSON
data = {'name': 'server1', 'port': 8080}
json_str = json.dumps(data, indent=2)
parsed = json.loads(json_str)

# API Requests
response = requests.get('https://api.example.com/status')
if response.status_code == 200:
    data = response.json()

# List Comprehension
servers = ['web1', 'web2', 'db1']
web_servers = [s for s in servers if s.startswith('web')]

# Dictionary Operations
config = {
    'host': 'localhost',
    'port': 5432,
    'database': 'mydb'
}
for key, value in config.items():
    print(f"{key}: {value}")
```

### Comparison Operators (Bash)

| Operator | Description | Example |
|:---------|:------------|:--------|
| `-eq` | Equal | `[ $a -eq $b ]` |
| `-ne` | Not equal | `[ $a -ne $b ]` |
| `-gt` | Greater than | `[ $a -gt $b ]` |
| `-lt` | Less than | `[ $a -lt $b ]` |
| `-ge` | Greater or equal | `[ $a -ge $b ]` |
| `-le` | Less or equal | `[ $a -le $b ]` |
| `-z` | String is empty | `[ -z "$str" ]` |
| `-n` | String is not empty | `[ -n "$str" ]` |
| `-f` | File exists | `[ -f file ]` |
| `-d` | Directory exists | `[ -d dir ]` |

---

## 📄 YAML & JSON

> *Configuration languages used extensively in DevOps for defining infrastructure, pipelines, and application configs.*

### YAML Syntax

```yaml
# YAML Basics
---
# Strings
name: DevOps Engineer
description: "String with special: characters"
multiline: |
  This is a multiline
  string that preserves
  line breaks

# Numbers & Booleans
port: 8080
replicas: 3
enabled: true
ratio: 3.14

# Lists
fruits:
  - apple
  - banana
  - orange

# Inline list
colors: [red, green, blue]

# Dictionaries/Maps
database:
  host: localhost
  port: 5432
  name: mydb
  credentials:
    username: admin
    password: secret

# Inline dictionary
server: {host: localhost, port: 8080}

# Anchors & Aliases (Reusability)
defaults: &defaults
  timeout: 30
  retries: 3

production:
  <<: *defaults      # Merge defaults
  host: prod.example.com

development:
  <<: *defaults
  host: dev.example.com
```

### JSON Syntax

```json
{
  "name": "DevOps Engineer",
  "age": 30,
  "active": true,
  "skills": [
    "Linux",
    "Docker",
    "Kubernetes"
  ],
  "experience": {
    "years": 5,
    "companies": ["Company A", "Company B"],
    "current": {
      "role": "Senior DevOps",
      "team_size": 8
    }
  },
  "certifications": null
}
```

### YAML vs JSON Comparison

| Feature | YAML | JSON |
|:--------|:-----|:-----|
| **Readability** | More human-readable | More compact |
| **Comments** | ✅ Supported (`#`) | ❌ Not supported |
| **Data Types** | Inferred | Explicit |
| **Use Cases** | Config files, K8s manifests | APIs, data exchange |
| **Indentation** | Significant (2 spaces) | Brackets define structure |

---

## 🖥️ Virtualization & Containers

> *Understanding virtualization and containers is essential before diving into Docker and Kubernetes.*

### Virtualization vs Containers

```
┌─────────────────────────────────────────────────────────────────────────────┐
│           VIRTUAL MACHINES                    CONTAINERS                    │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│   ┌─────────┐ ┌─────────┐ ┌─────────┐    ┌─────────┐ ┌─────────┐ ┌─────┐  │
│   │  App A  │ │  App B  │ │  App C  │    │  App A  │ │  App B  │ │App C│  │
│   ├─────────┤ ├─────────┤ ├─────────┤    ├─────────┤ ├─────────┤ ├─────┤  │
│   │  Libs   │ │  Libs   │ │  Libs   │    │  Libs   │ │  Libs   │ │Libs │  │
│   ├─────────┤ ├─────────┤ ├─────────┤    └────┬────┘ └────┬────┘ └──┬──┘  │
│   │Guest OS │ │Guest OS │ │Guest OS │         │           │         │     │
│   └────┬────┘ └────┬────┘ └────┬────┘    ┌────┴───────────┴─────────┴──┐  │
│        │           │           │         │       Container Runtime      │  │
│   ┌────┴───────────┴───────────┴────┐    │         (Docker)             │  │
│   │          Hypervisor             │    └──────────────┬───────────────┘  │
│   │     (VMware, VirtualBox)        │                   │                  │
│   └──────────────┬──────────────────┘    ┌──────────────┴───────────────┐  │
│                  │                       │           Host OS             │  │
│   ┌──────────────┴──────────────────┐    └──────────────┬───────────────┘  │
│   │           Host OS               │                   │                  │
│   └──────────────┬──────────────────┘    ┌──────────────┴───────────────┐  │
│                  │                       │         Hardware              │  │
│   ┌──────────────┴──────────────────┐    └──────────────────────────────┘  │
│   │          Hardware               │                                      │
│   └─────────────────────────────────┘                                      │
│                                                                             │
│   Heavy | Slower startup | Full isolation    Light | Fast | Process-level │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘
```

### Basic Docker Commands

```bash
# Images
docker images                      # List images
docker pull nginx                  # Pull image
docker build -t myapp .            # Build image
docker rmi image                   # Remove image

# Containers
docker ps                          # Running containers
docker ps -a                       # All containers
docker run -d -p 80:80 nginx       # Run container
docker stop container              # Stop container
docker rm container                # Remove container

# Inspection
docker logs container              # View logs
docker exec -it container bash     # Shell into container
docker inspect container           # Container details
```

---

## ☁️ Cloud Basics

> *Familiarity with cloud concepts prepares you for working with AWS, Azure, GCP, and other providers.*

### Cloud Service Models

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                         CLOUD SERVICE MODELS                                │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│   On-Premises     IaaS            PaaS            SaaS                     │
│   ────────────    ────            ────            ────                     │
│   ┌──────────┐    ┌──────────┐    ┌──────────┐    ┌──────────┐            │
│   │   Apps   │    │   Apps   │    │   Apps   │    │██████████│            │
│   ├──────────┤    ├──────────┤    ├──────────┤    ├──────────┤            │
│   │   Data   │    │   Data   │    │   Data   │    │██████████│            │
│   ├──────────┤    ├──────────┤    ├──────────┤    ├──────████│            │
│   │ Runtime  │    │ Runtime  │    │██████████│    │██████████│            │
│   ├──────────┤    ├──────────┤    ├──████████┤    ├──████████┤            │
│   │   O/S    │    │   O/S    │    │██████████│    │██████████│            │
│   ├──────────┤    ├──────████┤    ├──████████┤    ├──████████┤            │
│   │  Server  │    │██████████│    │██████████│    │██████████│            │
│   ├──────────┤    ├──████████┤    ├──████████┤    ├──████████┤            │
│   │ Storage  │    │██████████│    │██████████│    │██████████│            │
│   ├──────────┤    ├──████████┤    ├──████████┤    ├──████████┤            │
│   │ Network  │    │██████████│    │██████████│    │██████████│            │
│   └──────────┘    └──████████┘    └──████████┘    └──████████┘            │
│                                                                             │
│   You Manage      ██ Provider     Examples:                                │
│   Everything         Manages      IaaS: EC2, Azure VMs, GCE                │
│                                   PaaS: Heroku, App Engine, Azure App Svc  │
│                                   SaaS: Gmail, Salesforce, Office 365      │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘
```

### Key Cloud Concepts

| Concept | Description |
|:--------|:------------|
| **Regions** | Geographic locations for data centers |
| **Availability Zones** | Isolated data centers within a region |
| **VPC** | Virtual Private Cloud - isolated network |
| **Subnets** | Subdivisions within a VPC |
| **Security Groups** | Virtual firewalls for instances |
| **IAM** | Identity and Access Management |
| **S3/Blob Storage** | Object storage services |
| **Load Balancer** | Distributes traffic across instances |
| **Auto Scaling** | Automatically adjust capacity |

---

## 🔐 Security Fundamentals

> *Security is everyone's responsibility in DevOps (DevSecOps).*

### Key Security Concepts

| Concept | Description |
|:--------|:------------|
| **Authentication** | Verify identity (who you are) |
| **Authorization** | Verify permissions (what you can do) |
| **Encryption** | Protect data in transit and at rest |
| **SSL/TLS** | Secure communication protocols |
| **SSH Keys** | Secure authentication for servers |
| **Secrets Management** | Secure storage for sensitive data |
| **Least Privilege** | Minimal permissions needed |
| **Defense in Depth** | Multiple layers of security |

### SSH Key Management

```bash
# Generate SSH Key Pair
ssh-keygen -t ed25519 -C "your_email@example.com"

# Or with RSA
ssh-keygen -t rsa -b 4096 -C "your_email@example.com"

# Copy public key to server
ssh-copy-id user@server

# SSH Config (~/.ssh/config)
Host myserver
    HostName 192.168.1.100
    User admin
    IdentityFile ~/.ssh/id_ed25519
    Port 22

# Connect using alias
ssh myserver
```

### Security Best Practices

- ✅ Never commit secrets to version control
- ✅ Use environment variables for sensitive data
- ✅ Rotate credentials regularly
- ✅ Enable MFA (Multi-Factor Authentication)
- ✅ Keep systems and packages updated
- ✅ Use strong, unique passwords
- ✅ Implement network segmentation
- ✅ Regular security audits and scans

---

## 🗺️ Learning Roadmap

### Beginner (1-2 months)

- [ ] Linux command line proficiency
- [ ] Basic networking concepts
- [ ] Git fundamentals
- [ ] Bash scripting basics
- [ ] YAML syntax

### Intermediate (2-3 months)

- [ ] Advanced Linux administration
- [ ] Python scripting
- [ ] Docker basics
- [ ] Cloud fundamentals (AWS/Azure/GCP)
- [ ] CI/CD concepts

### Advanced (Ready for DevOps tools)

- [ ] Container orchestration (Kubernetes)
- [ ] Infrastructure as Code (Terraform)
- [ ] Configuration management (Ansible)
- [ ] Monitoring & Logging
- [ ] Security practices

---

## 📚 Recommended Resources

### Books
- 📖 *The Linux Command Line* by William Shotts
- 📖 *Pro Git* by Scott Chacon (free online)
- 📖 *Python Crash Course* by Eric Matthes
- 📖 *The Phoenix Project* by Gene Kim

### Online Platforms
- 🌐 [Linux Journey](https://linuxjourney.com/) - Free Linux learning
- 🌐 [Learn Git Branching](https://learngitbranching.js.org/) - Interactive Git
- 🌐 [Codecademy](https://www.codecademy.com/) - Python, Bash courses
- 🌐 [KodeKloud](https://kodekloud.com/) - DevOps labs

### Practice
- 💻 Set up a home lab with VirtualBox/Vagrant
- 💻 Contribute to open source projects
- 💻 Build personal projects and automate tasks
- 💻 Get hands-on with cloud free tiers

---

<div align="center">

## 🚀 Ready to Continue?

Once you're comfortable with these prerequisites, move on to:

**[← Back to Main](../README.md)** | **[CI/CD →](../CI-CD/README.md)** | **[Kubernetes →](../Kubernetes-Concept/README.md)**

---

*"The expert in anything was once a beginner."* — Helen Hayes

</div>
