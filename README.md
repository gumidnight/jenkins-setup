# Jenkins AWS Setup - Initial Documentation

## Purpose
This document describes the basic installation and setup of Jenkins on an AWS EC2 instance.

---

## Prerequisites

- AWS account with permission to create EC2 instances
- SSH key pair for accessing the EC2 instance
- Basic knowledge of Linux and AWS CLI

---

## Setup Steps

### 1. Launch an EC2 Instance

- Choose Ubuntu Server (e.g., Ubuntu 22.04 LTS)
- Configure Security Group to allow inbound traffic on port **8080** (Jenkins default port)
- Attach your SSH key pair for access

### 2. Connect to the EC2 Instance

```bash
ssh -i yourkey.pem ubuntu@<ec2-public-ip>
```
3. Install Java
Jenkins requires Java to run:

sudo apt update
sudo apt install openjdk-11-jdk -y
java -version
4. Install Jenkins
wget -q -O - https://pkg.jenkins.io/debian/jenkins.io.key | sudo apt-key add -
sudo sh -c 'echo deb https://pkg.jenkins.io/debian binary/ > /etc/apt/sources.list.d/jenkins.list'
sudo apt update
sudo apt install jenkins -y
5. Start and Enable Jenkins Service

sudo systemctl start jenkins
sudo systemctl enable jenkins

6. Adjust Firewall (if using UFW)

sudo ufw allow 8080
sudo ufw status
7. Access Jenkins Web Interface
Open your browser and go to:
http://<ec2-public-ip>:8080

To get the initial admin password, run on the server:

sudo cat /var/lib/jenkins/secrets/initialAdminPassword
Paste the password in the Jenkins setup wizard to proceed with installation.
