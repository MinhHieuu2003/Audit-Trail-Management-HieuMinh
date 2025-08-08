---
title : "Triển khai Immutable Logging với (AWS S3)"
date :  2025-08-03 
weight : 4 
chapter : false
pre : " <b> 4. </b> "
---

### Triển khai Immutable Logging
Sử dụng S3 có hỗ trợ Object Lock và Versioning, phù hợp cho đồ án.

1. S3 Bucket
- Console → S3 → Create bucket  
  • **Bucket name**: `audit-demo-logs`  
  • **Region**: ap-southeast-1  
  • Bật **Bucket Versioning**.  
  • Tích vào **Enable Object Lock** trước khi tạo bucket.  
- Nhấn **Create bucket** và chờ hoàn tất.
![S3](/images/4.s3/001.png)

![S3](/images/4.s3/002.png)

2. Cấu hình Default Retention
 
- Vào bucket `audit-demo-logs` → **Properties** → **Object Lock** → **Edit**  
  • Chọn **Default retention**: Mode = **Compliance**, Retention period = **365 days** (hoặc ngắn hơn cho demo, ví dụ 7 days)  
- Save changes.
![S3](/images/4.s3/003.png)

3. IAM Policy cho S3 Write
  Tạo policy JSON và gắn vào role `AuditLoggerLambdaRole`:

{
  "Version":"2012-10-17",
  "Statement":[
    {
      "Effect":"Allow",
      "Action":[
        "s3:PutObject",
        "s3:ListBucket",
        "s3:GetObject"
      ],
      "Resource":[
        "arn:aws:s3:::audit-demo-logs",
        "arn:aws:s3:::audit-demo-logs/*"
      ]
    }
  ]
}
 
![S3](/images/4.s3/004.png)
 
4. Ghi Audit Log vào S3 từ Lambda

- Role của Lambda (**AuditLoggerLambdaRole**) phải có policy cho phép:

+ Trong AWS Console → Lambda → AuditLoggerDemo → Configuration → Environment variables → Edit:
+ Key: **BUCKET_NAME** = Value: `audit-demo-logs`
+ Key: **LOG_PREFIX** = Value: `logs/` (tuỳ chọn, để gom log theo folder)
+ Deploy 
![S3](/images/4.s3/005.png)

5. Kiểm thử & xác minh

![S3](/images/4.s3/006.png)

![S3](/images/4.s3/007.png)

![S3](/images/4.s3/008.png)



