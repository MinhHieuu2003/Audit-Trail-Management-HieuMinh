---
title : "Clean Resources"
date :  2025-08-06
weight : 11
chapter : false
pre : " <b> 11. </b> "
---
### Clean Resources
Loại bỏ hết EC2, VPC, Lambda, S3, OpenSearch, Glue, Athena, Backup, CloudWatch, SNS, EventBridge… đã dùng trong demo.

1. Xóa EC2 & Networking
-   Terminate EC2 Instance
    + Vào AWS Console → EC2 → Instances.
    + Tích chọn AuditDemo-Server → Actions (ở trên) → Instance state → Terminate instance → xác nhận Terminate.


-   Xóa Key Pair
    + EC2 → Key Pairs (menu bên trái) → chọn audit-demo-key → Actions → Delete key pair → Delete.


-   Xóa VPC = xóa luôn mọi thứ thuộc về VPC đó
    + VPC → Your VPCs → chọn AuditDemo-VPC → Actions → Delete VPC → Delete.


2. Xóa S3 Buckets

- Empty & Delete bucket audit-demo-logs
    + AWS Console → S3 → Buckets → chọn audit-demo-logs.
    + Trên tab Overview, click Empty bucket → nhập tên bucket → Empty.
    + Sau khi xong, click Delete → nhập tên → Delete bucket.


- Empty & Delete bucket audit-demo-query-results
    + S3 → chọn bucket → Empty bucket → xác nhận → sau đó Delete.

3. Xóa Glue, Athena & Backup

- Xóa Glue crawler
    + AWS Console → AWS Glue → Crawlers → chọn AuditLogsS3Crawler → Action → Delete crawler → Delete.

- Xóa Glue database
    + Glue → Data Catalog → Databases → chọn audit_reports → Action → Delete database → Delete.

- Xóa Athena saved queries
    + AWS Console → Athena → chọn tab Saved queries → click tên query lưu DailyAuditReport → Actions → Delete query → Delete.

- Xóa AWS Backup plan & vault
    + AWS Console → AWS Backup → Backup plans → chọn AuditBackupPlan → Actions → Delete backup plan → Delete.
    + Backup → Backup vaults → chọn AuditBackupVault → Actions → Delete backup vault → Delete.


4. Xóa Lambda & IAM

- Xóa Lambda function
    + AWS Console → Lambda → Functions → chọn AuditLoggerDemo → Actions → Delete function → xác nhận Delete.

- Xóa IAM Role của Lambda
    + Console → IAM → Roles → tìm AuditLoggerLambdaRole → click vào role → tab Permissions → nếu có inline policy click Delete inline policy để xóa → trở lại trang role → Role actions → Delete role → xác nhận Delete.

- Xóa IAM Role của Glue Crawler
    + IAM → Roles → chọn AWSGlueServiceRole-AuditLogsS3Crawler → Role actions → Delete role → Delete.

- Xóa SNS topic
    + AWS Console → SNS → Topics → chọn AuditAlertsTopic → Actions → Delete topic → Delete.

- Xóa EventBridge rule
    + Console → EventBridge → Rules → chọn rule DailyAuditReportRule → Actions → Remove targets → tick target → Remove → rồi Actions → Delete rule → Delete.


5. Xóa OpenSearch Domain

- AWS Console → OpenSearch Service → Domains → chọn audit-trail-demo → Actions → Delete domain → nhập tên domain → Delete.

6. Xóa CloudWatch Resources

- Xóa Metric filter
    + CloudWatch → Logs → Log groups → chọn /aws/lambda/AuditLoggerDemo → tab Metric filters → chọn AuditErrorFilter → Actions → Delete filter.

- Xóa Alarm
    + CloudWatch → Alarms → All alarms → chọn HighErrorAuditAlert → Actions → Delete → xác nhận.

- Xóa Log group
    + CloudWatch → Logs → Log groups → chọn /aws/lambda/AuditLoggerDemo → Actions → Delete log group → Delete.

- Xóa QuickSight Artifacts
    + QuickSight → Dashboards → tích chọn Audit Trail Investigation → Delete → Delete.

    + QuickSight → Analyses → chọn AuditTrailInvestigation → Delete → Delete.

    + QuickSight → Datasets → chọn AuditLogsAthena → Delete → Delete.


### Cảm ơn vì đã xem tới đây.