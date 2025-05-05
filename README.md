# AWS 3-Tier Web App Lab

This project demonstrates a basic 3-tier web application hosted on AWS. It includes a public-facing web server, a private database backend, and static assets. The goal is to walk through real-world deployment and connection of services across EC2, RDS, and S3.

---

## 📐 Architecture Overview

```
Browser
   │
   ▼
[ Application Tier: EC2 Instance ]
   │
   ▼
[ Database Tier: Amazon RDS (MySQL) ]
```

---

## 📦 Project Structure

```
aws-3tier-webapp-lab/
├── README.md
├── app/                        # Static HTML frontend
│   └── index.html
├── assets/                     # (Optional) schema dumps, screenshots
│   └── users.sql
├── docs/
│   ├── ec2-setup-guide.md
│   ├── rds-connection-guide.md
│   ├── load-balancer-setup.md
│   └── s3-static-hosting.md
```

---

## 🔧 Components

### 1. EC2 Web Server
- Amazon Linux 2023
- Apache (`httpd`) installed
- Serves `/var/www/html/index.html`
- SSH with `webserver-key.pem`

### 2. Amazon RDS (MySQL)
- MySQL 8.0
- Database: `webapp`
- Table: `users`
- Access from EC2 via private subnet & SG rule on port `3306`

### 3. S3 Static Assets (Optional)
- Hosting documentation or frontend files

---

## 💻 Demo Data

Sample `users` table in MySQL:

| id | username    | email             | created_at          |
|----|-------------|-------------------|---------------------|
| 1  | chet        | chet@example.com  | 2025-05-05 06:43:16 |
| 2  | admin       | admin@example.com | 2025-05-05 06:43:16 |
| 3  | Alice Smith | alice@example.com | 2025-05-05 06:49:17 |
| 4  | Bob Jones   | bob@example.com   | 2025-05-05 06:49:17 |

---

## 📓 Guides

- [`docs/ec2-setup-guide.md`](docs/ec2-setup-guide.md) – Provision EC2 and install Apache
- [`docs/rds-connection-guide.md`](docs/rds-connection-guide.md) – Connect from EC2 to RDS
- [`docs/load-balancer-setup.md`](docs/load-balancer-setup.md) – Add HA via ALB
- [`docs/s3-static-hosting.md`](docs/s3-static-hosting.md) – (Optional) serve static files via S3

---

## 📸 Screenshots (save to `/assets`)
- ✅ Web server HTML render from browser
- ✅ Successful MySQL CLI query from EC2
- ✅ AWS Console views (EC2 instance, RDS instance)

---

## 🧠 Lessons Learned

- Cloud networking matters: correct VPC, subnets, and security groups are **critical** for service communication.
- MySQL CLI and security key setup can get finicky—understanding public vs private access is huge.
- `mysqldump` is your friend when you want to back up or export schemas.
- Markdown documentation helps clarify what happened, and lets others (or future you) replicate steps easily.
- Coding a full web app backend/frontend is complex, but standing up infrastructure is a valuable first step into cloud architecture.

---

## ✅ Next Steps (Optional)

- Add an ALB (Application Load Balancer) and autoscaling group
- Use a real app framework like Flask or Node.js
- Secure with HTTPS using ACM + Route 53
