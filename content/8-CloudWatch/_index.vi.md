---
title : "Monitoring & Alerts qua Amazon CloudWatch"
date :  2025-08-05
weight : 8 
chapter : false
pre : " <b> 8. </b> "
---
### Amazon CloudWatch
Khi Lambda audit log in ra các message chứa từ khoá “Error”, CloudWatch sẽ tự đếm, và nếu vượt ngưỡng sẽ tự động gửi cảnh báo qua email/Slack.

1. Tạo Metric Filter

- Vào **CloudWatch Logs**
    + AWS Console → **CloudWatch** → bên trái chọn Logs → Log groups.
![watch](/images/8.cloudwatch/001.png)
- Chọn log group của **Lambda audit**
    + Click vào `/aws/lambda/AuditLoggerDemo`.

- Tạo metric filter
    + Mở tab **Metric filters** → click **Create metric filter**.
    + Trong ô **Filter pattern** -> chọn `ERROR`.

![watch](/images/8.cloudwatch/002.png)

- Đặt tên & cấu hình metric
    + **Filter name**: `AuditErrorFilter`
    + **Metric namespace**: `AuditDemo`
    + **Metric name**: `ErrorCount`
    + **Metric value**: 1
    + Click **Next** → Create **filter**.

![watch](/images/8.cloudwatch/003.png)

![watch](/images/8.cloudwatch/004.png)

2. Tạo Alarm

![watch](/images/8.cloudwatch/005.png)
- Vào CloudWatch Alarms
    + AWS Console → Services → **CloudWatch** → **Alarms** → **All alarms** → **Create alarm**.
- Chọn metric: chọn metric có tên `AuditErrorFilter`.

![watch](/images/8.cloudwatch/006.png)

- Cấu hình:
    + Statistic: Sum
    + Period: 5 minutes
    + Threshold type: Static
    + Whenever ErrorCount >= 5
    + For: 1 consecutive period
    + Click Next.
- Tên Alarm:
    + **Alarm name**: `HighErrorAuditAlert`
    + Description: ...
    + Click Next.
- Cấu hình hành động:
    + Send notification to: 
    + Topic name: `AuditAlertsTopic`
    + Display name: `Audit Alerts`
    + Subscription protocol: `tranleminhhieu.it@gmail.com`  (Mail google).
    + Click Next -> **Create alarm**.

![watch](/images/8.cloudwatch/007.png)
![watch](/images/8.cloudwatch/009.png)

3. Kiểm thử Alarm

- Quan sát trạng thái khi gây lỗi ở Lambda nó sẽ báo từ trạng thái **OK** sang **In alarm**.
- Kiểm tra email để nhận được thông báo.

![watch](/images/8.cloudwatch/010.png)

![watch](/images/8.cloudwatch/011.png)

![watch](/images/8.cloudwatch/012.png)



