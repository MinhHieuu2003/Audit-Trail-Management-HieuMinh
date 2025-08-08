---
title : "Operational Procedures"
date :  2025-08-05
weight : 9 
chapter : false
pre : " <b> 9. </b> "
---
### Operational Procedures
Ensure your logs are kept for the correct retention period, have backup copies, and have a standard operating procedure (SOP) for incident response.

1. Configure Log Retention

- Go to **CloudWatch Logs**
    + AWS Console → **CloudWatch** → on the left select Logs → Log groups.
![opera](/images/9.op/001.png)
   + Select the log group for **Lambda audit**
   + Click on `/aws/lambda/AuditLoggerDemo`.
    +  Click **Actions** → **Edit retention**.
    +  Choose the retention period (here, select 7 days) → **Save**.

- S3 Object Lock
    + AWS Console → **S3** → click on the `audit-demo-logs` bucket.
    + Go to the **Properties** tab → scroll down to **Object lock** → click **Edit**
    + Set Retention mode = Compliance (immutable), Retention period = 10 days → Save.

![opera](/images/9.op/002.png)

2. Backup & Recovery
-   Create Backup vault
    + Console: AWS Backup → **Backup vaults** → **Create backup vault** → Name = `AuditBackupVault`.
![opera](/images/9.op/003.png)

- Create Backup plan
    + Console → **AWS Backup** → **Backup plans** → **Create backup plan** → **Build a new plan**.
    + Plan name: `AuditBackupPlan`
    + Frequency: Daily at 00:00
    + Retention: 7 days
    + Click **Create plan**.
![opera](/images/9.op/004.png)
![opera](/images/9.op/005.png)
![opera](/images/9.op/006.png)

- Assign resource to plan
    +  Console: Select `AuditBackupPlan` → **Assign resources** → **Resource type** = **S3** → ARN = `arn:aws:s3:::audit-demo-logs` → Assign.

![opera](/images/9.op/007.png)
![opera](/images/9.op/008.png)

3. Incident Response SOP
- Proof of data (S3 Object Lock)
    + Use CLI to list versions:

    aws s3api list-object-versions \
  --bucket audit-demo-logs \
  --prefix logs/

- Check if any version has been deleted or overwritten without authorization.
![opera](/images/9.op/009.png)

- Rebuild QuickSight dashboard

- QuickSight → **Datasets** → select `AuditLogsAthena` → click **Refresh** → wait for SPICE import → **Visualize** to update the dashboard with new data.

With these steps, we have set up retention, backup/recovery, and incident response procedures for the audit system, ensuring it is always safe, recoverable, and operates smoothly.