# clarusway-week9-deployment
AWS Auto Scaling + ALB + S3 website deployment for Clarusway Bootcamp
# Week 9 Deployment – Clarusway Bootcamp 🚀

🎓 Prepared by: **Renad**  
📅 Date: April 2025  
🧠 Deployment Type: S3 Static Hosting + EC2 with Auto Scaling + Application Load Balancer (ALB)

---

## 💡 Project Objective

Deploy a scalable and highly available web app using AWS tools:
- Host static content in **S3**
- Serve dynamic content with **EC2 + NGINX**
- Scale using **Auto Scaling Group**
- Load balance using **ALB**
- Health check using **Target Group**

---

## 🧰 Tech Stack

- Amazon S3
- Amazon EC2 (Amazon Linux 2)
- Auto Scaling Group (ASG)
- Application Load Balancer (ALB)
- IAM Roles
- User Data script
- Security Groups

---

## ⚙️ Infrastructure Overview

### 🔹 Static Website via S3
- Bucket: `renad-sda2023-clarusway-assets`
- Static hosting enabled
- Public access configured
- Files uploaded: `index.html`, `logo.png`, `sda.png`
- ✅ [S3 URL](http://renad-sda2023-clarusway-assets.s3-website.eu-north-1.amazonaws.com/)

---

### 🔹 Launch Template User Data Script

```bash
#!/bin/bash
yum update -y
amazon-linux-extras enable nginx1
yum install -y nginx
systemctl start nginx
systemctl enable nginx
echo "<h1>Served by: $(hostname)</h1>" > /usr/share/nginx/html/index.html
```
🔹 Auto Scaling Group
Launch template: clarusway-template

Min: 1, Max: 3, Desired: 2

Target Group linked

Instances running and passing health checks ✅

🔹 Application Load Balancer (ALB)
Type: Application

Scheme: Internet-facing

Listener: port 80

Linked to Target Group

✅ DNS:
http://clarusway-alb2-318312631.eu-north-1.elb.amazonaws.com/

Example response:
Served by: ip-172-31-30-159

