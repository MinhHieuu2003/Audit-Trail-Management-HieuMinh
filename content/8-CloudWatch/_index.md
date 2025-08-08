---
title : "Monitoring & Alerts with Amazon CloudWatch"
date :  2025-08-05
weight : 8 
chapter : false
pre : " <b> 8. </b> "
---
### Amazon CloudWatch
When the Lambda audit logs messages containing the keyword “Error”, CloudWatch will automatically count them, and if the threshold is exceeded, it will automatically send alerts via email/Slack.

1. Create Metric Filter

- Go to **CloudWatch Logs**
    + AWS Console → **CloudWatch** → on the left select Logs → Log groups.
![watch](/images/8.cloudwatch/001.png)
- Select the log group for **Lambda audit**
    + Click on `/aws/lambda/AuditLoggerDemo`.

- Create metric filter
    + Open the **Metric filters** tab → click **Create metric filter**.
    + In the **Filter pattern** box -> enter `ERROR`.

![watch](/images/8.cloudwatch/002.png)

- Set name & configure metric
    + **Filter name**: `AuditErrorFilter`
    + **Metric namespace**: `AuditDemo`
    + **Metric name**: `ErrorCount`
    + **Metric value**: 1
    + Click **Next** → Create **filter**.

![watch](/images/8.cloudwatch/003.png)

![watch](/images/8.cloudwatch/004.png)

2. Create Alarm

![watch](/images/8.cloudwatch/005.png)
- Go to CloudWatch Alarms
    + AWS Console → Services → **CloudWatch** → **Alarms** → **All alarms** → **Create alarm**.
- Select metric: choose the metric named `AuditErrorFilter`.

![watch](/images/8.cloudwatch/006.png)

- Configuration:
    + Statistic: Sum
    + Period: 5 minutes
    + Threshold type: Static
    + Whenever ErrorCount >= 5
    + For: 1 consecutive period
    + Click Next.
- Alarm Name:
    + **Alarm name**: `HighErrorAuditAlert`
    + Description: ...
    + Click Next.
- Configure actions:
    + Send notification to: 
    + Topic name: `AuditAlertsTopic`
    + Display name: `Audit Alerts`
    + Subscription protocol: `tranleminhhieu.it@gmail.com`  (Gmail).
    + Click Next -> **Create alarm**.

![watch](/images/8.cloudwatch/007.png)
![watch](/images/8.cloudwatch/009.png)

3. Test the Alarm

- Observe the status: when an error is triggered in Lambda, it will change from **OK** to **In alarm**.
- Check your email to receive the notification.

![watch](/images/8.cloudwatch/010.png)

![watch](/images/8.cloudwatch/011.png)

![watch](/images/8.cloudwatch/012.png)