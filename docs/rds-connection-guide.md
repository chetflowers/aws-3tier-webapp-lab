# RDS Connection Guide

This guide outlines how to connect to the RDS MySQL instance from the EC2 web server instance in the AWS 3-Tier Web App Lab.

## Prerequisites

- EC2 must be in the same VPC as RDS
- Security Group must allow inbound MySQL (port 3306) from EC2 to RDS
- SSH access to EC2 via webserver-key.pem
- MySQL client installed on EC2

## SSH into EC2 Instance

```bash
ssh -i ~/.ssh/webserver-key.pem ec2-user@13.219.81.251
```

## Connect to RDS MySQL

```bash
mysql -h webapp-db.cuxami6yiy1p.us-east-1.rds.amazonaws.com -u admin -p
```

Enter the password when prompted.

## MySQL Commands

```sql
SHOW DATABASES;
USE webapp;
SHOW TABLES;
SELECT * FROM users;
```

Expected Output:

```
+----+-------------+-------------------+---------------------+
| id | username    | email             | created_at          |
+----+-------------+-------------------+---------------------+
|  1 | chet        | chet@example.com  | 2025-05-05 06:43:16 |
|  2 | admin       | admin@example.com | 2025-05-05 06:43:16 |
|  3 | Alice Smith | alice@example.com | 2025-05-05 06:49:17 |
|  4 | Bob Jones   | bob@example.com   | 2025-05-05 06:49:17 |
+----+-------------+-------------------+---------------------+
```

## Export Table (Optional)

```bash
mysqldump -h webapp-db.cuxami6yiy1p.us-east-1.rds.amazonaws.com -u admin -p webapp users > users.sql
```

Save this file to `/assets` if you want to include it in the repo.
