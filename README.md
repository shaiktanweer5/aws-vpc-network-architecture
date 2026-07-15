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

Created the following subnets inside the VPC:

- Public Subnet: **10.0.1.0/24**
- Private Subnet: **10.0.2.0/24**

The public subnet is used for resources that require internet access, while the private subnet is reserved for internal resources.

---

### Step 3

Created an Internet Gateway (IGW) and attached it to the VPC to enable internet connectivity.

---

### Step 4

Created a Public Route Table.

Configured the route table to allow internet access through the Internet Gateway.

---

### Step 5

Added the following route to the Public Route Table:

```text
Destination:
0.0.0.0/0

Target:
Internet Gateway
```

This route allows outbound internet traffic from the public subnet.

---

### Step 6

Associated the **Public Subnet** with the **Public Route Table**.

This ensures that all resources launched in the public subnet can communicate with the Internet Gateway.

---

### Step 7

Enabled **Auto Assign Public IPv4 Address** for the Public Subnet.

This automatically assigns a public IP address to EC2 instances launched in the public subnet.

---

### Step 8

Created a Security Group named:

```
Project-Web-SG
```

Configured the following inbound rules:

| Type | Port | Source |
|------|------|--------|
| SSH | 22 | My IP |
| HTTP | 80 | Anywhere (0.0.0.0/0) |

Outbound Rule:

- Allow All Traffic

---

### Step 9

Launched an Amazon EC2 instance with the following configuration:

| Setting | Value |
|---------|-------|
| AMI | Amazon Linux 2023 |
| Instance Type | t2.micro |
| Network | Project-VPC |
| Subnet | Public Subnet |
| Auto Assign Public IP | Enabled |
| Security Group | Project-Web-SG |
| Key Pair | Project-KeyPair |

---

### Step 10

Connected to the EC2 instance using SSH.

Updated the system packages:

```bash
sudo yum update -y
```

Installed Apache Web Server:

```bash
sudo yum install httpd -y
```

Enabled Apache to start automatically:

```bash
sudo systemctl enable httpd
```

Started the Apache service:

```bash
sudo systemctl start httpd
```

Verified that Apache was running:

```bash
sudo systemctl status httpd
```

---

### Step 11

Created a sample web page.

```bash
sudo nano /var/www/html/index.html
```

Added the following HTML:

```html
<!DOCTYPE html>
<html>
<head>
    <title>AWS VPC Project</title>
</head>
<body>
    <h1>🚀 AWS VPC Project</h1>
    <p>Hosted on Amazon EC2</p>
    <p>Created by Tanweer Ahmed</p>
</body>
</html>
```

Saved the file and accessed the EC2 Public IP from a web browser.

The webpage loaded successfully, confirming that the VPC, Internet Gateway, Route Table, Security Group, EC2 instance, and Apache Web Server were configured correctly.

---

# 📷 Project Screenshots

## 1. VPC Created

Created a custom VPC with CIDR block **10.0.0.0/16**.

![VPC Created](screenshots/01-vpc-created.png)

---

## 2. Public Subnet Created

Created a public subnet (**10.0.1.0/24**) for internet-facing resources.

![Public Subnet](screenshots/02-public-subnet-created.png)

---

## 3. Private Subnet Created

Created a private subnet (**10.0.2.0/24**) for internal resources.

![Private Subnet](screenshots/03-private-subnet-created.png)

---

## 4. Internet Gateway Created

Created an Internet Gateway to provide internet connectivity.

![Internet Gateway](screenshots/04-internet-gateway-created.png)

---

## 5. Internet Gateway Attached

Attached the Internet Gateway to the custom VPC.

![IGW Attached](screenshots/05-igw-attached.png)

---

## 6. Public Route Table Created

Created a dedicated Public Route Table.

![Public Route Table](screenshots/06-public-route-table-created.png)

---

## 7. Route Added

Added a default route (0.0.0.0/0) pointing to the Internet Gateway.

![Route Added](screenshots/07-route-added.png)

---

## 8. Public Subnet Associated

Associated the Public Subnet with the Public Route Table.

![Subnet Association](screenshots/08-public-subnet-associated.png)

---

## 9. Auto Public IP Enabled

Enabled automatic assignment of Public IPv4 addresses.

![Auto Public IP](screenshots/09-auto-public-ip-enabled.png)

---

## 10. Security Group Created

Configured Security Group rules allowing SSH and HTTP traffic.

![Security Group](screenshots/10-security-group-created.png)

---

## 11. Apache Web Server Running

Successfully deployed the Apache web server and verified it using the EC2 Public IP.

![Web Server](screenshots/11-webpage-running.png)

---

## 12. EC2 Instance Running

Amazon EC2 instance running successfully in the Public Subnet.

![EC2 Instance](screenshots/12-ec2-instance-running.png)

---

# 💡 Skills Demonstrated

- Amazon VPC
- CIDR Block Planning
- Public & Private Subnets
- Internet Gateway (IGW)
- Route Tables
- Security Groups
- Amazon EC2
- Linux Administration
- Apache HTTP Server
- AWS Networking Fundamentals

---

# 📖 Key Learnings

- Designed a custom AWS VPC from scratch.
- Planned CIDR ranges for VPC and subnets.
- Understood the difference between Public and Private Subnets.
- Configured Internet Gateway and Route Tables.
- Secured resources using Security Groups.
- Launched an EC2 instance in a Public Subnet.
- Installed and configured Apache Web Server.
- Verified web application accessibility over the Internet.

---

# 🧹 Cleanup

To avoid unnecessary AWS charges, the following resources were deleted after completing the project:

- EC2 Instance
- Security Group
- Route Tables
- Internet Gateway
- Public Subnet
- Private Subnet
- VPC

- ---

# 📂 Repository

GitHub Repository:

https://github.com/shaiktanweer5/aws-vpc-network-architecture

---

# 👨‍💻 Connect With Me

### 🌐 Portfolio

https://tanweerahmed.in

### 💼 LinkedIn

https://www.linkedin.com/in/shaik-tanweer-ahmed/

### 🖥 GitHub

https://github.com/shaiktanweer5

---

## ⭐ Support

If you found this project useful, please consider giving this repository a ⭐ on GitHub.
