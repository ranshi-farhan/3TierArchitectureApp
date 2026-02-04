# AWS 3-Tier Architecture Project

## Author

**Ranshi**

---

## 📌 Project Overview

This project demonstrates the implementation of a **highly available, fault-tolerant AWS 3-Tier Architecture**. The architecture is designed using best practices with clear separation of concerns across **Web**, **Application**, and **Database** tiers.

The project focuses on real-world cloud infrastructure design rather than just application code, making it suitable for learning and hands-on practice with real-world cloud infrastructure.

---

## 🏗️ Architecture Breakdown

### 1️⃣ Web Tier (Presentation Layer)

* Hosted on **EC2 instances** in **public subnets**
* Uses **Nginx** to serve frontend content
* Fronted by an **External Application Load Balancer (ALB)**
* Accessible over **HTTP/HTTPS**

### 2️⃣ Application Tier (Business Logic Layer)

* **Python-based backend application**
* Runs on **EC2 instances in private subnets**
* Managed behind an **Internal Application Load Balancer**
* Uses **PM2 / process management** only for service control (not Node.js app)

### 3️⃣ Database Tier (Data Layer)

* **Amazon RDS (MySQL)**
* Deployed in **private subnets**
* Public access disabled
* Access restricted via **Security Groups**

---

## ☁️ AWS Services Used

* Amazon VPC
* Public & Private Subnets
* Internet Gateway & NAT Gateway
* EC2
* Application Load Balancers (External & Internal)
* Auto Scaling Groups
* Amazon RDS (MySQL)
* Amazon S3
* IAM Roles
* AWS Systems Manager (SSM)
* Route 53
* AWS Certificate Manager (ACM)

---

## 🔐 Security Design

* Separate security groups for each tier
* No public access to App or DB tier
* Internal ALB for backend traffic
* IAM Role used instead of Bastion Host
* Database credentials used only for internal connectivity

---

## ⚙️ Application Flow

1. User accesses the application via **Domain / ALB DNS**
2. Traffic hits **External ALB**
3. Requests are forwarded to **Web Tier**
4. Web Tier proxies API calls to **Internal ALB**
5. Internal ALB routes traffic to **App Tier**
6. App Tier communicates securely with **RDS MySQL**

---

## 📦 S3 Usage

* Stores application artifacts and configuration files
* Web tier and app tier instances pull code from S3
* Simplifies deployment and updates

---

## 🧪 Health Checks

* Application exposes a health endpoint
* Load balancers use health checks for traffic routing
* Ensures high availability and fault tolerance

---

## 🧹 Cleanup Strategy

To avoid unnecessary AWS charges, resources are deleted in the following order:

1. Auto Scaling Groups
2. Load Balancers
3. Target Groups
4. AMIs & Snapshots
5. RDS Instance
6. S3 Bucket
7. ACM Certificate
8. Route 53 Records
9. NAT Gateway & Elastic IP
10. VPC

---

## 🎯 Key Takeaways

* Real-world AWS architecture implementation
* Strong focus on security and scalability
* Clear separation of infrastructure layers

---

## 📌 Notes

* This project is for **learning and demonstration purposes**
* Secrets should be managed using **AWS Secrets Manager or SSM Parameter Store** in production

---

⭐ If you find this project useful, feel free to star the repository and use it as a reference for your AWS learning journey.
