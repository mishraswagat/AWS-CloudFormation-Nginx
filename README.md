🚀 Deploy NGINX on AWS EC2 using CloudFormation
This guide contains a ready-to-use CloudFormation template (not included here) and a complete tutorial to deploy an NGINX web server on AWS EC2 via the AWS CLI.
Perfect for learning AWS CloudFormation, quick deployments, or DevOps demos. 🌍
📂 Repository Contents
• ec2-nginx.yml → CloudFormation template (skip content here)
• README / This document → Full tutorial
🛠️ Prerequisites
✔️ An AWS account
✔️ Installed AWS CLI
✔️ Basic knowledge of AWS IAM, EC2, and CloudFormation
⚡ Step 1: Install & Configure AWS CLI
Install AWS CLI and verify installation:
aws --version
Create IAM user with AdministratorAccess + AWSCloudFormationFullAccess, save keys.
Configure CLI:
aws configure
🔑 Step 2: Create EC2 Key Pair
Create key pair:
aws ec2 create-key-pair --key-name nginx-keypair --query 'KeyMaterial' --output text > nginx-keypair.pem
Verify: aws ec2 describe-key-pairs --key-name nginx-keypair
📝 Step 3: CloudFormation Template
Refer to ec2-nginx.yml file in the repo. (Content skipped here)
☁️ Step 4: Deploy the Stack
Get your public IP: curl https://checkip.amazonaws.com/
Deploy:
aws cloudformation create-stack \
  --template-file ec2-nginx.yml \
  --stack-name NginxOnEC2 \
  --parameter-overrides KeyPairName=nginx-keypair YourIPAddress=<YOUR_IP>/32 \
  --capabilities CAPABILITY_IAM
⏱️ Step 5: Monitor Progress
Check events: aws cloudformation describe-stack-events --stack-name NginxOnEC2
Check status: aws cloudformation describe-stacks --stack-name NginxOnEC2 --query "Stacks[0].StackStatus"
✅ When CREATE_COMPLETE, resources are ready.
🌐 Step 6: Access Your Website
aws cloudformation describe-stacks \
  --stack-name NginxOnEC2 \
  --query "Stacks[0].Outputs[?OutputKey=='WebsiteURL'].OutputValue" \
  --output text
Example: http://ec2-xx-xx-xx-xx.compute-1.amazonaws.com
🧹 Step 7: Cleanup
Delete all resources:
aws cloudformation delete-stack --stack-name NginxOnEC2
✅ Summary
⭐ Installed and configured AWS CLI
⭐ Created IAM user and EC2 key pair
⭐ Built CloudFormation template (ec2-nginx.yml)
⭐ Deployed NGINX server on EC2
⭐ Retrieved public URL & tested deployment
⭐ Cleaned up resources
