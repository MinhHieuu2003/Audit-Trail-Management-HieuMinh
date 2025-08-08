---
title : "Phân tích Trail với Amazon OpenSearch Service"
date :  2025-08-03 
weight : 5 
chapter : false
pre : " <b> 5. </b> "
---

Thu thập, lập chỉ mục và trực quan hoá các audit log để phục vụ phân tích và điều tra.

#### Amazon OpenSearch Service
![FWD](/images/5.fwd/001.png)
1. Tạo Domain OpenSearch
- AWS Console → **OpenSearch Service** → **Create domain**.

- Chọn **Deployment type**: Development and testing.

- Đặt **Domain name**: `audit-trail-demo`.

- Set capacity: 1 instance, loại `c7g.xlarge.search`.

- **Network configuration**:
  + VPC: `AuditDemo-VPC`
  + Subnet: `AuditDemo-PublicSubnet`
  (Vào Route tables -> Edit **subnet associations** -> click chọn cả 2 Subnets -> nhấn Save)
  + Security Group: `AuditDemo-SG`
  + Fine-grained access control: **Create master user** ( Hãy tự tạo username và password)
![FWD](/images/5.fwd/002.png)

![FWD](/images/5.fwd/003.png)
- **Access policy** (cho phép Lambda và bạn truy cập):

  {
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Principal": {
        "AWS": [
          "arn:aws:iam::<ACCOUNT_ID>:role/AuditLoggerLambdaRole",
          "arn:aws:iam::<ACCOUNT_ID>:user/<YourIAMUser>"
        ]
      },
      "Action": "es:*",
      "Resource": "arn:aws:es:<REGION>:<ACCOUNT_ID>:domain/audit-trail-demo/*"
    }
  ]
}


- Click **Create domain** và chờ trạng thái chuyển thành **Active**.

{{% notice info %}}
Em đã thử nhưng vẫn không biết tạo domain sao cho đúng.
{{% /notice %}}

2. Tại trang **Kinesis**. chọn **Create data stream**

  + Console → **Kinesis Data Firehose** → **Create Firehose stream**.
![FWD](/images/5.fwd/004.png)
  + Source: chọn **Amazon Kinesis Data Stream** `AuditStream` (hoặc Direct PUT nếu không dùng buffer).
  + Destination: **Amazon OpenSearch Service** → Domain `audit-trail-demo` → nhập Index name `audit-logs`.

{{% notice info %}}
Bước 1 phải hoàn thành.
{{% /notice %}}

![FWD](/images/5.fwd/005.png)

  + Role: chọn (hoặc tạo) IAM Role `FirehoseDeliveryRole` có quyền `es:ESHttpPost` và `s3:PutObject` (nếu bật backup).
  + (Tùy chọn) bật S3 backup để lưu bản sao log vào bucket như `audit-demo-backup`.
  + Click **Create delivery stream**.
- Kết nối CloudWatch Logs tới Firehose:
  + Console → **CloudWatch** → **Log groups** → chọn **/aws/lambda/AuditLoggerDemo** → Actions → **Stream to AWS service**.
  + Chọn **Kinesis Firehose** → chọn **stream AuditStream** → Save.
![FWD](/images/5.fwd/006.png)

3. Tạo Index Pattern & Visualizations trên OpenSearch Dashboards

- Mở **OpenSearch Dashboards** từ link trong OpenSearch Console.

- Vào **Stack Management** → **Index Patterns** → **Create index pattern**:

  + Index pattern: `audit-logs*`
  + Chọn trường timestamp (`timestamp` hoặc `@timestamp`) để filter theo thời gian.

- **Visualize Library** → **Create visualization**:

  + **Bar chart**: count của documents theo field action.
  + **Date histogram**: timeline events theo khung giờ.
  + **Data table**: top 10 users có nhiều events nhất (group by user).

- **Dashboard** → **Create dashboard** `Audit Trail Dashboard` → Add các visualization vừa tạo.
 

4. Kiểm thử & Xác minh

- Gửi một vài test events qua Lambda (bước 2) để sinh log.

- Chờ vài phút, Firehose sẽ đẩy dữ liệu vào OpenSearch.

- **Discover**: trên Dashboards, vào tab **Discover** để xem raw log.

- Dashboard: mở `Audit Trail Dashboard`, kiểm tra:
  + Biểu đồ bar chart hiển thị đúng số lượng events theo `action`.
  + Timeline hiển thị liên tục theo timestamp.
  + Data table liệt kê đúng top users.

![FWD](/images/5.fwd/007.png)

{{% notice info %}}
Làm hoàn thành các bước sẽ hiện thị kết quả.
{{% /notice %}}




