# 🚀 Deploy NGINX on AWS EC2 using CloudFormation

This repository contains a **ready-to-use CloudFormation template** and a **complete tutorial** to deploy an **NGINX web server** on AWS EC2 via the AWS CLI.  
Perfect for **learning AWS CloudFormation**, quick deployments, or DevOps demos. 🌍

---

## 📂 Repository Contents
- **`ec2-nginx.yml`** → CloudFormation template that provisions:
  - 🏗️ VPC, Subnet, Internet Gateway  
  - 🔐 Security Group (HTTP + SSH)  
  - 👤 IAM Role + Instance Profile  
  - 💻 EC2 instance running **NGINX in Docker**  

- **`README.md`** → Full tutorial (you’re reading it now!)

---

## 🛠️ Prerequisites
✔️ An **AWS account**  
✔️ Installed **[AWS CLI](https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html)**  
✔️ Basic knowledge of **AWS IAM, EC2, and CloudFormation**  

---

## ⚡ Step 1: Install & Configure AWS CLI

### 🔽 Install AWS CLI
```bash
aws --version

### 🔑 Create IAM User
 - AWS Console → IAM → Users → Create user
 - Username: cloudformation-user
 - Uncheck: "Provide user access to the AWS Management Console"
 - Attach policies:
 - AdministratorAccess (for demo purposes)
 - AWSCloudFormationFullAccess
 - Create user → Security credentials → Create access key (for CLI)
 - Save Access Key ID and Secret Key securely

### ⚙️ Configure AWS CLI
```bash
aws configure

### Provide:
 - AWS Access Key ID: <YOUR_KEY>
 - AWS Secret Access Key: <YOUR_SECRET>
 - Default region name: us-east-1    # or your preferred region
 - Default output format: json








