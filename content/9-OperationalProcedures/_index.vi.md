---
title : "Operational Procedures"
date :  2025-08-05
weight : 9 
chapter : false
pre : " <b> 9. </b> "
---
### Operational Procedures
Bảo đảm log của bạn được giữ đúng thời hạn (retention), có bản sao dự phòng (backup) và có quy trình xử lý khi có sự cố (SOP).

1. Cấu hình Log Retention

- Vào **CloudWatch Logs**
    + AWS Console → **CloudWatch** → bên trái chọn Logs → Log groups.
![opera](/images/9.op/001.png)
   + Chọn log group của **Lambda audit**
   + Click vào `/aws/lambda/AuditLoggerDemo`.
    +  Click **Actions** → **Edit retention**.
    +  Tuỳ chọn ( ở đây em chọn 7 day) → **Save**.


- S3 Object Lock
    + AWS Console → **S3** → click vào bucket `audit-demo-logs`.
    + Sang tab **Properties** → kéo xuống **Object lock** → click **Edit**
    + Chọn Retention mode = Compliance (bất biến), Retention period = 10 days → Save.

![opera](/images/9.op/002.png)

2. Backup & Recovery
-   Tạo Backup vault
    + Console: AWS Backup → **Backup vaults** → **Create backup vault** → Name = `AuditBackupVault`.
![opera](/images/9.op/003.png)

- Tạo Backup plan
    + Console → **AWS Backup** → **Backup plans** → **Create backup plan** → **Build a new plan**.
    + Plan name: `AuditBackupPlan`
    + Frequency: Daily at 00:00
    + Retention: 7 days
    + Click **Create plan**.
![opera](/images/9.op/004.png)
![opera](/images/9.op/005.png)
![opera](/images/9.op/006.png)

- Gán resource cho plan
    +  Console: Chọn `AuditBackupPlan` → **Assign resources** → **Resource type** = **S3** → ARN = `arn:aws:s3:::audit-demo-logs` → Assign.

![opera](/images/9.op/007.png)
![opera](/images/9.op/008.png)

3. SOP xử lý sự cố
- Proof dữ liệu (S3 Object Lock)
    + Dùng CLI liệt kê version:

    aws s3api list-object-versions \
  --bucket audit-demo-logs \
  --prefix logs/

- Kiểm tra xem có version nào bị xóa hay overwritten trái phép không.
![opera](/images/9.op/009.png)

- Rebuild dashboard QuickSight

- QuickSight → **Datasets** → chọn `AuditLogsAthena` → click **Refresh** → chờ SPICE import → **Visualize** để dashboard cập nhật dữ liệu mới.

Với bước này, chúng ta đã thiết lập được retention, backup/recovery và quy trình xử lý sự cố cho hệ thống audit, đảm bảo nó luôn an toàn, có thể phục hồi và vận hành suôn sẻ.


