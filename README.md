# 🚀 Deploy NGINX on AWS EC2 using CloudFormation

This repository contains a **ready-to-use CloudFormation template** and a **complete tutorial** to deploy an NGINX web server on AWS EC2 via the AWS CLI.  
Perfect for **learning AWS CloudFormation**, quick deployments, or DevOps demos. 🌍

---

## 📂 Repository Contents
- **`ec2-nginx.yml`** → CloudFormation template that provisions:
  - VPC, Subnet, Internet Gateway
  - Security Group (HTTP + SSH)
  - IAM Role + Instance Profile
  - EC2 instance running **NGINX in Docker**
- **`README.md`** → Full tutorial (you’re reading it now!)

- ## 🛠️ Prerequisites
- An **AWS account**
- Installed [AWS CLI](https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html)
- Basic knowledge of AWS IAM, EC2, and CloudFormation

- ## ⚡ Step 1: Install & Configure AWS CLI

### Install
- **Windows**: Download MSI installer from [AWS CLI](https://aws.amazon.com/cli/).  
- **Linux/Mac**: Follow [docs](https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html).

Verify installation:
**aws --version**

**Configure**

**Create an IAM User in AWS Console:**
Go to IAM → Users → Create user

Name: cloudformation-user
Uncheck “Provide user access to the AWS Management Console”
Attach policies:
AdministratorAccess (demo purpose)
AWSCloudFormationFullAccess
Create user → Security Credentials → Create Access Key → CLI access
Save Access Key ID and Secret Key

Now run: **aws configure**
Provide: AWS Access Key ID: <YOUR_KEY>
AWS Secret Access Key: <YOUR_SECRET>
Default region name: us-east-1 < Any Region you want to use the template>
Default output format: json
Verify: **aws sts get-caller-identity**

Expected output:
{
  "UserId": "AIDASAMPLEUSERID",
  "Account": "123456789012",
  "Arn": "arn:aws:iam::123456789012:user/cloudformation-user"
}

🔑 Step 2: Create EC2 Key Pair
aws ec2 create-key-pair --key-name nginx-keypair --query 'KeyMaterial' --output text > nginx-keypair.pem
OR
You can create by visiting AWS Management Console's EC2

Verify : **aws ec2 describe-key-pairs --key-name nginx-keypair**

📝 Step 3: CloudFormation Template
 Refer to the ec2-nginx.yml file inside the Template Directory

☁️ Step 4: Deploy the Stack
Get your public IP: **curl https://checkip.amazonaws.com/**

Deploy: 
aws cloudformation create-stack \
  --template-file ec2-nginx.yml \
  --stack-name NginxOnEC2 \
  --parameter-overrides KeyPairName=nginx-keypair YourIPAddress=<YOUR_IP>/32 \
  --capabilities CAPABILITY_IAM

⏱️ Step 5: Monitor Progress :
Check Events: **aws cloudformation describe-stack-events --stack-name NginxOnEC2**
Check Status: **aws cloudformation describe-stacks --stack-name NginxOnEC2 --query "Stacks[0].StackStatus"**

✅ When it says CREATE_COMPLETE, your resources are ready.

🌐 Step 6: Access Your Website
Get the URL:
aws cloudformation describe-stacks \
  --stack-name NginxOnEC2 \
  --query "Stacks[0].Outputs[?OutputKey=='WebsiteURL'].OutputValue" \
  --output text
Example: **http://ec2-34-207-141-253.compute-1.amazonaws.com**

🧹 Step 7: Cleanup
Delete stack and all resources: **aws cloudformation delete-stack --stack-name NginxOnEC2**


✅ Summary

⭐Installed and configured AWS CLI
⭐Created IAM user and EC2 key pair
⭐Built CloudFormation template (ec2-nginx.yml)
⭐Deployed NGINX server on EC2
⭐Retrieved public URL & tested deployment
⭐Cleaned up resources


