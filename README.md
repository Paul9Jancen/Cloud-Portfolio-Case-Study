# Cloud Portfolio Case Study — ALB + ASG Production Web App

## Project Title
**High Availability Web Application with ALB + ASG (AWS)**

---

## 1. Project Summary
This case study demonstrates a **production-ready AWS infrastructure** that delivers a scalable, highly available web application using:

- **Application Load Balancer (ALB)**
- **Auto Scaling Group (ASG)**
- **Target Group Health Checks**
- **Launch Template with User Data**
- **Multi-AZ VPC Design**
- **Public & Private Subnets**
- **NAT Gateway for Private Subnets**

📌 The goal is to showcase cloud architecture design, automation, and reliability.

---

## 2. Problem Statement
Many applications fail to handle traffic spikes and server failures.  
This project addresses these issues by implementing:

- **Automatic scaling during high traffic**
- **Fault tolerance when an instance fails**
- **Load balancing to distribute traffic**
- **Health checks to ensure only healthy instances receive traffic**

---

## 3. Solution Overview
The infrastructure automatically deploys EC2 instances in a multi-AZ setup and uses ALB to distribute traffic.  
ASG maintains the desired capacity and replaces unhealthy instances.

### Final Result
The ALB returns:

ALB + ASG WORKING

yaml
Copy code

---

## 4. Architecture Diagram
Internet
|
v
[ALB] ---> [Target Group] ---> [ASG] ---> [EC2 Instances]
|
[Launch Template]
|
[User Data Script]

pgsql
Copy code

---

## 5. Key Components & Why They Matter

| Component | Purpose | Outcome |
|----------|---------|---------|
| **ALB** | Load balancing + High availability | Traffic is distributed evenly |
| **ASG** | Auto scaling + self-healing | Maintains minimum instance count |
| **Target Group** | Health check enforcement | Only healthy instances serve traffic |
| **Launch Template** | Automated instance configuration | Instances ready immediately |
| **User Data Script** | Auto installs web server | Zero manual server setup |
| **Multi-AZ** | Fault tolerance | No single point of failure |

---

## 6. Implementation Details

### 6.1 VPC Design
- 1 VPC (Production)
- 2 Public Subnets (2 AZs)
- 2 Private Subnets (2 AZs)
- Internet Gateway for public subnets
- NAT Gateway for private subnets

### 6.2 Security
- **ALB Security Group**
  - Allow inbound HTTP 80 from anywhere
- **Web Security Group**
  - Allow inbound HTTP 80 only from ALB SG

### 6.3 Launch Template (User Data)
```bash
#!/bin/bash
yum update -y
yum install -y httpd
systemctl start httpd
systemctl enable httpd
echo "ALB + ASG WORKING" > /var/www/html/index.html
7. Verification & Results
Final Output
ALB returns 200 OK

Web page displays:

nginx
Copy code
ALB + ASG WORKING
Target group shows Healthy instances

ASG maintains 2 InService instances

8. Lessons Learned (Case Study Insight)
Auto Scaling is essential for reliability and cost optimization.

Health checks ensure users never hit a broken server.

Launch templates + user data make deployments consistent and repeatable.

Multi-AZ design improves fault tolerance.
