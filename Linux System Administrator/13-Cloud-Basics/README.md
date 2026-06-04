# Phase 13: Cloud Basics (8 Days)

> Modern Linux administrators must work on AWS, Azure, and GCP. Learn cloud fundamentals and how to manage Linux instances in cloud environments.

**Phase Duration**: 8 days

---

## 📋 What You'll Learn

```
├── Cloud Computing Concepts
├── AWS EC2 Instances
├── Security Groups & VPC
├── Storage (S3, EBS)
├── IAM (Identity & Access)
├── Load Balancers
├── Auto Scaling
├── Azure/GCP Basics
└── Cost Optimization
```

---

## 🗓️ गाइड

### **DAY 1-2: Cloud Concepts**

```bash
# Cloud models:
IaaS: Infrastructure as a Service (AWS EC2)
PaaS: Platform as a Service (Heroku)
SaaS: Software as a Service (Google Workspace)

# Key concepts:
Regions: भौगोलिक location
Availability Zones: Data centers
VPC: Virtual network
Subnet: Network partition
```

---

### **DAY 3-4: AWS EC2**

```bash
# Launch instance:
# AWS Console → EC2 → Launch Instance
# AMI select करो (Ubuntu, Amazon Linux)
# Instance type (t2.micro, t2.small)
# Security group setup
# Key pair generate/select

# SSH connect:
ssh -i key.pem ubuntu@ec2-instance-ip
ssh -i key.pem ec2-user@instance-ip  # Amazon Linux
```

---

### **DAY 5-6: Security Groups & VPC**

```bash
# Security Group: Firewall की तरह

Inbound Rules:
- SSH (22): 0.0.0.0/0 (या restricted IP)
- HTTP (80): 0.0.0.0/0
- HTTPS (443): 0.0.0.0/0

Outbound Rules:
- All traffic (default)

# VPC Setup:
1. VPC create करो
2. Subnet बनाओ (public + private)
3. Route table configure करो
4. Instances launch करो
```

---

### **DAY 7-8: Storage & IAM**

```bash
# S3 (Simple Storage Service):
# File storage (जैसे Google Drive)

# EBS (Elastic Block Storage):
# Persistent disk (जैसे hard drive)

# IAM (Identity & Access Management):
# Users, Groups, Roles, Policies

# Example IAM policy:
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": "ec2:*",
      "Resource": "*"
    }
  ]
}
```

---

## 💡 Common AWS Services

```
EC2:        Virtual machines
S3:         Object storage
RDS:        Managed databases
Lambda:     Serverless computing
CloudWatch: Monitoring
Route53:    DNS
ELB/ALB:    Load balancing
```

---

अगला: **Phase 14: Automation with Ansible**
