---
title : "Compliance Reporting với Athena"
date :  2025-08-03 
weight : 6 
chapter : false
pre : " <b> 6. </b> "
---

Tổng hợp và lên lịch báo cáo từ audit logs đã lưu bất biến trong S3 bucket `audit-demo-logs`.

![Clean](/images/6.clean/001.png)

### Amazon Athena

1. Chuẩn bị dữ liệu log trên S3

  + Logs đã được ghi vào bucket `audit-demo-logs` trong folder `logs/` (tại 4).  
  + Đảm bảo bucket versioning và Object Lock vẫn active, nên dữ liệu không thể bị xóa/ghi đè.

![Clean](/images/6.clean/002.png)

![Clean](/images/6.clean/003.png)

2. Tạo AWS Glue Crawler
![Clean](/images/6.clean/004.png)
  + AWS Console → **Glue** → **Crawlers** → **Add crawler**.
  + Name: `AuditLogsS3Crawler`.
  + Data store: chọn **S3**, nhập path 1s3://audit-demo-logs/logs/1.
  + IAM role: chọn (hoặc tạo) `GlueCrawlerRole` có quyền:

JSON:
-   {
-     "Effect": "Allow",
-      "Action": ["s3:GetObject","s3:ListBucket"],
-     "Resource": ["arn:aws:s3:::audit-demo-logs","arn:aws:s3:::audit-demo-logs/logs/*"]
-   }

  + **Output** → **Database**: `audit_reports`, Table prefix: `audit_logs`.
  + **Schedule**: None (run on demand).
  + Tạo xong, chọn **Run crawler** và đợi trạng thái **Succeeded**.
![Clean](/images/6.clean/005.png)

![Clean](/images/6.clean/007.png)

![Clean](/images/6.clean/008.png)

![Clean](/images/6.clean/009.png)

3. Cấu hình Amazon Athena

  + AWS Console → Athena.
  + Settings (góc phải) → Query result location: s3://audit-demo-query-results/.
  + Trong Query Editor, chọn database audit_reports.
  + Kiểm tra table:

SELECT *
FROM "audit_reports"."audit_logsaudit_demo_logs"
LIMIT 5;

![Clean](/images/6.clean/010.png)

![Clean](/images/6.clean/011.png)

![Clean](/images/6.clean/014.png)

4. Xác nhận kết quả

- Vào S3 `audit-demo-query-results/Unsaved` -> Kiểm tra file

![Clean](/images/6.clean/012.png)

![Clean](/images/6.clean/013.png)







