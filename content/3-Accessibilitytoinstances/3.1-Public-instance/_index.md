---
title : "IAM Role for Lambda"
date :  2025-08-03 
weight : 1 
chapter : false
pre : " <b> 3.1. </b> "
---
#### Create IAM Role
1. Go to the [IAM Role management interface](https://us-east-1.console.aws.amazon.com/iam/home?region=ap-southeast-1#/roles/create).

  Step 1: Select **AWS service**.
  + Select **Lambda**.
  + Click **Next**.

  Step 2: Enter **AWSLambdaBasicExecutionRole** and check it.
  + Add a custom policy to allow **qldb:SendCommand** and **qldb:InsertDocument** (if writing directly to QLDB).

  Step 3: Name the role: **AuditLoggerLambdaRole**

![Connect](/images/3.connect/001.png)

![Connect](/images/3.connect/002.png)

![Connect](/images/3.connect/003.png)