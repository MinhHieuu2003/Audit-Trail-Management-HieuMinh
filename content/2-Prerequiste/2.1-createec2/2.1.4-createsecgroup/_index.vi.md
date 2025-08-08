---
title : "Tạo các security group"
date :  2025-07-28
weight : 4
chapter : false
pre : " <b> 2.1.4 </b> "
---

#### Tạo các security group

Trong bước này chúng ta sẽ tiến hành tạo các security group được sử dụng cho các instance của chúng ta. Các bạn có thể thấy, các securiy group này sẽ không cần phải mở các port truyền thống để **ssh** như port **22** hoặc **remote desktop** thông qua port **3389**.

#### Tạo security group cho Linux instance nằm trong public subnet 

1. Truy cập [giao diện quản trị dịch vụ VPC](https://console.aws.amazon.com/vpc)
  + Click **Security Group**.  
  + Click **Create security group**.

![SG](/images/2.prerequisite/019-createsg.png)
2. Click Create security group

3. Tại mục **Security group name**, điền **`AuditDemo-SG`**. 
  + Tại mục **Description**, điền **`AuditDemo`**.
  + Tại mục **VPC**, **A`uditDemo-VPC`** .

![SG](/images/2.prerequisite/023.png)

4. Chọn Inbound Rules:
  + SSH (TCP 22) nguồn **My IP**.
  + HTTPS (TCP 443) nguồn **`0.0.0.0/0`**
![SG](/images/2.prerequisite/0241.png)
5. Outbound:
  + Giữ mặc định All traffic
   + Click **Create security group**.

![SG](/images/2.prerequisite/221.png)
Như vậy chúng ta đã tiến hành xong việc tạo các security group cần thiết cho các EC2 instance và VPC Endpoint.