---
title : "Create Security Groups"
date :  2025-07-28 
weight : 4
chapter : false
pre : " <b> 2.1.4 </b> "
---

#### Create Security Groups

In this step, we will create the security groups used for our instances. As you can see, these security groups do not need to open traditional ports for **SSH** (port **22**) or **Remote Desktop** (port **3389**).

#### Create a security group for the Linux instance in the public subnet

1. Go to the [VPC service management interface](https://console.aws.amazon.com/vpc)
  + Click **Security Group**.  
  + Click **Create security group**.

![SG](/images/2.prerequisite/019-createsg.png)
2. Click Create security group

3. In the **Security group name** field, enter **AuditDemo-SG**.
  + In the **Description** field, enter **AuditDemo**.
  + In the **VPC** field, select **AuditDemo-VPC**.

![SG](/images/2.prerequisite/023.png)

4. Set Inbound Rules:
  + SSH (TCP 22) source **My IP**.
  + HTTPS (TCP 443) source **0.0.0.0/0**

5. Outbound:
  + Keep the default All traffic
  + Click **Create security group**.
![SG](/images/2.prerequisite/024.png)
This completes the creation of the necessary security groups for EC2 instances and the VPC Endpoint.