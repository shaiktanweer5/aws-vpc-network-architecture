# AWS VPC Network Architecture with EC2 Web Server

![AWS](https://img.shields.io/badge/AWS-VPC-orange?logo=amazonaws)
![EC2](https://img.shields.io/badge/Amazon-EC2-orange)
![Linux](https://img.shields.io/badge/Linux-Amazon_Linux-green)
![Status](https://img.shields.io/badge/Project-Completed-brightgreen)
![License](https://img.shields.io/badge/License-MIT-blue)

---

# 📌 Project Overview

This project demonstrates how to design and deploy a secure AWS Virtual Private Cloud (VPC) from scratch and launch an Amazon EC2 web server inside a public subnet.

The project covers core AWS networking concepts including VPCs, Subnets, Internet Gateway, Route Tables, Security Groups, and EC2 while following AWS networking best practices.

---

# 🎯 Project Objective

- Design a custom AWS VPC
- Create Public and Private Subnets
- Configure Internet Gateway
- Configure Route Tables
- Create Security Groups
- Launch an EC2 Instance
- Deploy an Apache Web Server
- Verify public internet access

---

# 📚 Table of Contents

- Project Overview
- Project Objective
- AWS Services Used
- Project Architecture
- Network Configuration
- Security Group Rules
- Implementation Steps
- Project Screenshots
- Skills Demonstrated
- Key Learnings
- Cleanup
- Repository
- Connect With Me

---

# 🚀 AWS Services Used

- Amazon VPC
- Public Subnet
- Private Subnet
- Internet Gateway (IGW)
- Route Tables
- Security Groups
- Amazon EC2
- Amazon Linux 2023

---

# 🏗️ Project Architecture

```text
                    Internet
                        │
                        ▼
               Internet Gateway
                        │
                        ▼
                 AWS VPC (10.0.0.0/16)
                ┌─────────────────────┐
                │                     │
                │ Public Subnet       │
                │ 10.0.1.0/24         │
                │                     │
                │  EC2 Web Server     │
                │                     │
                └─────────────────────┘
                        │
                Route Table (0.0.0.0/0)
                        │
                Internet Gateway

                ┌─────────────────────┐
                │ Private Subnet      │
                │ 10.0.2.0/24         │
                └─────────────────────┘
```

---

# 🌐 Network Configuration

| Resource | Configuration |
|----------|---------------|
| VPC | 10.0.0.0/16 |
| Public Subnet | 10.0.1.0/24 |
| Private Subnet | 10.0.2.0/24 |
| Internet Gateway | Attached |
| Route Table | Public Route Table |
| EC2 Instance | Amazon Linux 2023 |
| Instance Type | t2.micro |
| Security Group | SSH + HTTP |

---

# 🔐 Security Group Rules

## Inbound Rules

| Type | Port | Source |
|------|------|--------|
| SSH | 22 | My IP |
| HTTP | 80 | Anywhere (0.0.0.0/0) |

## Outbound Rules

- Allow All Traffic

---

# ⚙️ Implementation Steps

### Step 1

Created a custom VPC with CIDR block:

```
10.0.0.0/16
```

---

### Step 2

Created:

- Public Subnet (10.0.1.0/24)
- Private Subnet (10.0.2.
