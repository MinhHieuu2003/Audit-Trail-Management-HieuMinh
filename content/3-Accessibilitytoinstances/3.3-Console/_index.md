---
title : "Deploy Lambda via AWS CLI or Console"
date :  2025-08-03 
weight : 3
chapter : false
pre : " <b> 3.3. </b> "
---
#### Create an AWS Lambda Function
1. Via Console:
  + **AWS Console**: navigate to **Lambda** → **Functions** → **Create function**.
  + Function name: **AuditLoggerDemo**
  + Runtime: **Python 3.9**
  + Architecture: **x86_64**
  + Permissions: Open **Change default execution role** → Select **Use an existing role** -> **AuditLoggerLambdaRole**.
  + Click **Create function**.
![Connect](/images/3.connect/005.png)

2. On the new function page:
    + Code Source:
  + Select **Upload from** → **.zip file.**
  + Upload the **function.zip** file (containing audit_logger.py).
![Connect](/images/3.connect/006.png)
  + Deploy the code.
![Connect](/images/3.connect/007.png)
3. Test event
  + In the **Test** tab  
  + Set **Event name**: **TestLogin**
  + Paste the JSON:
  {"user":"hocsinh1","action":"login","timestamp":"2025-07-27T12:00:00Z"}
![Connect](/images/3.connect/008.png)
4. Run the Function
  + With the **TestLogin** event selected, click Test.
  + The execution result will be displayed below:
![Connect](/images/3.connect/009.png)

5. Configure CloudWatch Logs
    + Check the Log Group.
  + Console > CloudWatch > Logs > Log groups > **/aws/lambda/AuditLoggerDemo**.
  + Each invocation will create a new log stream.
    + Create Metric Filter (...)

![Connect](/images/3.connect/010.png)
