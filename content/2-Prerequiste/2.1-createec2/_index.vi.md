---
title : "Tạo VPC và các thành phần mạng"
date :  2025-07-28
weight : 1 
chapter : false
pre : " <b> 2.1 </b> "
---
### Chuẩn bị AWS Free Tier Account
Đăng ký tại https://aws.amazon.com/free, xác thực thông tin thẻ tín dụng.

Đăng nhập Console, chọn Region (ví dụ: Asia Pacific (Singapore) ap-southeast-1) để giảm độ trễ.

Tổng quan kiến trúc sau khi các bạn hoàn tất bước này sẽ như sau:

![VPC](/images/arc-01.png)

Để tìm hiểu cách tạo các VPC với public/private subnet các bạn có thể tham khảo bài lab :
  - [Làm việc với Amazon VPC](https://000003.awsstudygroup.com/vi/) 



### Nội dung
  - [Tạo VPC](2.1.1-createvpc/)
  - [Tạo Public subnet](2.1.2-createpublicsubnet/)
  - [Tạo Private subnet](2.1.3-createprivatesubnet/)
  - [Tạo security group](2.1.4-createsecgroup/)
  - [Tạo máy chủ Linux public](2.1.5-createec2linux/)
  - [Tạo máy chủ Windows private](2.1.6-createec2windows/)
