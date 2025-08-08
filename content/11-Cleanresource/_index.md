---
title : "Clean Resources"
date :  2025-08-06
weight : 11
chapter : false
pre : " <b> 11. </b> "
---
### Clean Resources
Remove all EC2, VPC, Lambda, S3, OpenSearch, Glue, Athena, Backup, CloudWatch, SNS, EventBridge, etc. used in the demo.

1. Delete EC2 & Networking
-   Terminate EC2 Instance
    + Go to AWS Console → EC2 → Instances.
    + Select AuditDemo-Server → Actions (at the top) → Instance state → Terminate instance → confirm Terminate.

-   Delete Key Pair
    + EC2 → Key Pairs (left menu) → select audit-demo-key → Actions → Delete key pair → Delete.

-   Delete VPC = delete everything belonging to that VPC
    + VPC → Your VPCs → select AuditDemo-VPC → Actions → Delete VPC → Delete.

2. Delete S3 Buckets

- Empty & Delete bucket audit-demo-logs
    + AWS Console → S3 → Buckets → select audit-demo-logs.
    + On the Overview tab, click Empty bucket → enter bucket name → Empty.
    + After that, click Delete → enter name → Delete bucket.

- Empty & Delete bucket audit-demo-query-results
    + S3 → select bucket → Empty bucket → confirm → then Delete.

3. Delete Glue, Athena & Backup

- Delete Glue crawler
    + AWS Console → AWS Glue → Crawlers → select AuditLogsS3Crawler → Action → Delete crawler → Delete.

- Delete Glue database
    + Glue → Data Catalog → Databases → select audit_reports → Action → Delete database → Delete.

- Delete Athena saved queries
    + AWS Console → Athena → select Saved queries tab → click saved query name DailyAuditReport → Actions → Delete query → Delete.

- Delete AWS Backup plan & vault
    + AWS Console → AWS Backup → Backup plans → select AuditBackupPlan → Actions → Delete backup plan → Delete.
    + Backup → Backup vaults → select AuditBackupVault → Actions → Delete backup vault → Delete.

4. Delete Lambda & IAM

- Delete Lambda function
    + AWS Console → Lambda → Functions → select AuditLoggerDemo → Actions → Delete function → confirm Delete.

- Delete IAM Role for Lambda
    + Console → IAM → Roles → find AuditLoggerLambdaRole → click the role → Permissions tab → if there is an inline policy click Delete inline policy to remove → back to role page → Role actions → Delete role → confirm Delete.

- Delete IAM Role for Glue Crawler
    + IAM → Roles → select AWSGlueServiceRole-AuditLogsS3Crawler → Role actions → Delete role → Delete.

- Delete SNS topic
    + AWS Console → SNS → Topics → select AuditAlertsTopic → Actions → Delete topic → Delete.

- Delete EventBridge rule
    + Console → EventBridge → Rules → select rule DailyAuditReportRule → Actions → Remove targets → tick target → Remove → then Actions → Delete rule → Delete.

5. Delete OpenSearch Domain

- AWS Console → OpenSearch Service → Domains → select audit-trail-demo → Actions → Delete domain → enter domain name → Delete.

6. Delete CloudWatch Resources

- Delete Metric filter
    + CloudWatch → Logs → Log groups → select /aws/lambda/AuditLoggerDemo → Metric filters tab → select AuditErrorFilter → Actions → Delete filter.

- Delete Alarm
    + CloudWatch → Alarms → All alarms → select HighErrorAuditAlert → Actions → Delete → confirm.

- Delete Log group
    + CloudWatch → Logs → Log groups → select /aws/lambda/AuditLoggerDemo → Actions → Delete log group → Delete.

- Delete QuickSight Artifacts
    + QuickSight → Dashboards → select Audit Trail Investigation → Delete → Delete.

    + QuickSight → Analyses → select AuditTrailInvestigation → Delete → Delete.

    + QuickSight → Datasets → select AuditLogsAthena → Delete → Delete.

### Thank you for watching.