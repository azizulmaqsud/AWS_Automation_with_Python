# AWS End-to-End Automation Project (Python boto3 + AWS Console + CLI)

A complete beginner-friendly DevOps project integrating multiple AWS services using:

✔ AWS Console

✔ AWS CLI

✔ Python SDK (boto3)

This is a hands-on project for new DevOps Engineers who want to build real AWS automation skills.

________________________________________
🏗 Architecture

Use your generated image:

➡ /architecture/architecture-diagram.png

________________________________________
🚀 Project Features 

✅ DynamoDB CRUD Operations

Create, Read, Update, Delete items using Python boto3.

✅ SNS Email Notifications

Send automated notification emails.

✅ SQS Queue Automation

Send and receive messages programmatically.

✅ ECS Deployment

Deploy a container image into an ECS cluster using Python.

✅ EKS Automation

Fetch kubeconfig for your EKS cluster using boto3.

✅ IAM Setup

Create IAM user, access keys, and permissions.

________________________________________
🧩 Prerequisites

•	AWS Account

•	Admin IAM user

•	Python3 + pip

•	AWS CLI

•	Docker (for ECS)

•	kubectl + eksctl (for EKS)

________________________________________
🛠 Setup Steps (Easy — For New DevOps Engineers)
________________________________________

1️⃣ Configure AWS CLI

aws configure
________________________________________

2️⃣ Create IAM User (Script)

iam_setup/iam_user_setup.sh

aws iam create-user --user-name devops-user

aws iam attach-user-policy --user-name devops-user \

  --policy-arn arn:aws:iam::aws:policy/AdministratorAccess
  
aws iam create-access-key --user-name devops-user

________________________________________
3️⃣ Run DynamoDB CRUD

python3 dynamodb_crud/dynamodb_crud.py

________________________________________
4️⃣ Send SNS Email

python3 sns_notifications/send_email.py

________________________________________
5️⃣ Send SQS Message

python3 sqs_automation/send_message.py

python3 sqs_automation/receive_message.py

________________________________________
6️⃣ Deploy ECS Service

python3 ecs_deployment/deploy_ecs_service.py

________________________________________
7️⃣ Fetch EKS Kubeconfig

python3 eks_kubeconfig/fetch_kubeconfig.py

________________________________________
📌 Code Files 
________________________________________

🗄 DynamoDB CRUD — dynamodb_crud.py

import boto3

table_name = "DevOpsItems"

dynamodb = boto3.resource('dynamodb')

table = dynamodb.Table(table_name)

# CREATE

table.put_item(Item={"id": "1", "name": "DevOps Tool", "value": "Terraform"})

print("Item inserted.")

# READ

response = table.get_item(Key={"id": "1"})

print("Read:", response.get("Item"))

# UPDATE

table.update_item(

    Key={"id": "1"},
    
    UpdateExpression="SET value=:v",
    
    ExpressionAttributeValues={":v": "Ansible"}

)

print("Item updated.")

# DELETE

table.delete_item(Key={"id": "1"})

print("Item deleted.")

________________________________________
✉️ SNS Email — send_email.py

import boto3

sns = boto3.client("sns")

sns.publish(

    TopicArn="arn:aws:sns:us-east-1:YOUR_ID:DevOpsTopic",
    
    Subject="DevOps Notification",
    
    Message="DynamoDB task completed successfully!"
    
)

print("Email Sent!")

________________________________________
📬 SQS — Send Message send_message.py

import boto3

sqs = boto3.client("sqs")

queue_url = "https://sqs.us-east-1.amazonaws.com/YOUR_ID/DevOpsQueue"

sqs.send_message(

    QueueUrl=queue_url,
    
    MessageBody="Hello from DevOps!"
    
)

print("Message sent.")
________________________________________
📥 SQS — Receive Message receive_message.py

import boto3

sqs = boto3.client("sqs")

queue_url = "https://sqs.us-east-1.amazonaws.com/YOUR_ID/DevOpsQueue"

messages = sqs.receive_message(QueueUrl=queue_url)

print(messages)
________________________________________
🐳 ECS Deployment — deploy_ecs_service.py

import boto3

ecs = boto3.client('ecs')

response = ecs.update_service(

    cluster="DevOpsCluster",
    
    service="DevOpsService",
    
    forceNewDeployment=True
    
)

print("ECS Deployment Triggered")

________________________________________
☸️ EKS Kubeconfig — fetch_kubeconfig.py

import boto3

import subprocess

eks = boto3.client('eks')

cluster_name = "DevOpsEKS"

subprocess.run([

    "aws", "eks", "--region", "us-east-1",
    
    "update-kubeconfig", "--name", cluster_name
    
])

print("Kubeconfig fetched successfully.")

________________________________________
# 🎯 Tips to Newbies:

## This project is extracted from my Realtime job experiences, and its 100% production-ready & interview-friendly…
- Please try to do hands-on more than MORE! 

## Thank YOU!!

