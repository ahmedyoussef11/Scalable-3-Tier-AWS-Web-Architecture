# Highly Available 3-Tier AWS Web Architecture

## 🚀 Project Overview
This project demonstrates the design and implementation of a fault-tolerant, highly available, and secure 3-tier web architecture on Amazon Web Services (AWS). The infrastructure is distributed across multiple Availability Zones to ensure redundancy and high performance.

## 🏗️ Architecture Diagram
<img width="1536" height="1024" alt="aws" src="https://github.com/user-attachments/assets/68743249-03a7-4448-b416-d01b33d7408d" />

## 🛠️ AWS Services Utilized
* **Networking & Security:** Custom VPC, Public/Private Subnets, Internet Gateway, NAT Gateway, Security Groups, IAM Roles.
* **Compute & Scaling:** EC2 Instances, Auto Scaling Groups (ASG), Application Load Balancer (ALB).
* **Database:** Amazon RDS (Multi-AZ deployment for data persistence).

## ⚙️ Implementation Steps

### 1. Network Foundation (VPC & Subnets)
* Created a custom VPC with a CIDR block.
* Designed a 3-tier subnet architecture across 2 Availability Zones (AZs):
  * **Public Subnets:** For the Application Load Balancer (ALB) and NAT Gateways.
  * **Private Subnets (App Tier):** For EC2 instances hosting the web application.
  * **Private Subnets (DB Tier):** For the RDS database instances.
* Configured Route Tables to direct internet traffic appropriately.

### 2. Compute & High Availability
* Created Launch Templates specifying the Amazon Machine Image (AMI) and instance type.
* Configured an **Application Load Balancer (ALB)** in the public subnets to distribute incoming HTTP/HTTPS traffic.
* Implemented an **Auto Scaling Group (ASG)** attached to the ALB target group to automatically scale EC2 instances in the private subnets based on CPU utilization.

### 3. Data Persistence
* Provisioned an **Amazon RDS** MySQL/PostgreSQL database in the private database subnets.
* Enabled Multi-AZ for the database to ensure automatic failover and high availability.

### 4. Security Enforcement
* **Security Groups:** * ALB SG: Allows inbound HTTP/HTTPS from the internet.
  * Web Tier SG: Allows inbound traffic *only* from the ALB SG.
  * Database SG: Allows inbound traffic *only* from the Web Tier SG on port 3306/5432.
* **IAM Roles:** Implemented least-privilege IAM roles for EC2 instances to access required AWS services (like Systems Manager for secure access without SSH keys).
