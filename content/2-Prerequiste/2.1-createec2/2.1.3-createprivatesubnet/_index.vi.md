---
title : "Tạo Internet Gateway & Route Table"
date :  2025-07-28 
weight : 3
chapter : false
pre : " <b> 2.1.3 </b> "
---

#### Tạo Private subnet

1. Click **Internet Gateways**.

![VPC](/images/2.prerequisite/017.png)

2. Cấu hình **Internet Gateways**.
  + Tại Name tag, nhập `AuditDemo-IGW`.
  + Click Create internet gateway.

- Xác nhận tạo Internet Gateway thành công
![VPC](/images/2.prerequisite/018.png)

3. Xác nhận tạo Internet Gateway thành công

Kết nối với VPC
4. Gắn Internet Gateway vào VPC
  + Click Actions
  + Chọn Attach to `AuditDemo-VPC`.
  + Chọn VPC ASG từ danh sách (VPC ID sẽ tự động điền)
  + Click Attach internet gateway
![VPC](/images/2.prerequisite/019.png)

![VPC](/images/2.prerequisite/0191.png)

#### Tạo Route tables

Tạo Route Table trong Amazon VPC
1. Truy cập giao diện VPC
  + Chọn Route Tables từ menu bên trái
  + Click vào Create route table
![VPC](/images/2.prerequisite/020.png)

2. Cấu hình Route Table
  + Name: `AuditDemo-RT`.
  + VPC: `AuditDemo-VPC`.
  + Click Create route table.
![VPC](/images/2.prerequisite/021.png)

3. Trong Route Table 
  + Chọn Edit Routes → Add route.
  + Destination: `0.0.0.0/0*`
  + Target: **Internet Gateway** -> `igw-(AuditDemo-IGW)`
  + Click Save routes.
![VPC](/images/2.prerequisite/022.png)

![VPC](/images/2.prerequisite/0221.png)