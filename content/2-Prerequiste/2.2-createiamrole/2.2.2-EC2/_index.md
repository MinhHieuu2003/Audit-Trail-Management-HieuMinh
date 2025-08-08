---
title : "EC2"
date :  2025-08-02
weight : 2
chapter : false
pre : " <b> 2.2.2 </b> "
---

#### Launch EC2

1. On the **EC2** page:
  + Click **Launch instance**.

![VPC](/images/2.prerequisite/027.png)

2. On the **Launch instance** page:
  + In the **Name** field, enter **AuditDemo-Server**.
  + For **AMI**, select **Amazon Linux** (managed with **yum**).
  + For **Instance type**, choose **t2.micro**.
![VPC](/images/2.prerequisite/028.png)
  + For **Key pair**, select **audit-demo-key**.
  + Network settings: **VPC** = **AuditDemo-VPC**, **Subnet** = **AuditDemo-PublicSubnet**, **Security Group** = **AuditDemo-SG**.

![VPC](/images/2.prerequisite/029.png)

3. Click **Launch instance** and wait until the status is