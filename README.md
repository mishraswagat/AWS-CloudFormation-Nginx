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
```
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
```
### Provide:
 - AWS Access Key ID: <YOUR_KEY>
 - AWS Secret Access Key: <YOUR_SECRET>
 - Default region name: us-east-1    # or your preferred region
 - Default output format: json
### Verify:
```bash
aws sts get-caller-identity
```
### Expected output:
 - {
 - "UserId": "AIDASAMPLEUSERID",
 - "Account": "123456789012",
 - "Arn": "arn:aws:iam::123456789012:user/cloudformation-user"
 - }


## 🔑 Step 2: Create EC2 Key Pair
```bash
aws ec2 create-key-pair --key-name nginx-keypair --query 'KeyMaterial' --output text > nginx-keypair.pem
```
### Verify:
```bash
aws ec2 describe-key-pairs --key-name nginx-keypair
```
## 📝 Step 3: CloudFormation Template
 - The template can be found inside the Template Folder named as ec2-nginx.yml

## ☁️ Step 4: Deploy the Stack

### Get your public IP:
```bash
curl https://checkip.amazonaws.com/
```
### Deploy:
```bash
aws cloudformation create-stack \
  --template-file ec2-nginx.yml \
  --stack-name NginxOnEC2 \
  --parameter-overrides KeyPairName=nginx-keypair YourIPAddress=<YOUR_IP>/32 \
  --capabilities CAPABILITY_IAM
```
## ⏱️ Step 5: Monitor Progress
### Check Events:
```bash
aws cloudformation describe-stack-events --stack-name NginxOnEC2
```
### Check Status: 
```bash
aws cloudformation describe-stacks \
  --stack-name NginxOnEC2 \
  --query "Stacks[0].StackStatus"
```
✅ When it shows CREATE_COMPLETE, your resources are ready.

## 🌐 Step 6: Access Your Website
```bash
aws cloudformation describe-stacks \
  --stack-name NginxOnEC2 \
  --query "Stacks[0].Outputs[?OutputKey=='WebsiteURL'].OutputValue" \
  --output text
```
### Example: http://ec2-34-207-141-253.compute-1.amazonaws.com

## 🧹 Step 7: Cleanup
### Delete all resources:
```bash
aws cloudformation delete-stack --stack-name NginxOnEC2
```

### ✅ Summary

⭐ Installed and configured AWS CLI
⭐ Created IAM user and EC2 key pair
⭐ Built CloudFormation template (ec2-nginx.yml)
⭐ Deployed NGINX server on EC2
⭐ Retrieved public URL & tested deployment
⭐ Cleaned up resources


