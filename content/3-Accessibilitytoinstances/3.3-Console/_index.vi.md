---
title : "Triển khai Lambda qua AWS CLI hoặc Console"
date :  2025-08-03 
weight : 3
chapter : false
pre : " <b> 3.3. </b> "
---
#### Tạo một AWS Lambda Function
1. Via Console:
  + **AWS Console**: điều hướng đến **Lambda** → **Functions** → **Create function**.
  + Function name: **AuditLoggerDemo**
  + Runtime: **Python 3.9**
  + Architecture: **x86_64**
  + Permissions: Mở **Change default execution role** → Chọn **Use an existing role** -> **AuditLoggerLambdaRole**.
  + Nhấn **Create function**.
![Connect](/images/3.connect/005.png)

2. Tại trang function mới.
    + Code Source:
  + Chọn **Upload from** → **.zip file.**
  + Upload **file function.zip** (chứa audit_logger.py).
![Connect](/images/3.connect/006.png)
  + Deploy code.
![Connect](/images/3.connect/007.png)
3. Test event
  + Trong tab **Test**  
  + Đặt **Event name**: **TestLogin**
  + Dán JSON:
  {"user":"hocsinh1","action":"login","timestamp":"2025-07-27T12:00:00Z"}
  ![Connect](/images/3.connect/008.png)
4. Chạy thử Function
  + Với event **TestLogin** đã chọn, click Test.
  + Kết quả execution sẽ hiển thị phía dưới:
![Connect](/images/3.connect/009.png)

5. Cấu hình CloudWatch Logs Cấu hình CloudWatch Logs
    + Kiểm tra Log Group.
  + Console > CloudWatch > Logs > Log groups > **/aws/lambda/AuditLoggerDemo**.
  + Mỗi invocation sẽ tạo log stream mới.
    + Tạo Metric Filter (...)

![Connect](/images/3.connect/010.png)


Lambda function đã có IAM Role với quyền ghi Logs và (tùy chọn) QLDB.

Mỗi sự kiện mẫu hiển thị JSON payload trong CloudWatch Logs.

Test event chạy thành công và in payload đúng.

