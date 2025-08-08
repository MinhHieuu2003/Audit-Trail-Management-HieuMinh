---
title : "IAM Role cho Lambda"
date :  2025-08-03 
weight : 1 
chapter : false
pre : " <b> 3.1. </b> "
---
#### Tạo IMA Role
1. Truy cập vào [giao diện quản trị của dịch vụ IMA Role](https://us-east-1.console.aws.amazon.com/iam/home?region=ap-southeast-1#/roles/create).

  B1 Click chọn **AWS service**.
  + Click chọn **Lambda**.
  + Click **Next**.

  B2 Điền **AWSLambdaBasicExecutionRole** rồi tick chọn.
  + Custom policy cho phép **qldb:SendCommand** và **qldb:InsertDocument** (nếu ghi trực tiếp vào QLDB).

  B3 Đặt tên role: **AuditLoggerLambdaRole**

![Connect](/images/3.connect/001.png)

![Connect](/images/3.connect/002.png)

![Connect](/images/3.connect/003.png)




