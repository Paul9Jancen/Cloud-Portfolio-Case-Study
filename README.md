Cloud Portfolio Case Study — AWS Multi-Tier Web Application
✅ Project Overview

This project demonstrates a production-grade multi-tier web application architecture built entirely using AWS Free Tier services.
It is designed to scale to hundreds of users, maintain high availability, and enforce enterprise governance without incurring any cost.

Key Goals

Build a multi-tier system

Scale automatically (2–4 instances)

Implement monitoring, logging, and compliance

Maintain Free Tier safety

Prepare a portfolio-ready case study

🏗 Architecture Diagram (Logical)
Internet
   |
   v
Application Load Balancer (ALB)
   |
   v
Target Group (Web-TG)
   |
   v
Auto Scaling Group (Web-ASG)
   |
   v
EC2 Instances (Web Servers)
   |
   v
(Optionally connect to RDS/NoSQL in future)


High Availability

Deployed across 2 AZs (us-east-1a & us-east-1b)

Load-balanced traffic

Auto-scaling across zones

⚙️ Components
Component	Purpose	Status
VPC	Network isolation	Deployed
Public Subnets	Internet-facing web tier	Deployed
Security Groups	Allow only required traffic	Deployed
ALB	Distributes traffic across instances	Deployed
Target Group	Health checks and routing	Deployed
Auto Scaling Group	Automatic scaling 2–4 instances	Deployed
EC2 Instances	Web server hosts	Deployed
CloudWatch Logs	Central log storage	Deployed
CloudWatch Alarm	CPU threshold monitoring	Deployed
AMI Backup	Automated instance backups	Deployed
CloudTrail	Audit logs for all events	Deployed
AWS Config	Compliance rules and monitoring	Deployed
Tags	Enterprise-level resource management	Deployed
🧩 Detailed Features
1. High Availability & Scaling

ALB distributes traffic across multiple AZs

ASG maintains minimum 2 instances

Target tracking policy scales automatically between 2–4 instances

CPU target set at 50%

2. Monitoring & Alerts

CloudWatch Logs for web server logs

CloudWatch Alarm (Web-HighCPU)

Trigger: CPU > 80%

Period: 1 minute

Notifies via SNS (if configured)

3. Backup & Recovery

AMI Backup created for EC2 instances

Provides ability to restore instances quickly

4. Security & Compliance

No open SSH access (only via SSM)

CloudTrail enabled for Management + Data events

AWS Config with compliance rules:

restricted-ssh

ec2-instance-profile-attached

elb-logging-enabled

5. Enterprise Tagging

Standard tags applied across all resources:

Environment: Production

Project: Cloud-Portfolio

Owner: Paul Jancen De Guzman

ManagedBy: Manual

CostCenter: Engineering

🚀 Deployment Steps (What was done)

Create VPC & subnets

Create Security Groups

Create IAM Role (SSM)

Create Launch Template (Web-LT)

Create Target Group (Web-TG)

Create Application Load Balancer (MyALB)

Create Auto Scaling Group (Web-ASG)

Create CloudWatch Logs & Alarm

Create AMI backup

Enable CloudTrail

Enable AWS Config + Compliance rules

Apply enterprise tagging

🔍 How to Verify (Final Validation)
1. Check ALB

Go to EC2 → Load Balancers

Confirm MyALB is Active

Copy DNS and access in browser

2. Check Target Group

Go to EC2 → Target Groups

Confirm Web-TG has 2 Healthy targets

3. Check ASG

Go to EC2 → Auto Scaling Groups

Confirm Web-ASG is Active

Confirm capacity is Min 2, Desired 2, Max 4

4. Check CloudWatch

Go to CloudWatch → Alarms

Confirm Web-HighCPU is Active

5. Check Compliance

Go to AWS Config

Confirm all 3 rules are Active and compliant

💸 Cost Analysis (Free Tier Safe)

This architecture is built to stay within Free Tier:

Service	Free Tier Impact	Notes
EC2	750 hours/month	Using t3.micro or free tier eligible instances
ALB	Not free	But minimal cost if idle; use only for portfolio demo
CloudWatch	Free tier limits	Logs and alarms within limits
CloudTrail	Free tier	First trail free
AWS Config	Not free normally	Use minimal rules and delete after demo if cost is concern

Important: ALB is not fully free, but remains low-cost in small demo usage.

📌 Scaling Plan (How It Scales to Hundreds of Users)
Scenario	What Happens	Result
Low traffic	2 instances running	Minimum cost
Increased traffic	CPU > 50%	ASG adds instances
High traffic	More instances needed	Up to 4 instances
Extreme traffic	4 instances at 100%	Consider adding RDS / caching
🛡 RTO / RPO Plan
RTO (Recovery Time Objective)

EC2 failure → Auto Scaling launches new instance within minutes

ALB failure → AWS-managed (rare)

Region failure → Not covered (requires multi-region design)

RPO (Recovery Point Objective)

Web server data is ephemeral

Use S3 or EFS for persistent data (future upgrade)

📌 Monitoring Plan
Monitoring	Tool	Alert
CPU usage	CloudWatch	Alarm at 80%
Application logs	CloudWatch Logs	Streamed
Audit logs	CloudTrail	Stored in S3
Compliance	AWS Config	Rules enforced
📌 What Could Be Upgraded (Future Improvements)

These upgrades are beyond Free Tier or not needed for this portfolio:

Add RDS database in private subnet

Add Redis caching (ElastiCache)

Add WAF for security

Add Route 53 with custom domain

Add HTTPS (ACM + TLS)

Add multi-region DR

🧾 Final Notes

This architecture proves that you can design a production-grade, scalable, compliant multi-tier system using AWS Console and without writing any code or using paid services.

It is a strong portfolio case study demonstrating:

Cloud architecture thinking

Security best practices

Compliance and governance

Cost-aware design

Operational excellence
