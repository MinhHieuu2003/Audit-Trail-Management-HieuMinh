---
title : "Compliance Reporting with Athena"
date :  2025-08-03 
weight : 6 
chapter : false
pre : " <b> 6. </b> "
---

Aggregate and schedule reports from immutable audit logs stored in the S3 bucket `audit-demo-logs`.

![Clean](/images/6.clean/001.png)

### Amazon Athena

1. Prepare log data on S3

  + Logs have been written to the `audit-demo-logs` bucket in the `logs/` folder (see step 4).  
  + Ensure bucket versioning and Object Lock are still active, so data cannot be deleted/overwritten.

![Clean](/images/6.clean/002.png)

![Clean](/images/6.clean/003.png)

2. Create AWS Glue Crawler
![Clean](/images/6.clean/004.png)
  + AWS Console → **Glue** → **Crawlers** → **Add crawler**.
  + Name: `AuditLogsS3Crawler`.
  + Data store: select **S3**, enter path s3://audit-demo-logs/logs/.
  + IAM role: select (or create) `GlueCrawlerRole` with permissions:

JSON:
-   {
-     "Effect": "Allow",
-      "Action": ["s3:GetObject","s3:ListBucket"],
-     "Resource": ["arn:aws:s3:::audit-demo-logs","arn:aws:s3:::audit-demo-logs/logs/*"]
-   }

  + **Output** → **Database**: `audit_reports`, Table prefix: `audit_logs`.
  + **Schedule**: None (run on demand).
  + After creation, select **Run crawler** and wait for the status **Succeeded**.
![Clean](/images/6.clean/005.png)

![Clean](/images/6.clean/007.png)

![Clean](/images/6.clean/008.png)

![Clean](/images/6.clean/009.png)

3. Configure Amazon Athena

  + AWS Console → Athena.
  + Settings (top right) → Query result location: s3://audit-demo-query-results/.
  + In Query Editor, select the database `audit_reports`.
  + Check the table:

SELECT *
FROM "audit_reports"."audit_logsaudit_demo_logs"
LIMIT 5;

![Clean](/images/6.clean/010.png)

![Clean](/images/6.clean/011.png)

![Clean](/images/6.clean/014.png)

4. Verify results

- Go to S3 `audit-demo-query-results/Unsaved` -> Check the file

![Clean](/images/6.clean/012.png)

![Clean](/images/6.clean/013.png)