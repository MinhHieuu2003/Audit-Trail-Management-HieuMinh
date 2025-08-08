---
title : "EC2"
date :  2025-08-02
weight : 2
chapter : false
pre : " <b> 2.2.2 </b> "
---

#### Tạo Launch EC2

1. Tại trang **EC2**.
  + Click **Launch instance**.

![VPC](/images/2.prerequisite/027.png)

2. Tại trang **Launch instance**.
  + Tại mục **Name** điền **AuditDemo-Server**.
  + Tại mục **AMI** chọn **Amazon Linux** quản ý gói với **yum**.
  + Tại mục **Instance type** chọn **t2.micro**
![VPC](/images/2.prerequisite/028.png)
  + Tại mục **Key pair** chọn **audit-demo-key**
  + Network settings: **VPC** = **AuditDemo-VPC**, **Subnet** = **AuditDemo-PublicSubnet**, **Security Group** = **AuditDemo-SG**.

![VPC](/images/2.prerequisite/029.png)

3. Bấm **Launch instance** và chờ trạng thái running.

![VPC](/images/2.prerequisite/030.png)



