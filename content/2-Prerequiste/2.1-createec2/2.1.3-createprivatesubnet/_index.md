---
title : "Create Internet Gateway & Route Table"
date :  2025-07-28 
weight : 3
chapter : false
pre : " <b> 2.1.3 </b> "
---

#### Create Private Subnet

1. Click **Internet Gateways**.

![VPC](/images/2.prerequisite/017.png)

2. Configure **Internet Gateways**.
  + In the Name tag, enter **AuditDemo-IGW**.
  + Click Create internet gateway.

Confirm successful creation of Internet Gateway
![VPC](/images/2.prerequisite/018.png)

3. Confirm successful creation of Internet Gateway

Connect to VPC  
4. Attach Internet Gateway to VPC
  + Click Actions
  + Select Attach to **AuditDemo-VPC**
  + Select VPC ASG from the list (VPC ID will be filled automatically)
  + Click Attach internet gateway
![VPC](/images/2.prerequisite/019.png)

#### Create Route Tables

Create Route Table in Amazon VPC  
1. Go to the VPC interface
  + Select Route Tables from the left menu
  + Click Create route table
![VPC](/images/2.prerequisite/020.png)

2. Configure Route Table
  + Name: **AuditDemo-RT**
  + VPC: **AuditDemo-VPC**
  + Click Create route table
![VPC](/images/2.prerequisite/021.png)

3. In the Route Table
  + Click Edit Routes → Add route
  + Destination: **0.0.0.0/0**
  + Target: **Internet Gateway** -> igw-**(AuditDemo-IGW)**
  + Click Save routes
![VPC](/images/2.prerequisite/022.png)