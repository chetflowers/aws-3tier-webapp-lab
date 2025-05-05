# Load Balancer Setup Guide

This guide explains how to add a load balancer in front of your EC2 instance(s) to distribute traffic and provide high availability for your 3-tier web app.

## ✅ Prerequisites

- EC2 instance(s) running and healthy
- Security Group allowing HTTP (80) traffic
- IAM permissions to create ELB and Target Groups

## 🌐 Create Target Group

1. Go to **EC2 → Target Groups**
2. Create a new group:
   - Target type: Instances
   - Protocol: HTTP
   - Port: 80
   - VPC: Same as EC2
3. Register your EC2 instance

## 🧰 Create Application Load Balancer (ALB)

1. Go to **EC2 → Load Balancers**
2. Create **Application Load Balancer**
   - Scheme: Internet-facing
   - Listeners: HTTP on port 80
   - VPC/Subnets: Use public subnets
3. Security Group: Allow inbound HTTP (port 80)
4. Target Group: Select the one you just created

## 🔍 Verify Setup

1. Wait for ALB to become active
2. Open the ALB DNS name in your browser
3. You should see your custom EC2 page:  
   _“Hello from Chet's EC2 Web Server!”_

## 📸 Suggested Screenshots

- Load Balancer summary  
- Target Group health check status  
- Browser showing site via ALB DNS

## 🧠 Notes

- Health check failures = ALB won’t route traffic
- You can scale EC2 by registering multiple instances
- Optionally configure HTTPS with ACM + Listener Rules
