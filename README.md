# 🖥️ AWS 3-Tier Web App Lab

This project demonstrates a classic 3-tier architecture on AWS using EC2, RDS, and Apache. The walkthrough includes full CLI configuration, MySQL database creation, and custom webpage deployment — all documented with real output and screenshots.

---

## 🧱 Architecture Overview

- **Frontend:** EC2 running Apache HTTPD
- **Backend:** MySQL 8 on Amazon RDS
- **Storage (optional):** S3 static hosting
- **Security:** SSH key access and Security Groups
- **Tools Used:** CLI, yum, MySQL client, nano, bash

---

## 📁 Folder Structure

```
aws-3tier-webapp-lab/
├── app/
│   └── index.html
├── assets/
│   └── users.sql
├── docs/
│   ├── ec2-setup-guide.md
│   ├── rds-connection-guide.md
│   ├── load-balancer-setup.md
│   └── s3-static-hosting.md
├── screenshots/
│   └── *.png (all referenced images)
└── README.md
```

---

## ✅ Setup & Screenshots

### 1️⃣ Project Initialization

Created folder structure and initialized GitHub repo.

📸 `project-init-folder-structure.png`  
📸 `github-repo-open.png`

---

### 2️⃣ Create RDS Instance and Configure

- RDS created via AWS Console  
- Security Group updated to allow EC2 access on port 3306

📸 `rds-create-webapp-db.png`  
📸 `rds-webapp-db-summary.png`  
📸 `rds-inbound-rules-sg-update.png`

---

### 3️⃣ Launch EC2 and SSH In

Connected via `.pem` key from macOS terminal.

📸 `ec2-instance-summary.png`  
📸 `ec2-instance-dashboard.png`  
📸 `ssh-key-permissions.png`  
📸 `mac-ssh-into-ec2.png`  
📸 `ssh-into-ec2.png`  
📸 `whoami-and-update.png`

---

### 4️⃣ Install Apache Web Server

```bash
sudo yum install -y httpd
sudo systemctl start httpd
sudo systemctl enable httpd
```

📸 `install-apache-start.png`  
📸 `install-apache-complete.png`  
📸 `apache-start-and-enable.png`

---

### 5️⃣ Serve a Web Page

```bash
echo "<h1>Hello from Chet's EC2 Web Server!</h1>" | sudo tee /var/www/html/index.html
```

📸 `echo-html-bugged.png`  
📸 `echo-html-fixed.png`  
📸 `apache-default-page.png`  
📸 `custom-ec2-webpage.png`

---

### 6️⃣ Install MySQL Client on EC2

```bash
sudo yum install -y https://dev.mysql.com/get/mysql80-community-release-el9-1.noarch.rpm
sudo rpm --import https://repo.mysql.com/RPM-GPG-KEY-mysql-2022
sudo yum install -y mysql-community-client
```

📸 `ec2-install-mysql-repo.png`  
📸 `ec2-import-mysql-gpg.png`  
📸 `ec2-install-mysql-client.png`  
📸 `ec2-mysql-client-install-fail.png`

> If install fails:
```bash
sudo yum clean packages
sudo yum clean metadata
sudo yum makecache
sudo yum install -y mysql-community-client --nogpgcheck
```

📸 `ec2-clean-metadata.png`  
📸 `ec2-install-mysql-nogpg.png`  
📸 `ec2-mysql-client-install-success.png`

---

### 7️⃣ Connect to RDS from EC2

```bash
mysql -h webapp-db.cuxami6yiy1p.us-east-1.rds.amazonaws.com -u admin -p
```

📸 `ec2-mysql-login-success.png`

---

### 8️⃣ Create Database and Table

```sql
CREATE DATABASE webapp;
USE webapp;

CREATE TABLE users (
  id INT AUTO_INCREMENT PRIMARY KEY,
  username VARCHAR(50),
  email VARCHAR(100),
  created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

INSERT INTO users (username, email) VALUES
('chet', 'chet@example.com'),
('admin', 'admin@example.com'),
('Alice Smith', 'alice@example.com'),
('Bob Jones', 'bob@example.com');

SELECT * FROM users;
DESCRIBE users;
```

📸 `ec2-create-db-webapp.png`  
📸 `ec2-select-describe-users-table.png`

---

### 9️⃣ Export Table (Optional)

```bash
mysqldump -h webapp-db.cuxami6yiy1p.us-east-1.rds.amazonaws.com -u admin -p webapp users > users.sql
```

📸 `ec2-mysqldump-users.png`  
💾 File saved to `/assets/users.sql`

---

## 📸 Screenshots Summary

All screenshots listed above are stored under `/screenshots/` and chronologically named based on action.

---

## 🧾 Lessons Learned

- Security Groups must allow specific port access between EC2 and RDS
- Amazon Linux 2023 needs special handling for MySQL GPG keys
- Echoing HTML in bash requires escaping `!` and quotes
- Screenshot documentation matters — for projects and interviews

---

## 🧠 Interview Tip

> "This lab demonstrates I can configure full-stack infrastructure in AWS with EC2, RDS, security group tuning, and client/server communication — all validated with real data and CLI work."

---

## 📚 Related Documentation

- `docs/rds-connection-guide.md`
- `docs/ec2-setup-guide.md`
- `docs/load-balancer-setup.md`
- `docs/s3-static-hosting.md`
