# EC2 Setup Guide

This guide walks through launching an EC2 instance, configuring it with Apache, and preparing it to serve as the frontend of the AWS 3-tier web application.

## ✅ Prerequisites

- Key pair (`webserver-key.pem`)
- IAM permissions to launch EC2
- Security Group that allows:
  - Inbound HTTP (port 80) from 0.0.0.0/0
  - Inbound SSH (port 22) from your IP

## 🚀 Launch EC2 Instance

1. Choose **Amazon Linux 2023**
2. t2.micro (free tier)
3. Add to a VPC with access to RDS
4. Attach key pair `webserver-key.pem`
5. Open required ports in Security Group

📸 `ec2-instance-summary.png`  
📸 `ec2-instance-dashboard.png`

## 🔐 Connect via SSH

```bash
chmod 400 ~/.ssh/webserver-key.pem
ssh -i ~/.ssh/webserver-key.pem ec2-user@<EC2_PUBLIC_IP>
```

📸 `ssh-key-permissions.png`  
📸 `mac-ssh-into-ec2.png`  
📸 `ssh-into-ec2.png`

## 🔍 Initial Commands

```bash
whoami
sudo yum update -y
```

📸 `whoami-and-update.png`

## 📦 Install Apache

```bash
sudo yum install -y httpd
sudo systemctl start httpd
sudo systemctl enable httpd
```

📸 `install-apache-start.png`  
📸 `install-apache-complete.png`  
📸 `apache-start-and-enable.png`

## 🌐 Serve HTML

```bash
echo '<h1>Hello from Chet\'s EC2 Web Server!</h1>' | sudo tee /var/www/html/index.html
```

📸 `echo-html-bugged.png`  
📸 `echo-html-fixed.png`  
📸 `apache-default-page.png`  
📸 `custom-ec2-webpage.png`
