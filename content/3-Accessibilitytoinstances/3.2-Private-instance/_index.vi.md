---
title : "Viết và đóng gói Lambda Function"
date :  2025-08-03 
weight : 2 
chapter : false
pre : " <b> 3.2. </b> "
---

#### Lambda Function

1. Tạo mã nguồn(audit_logger.py)

+ import json
+ import boto3
+ from datetime import datetime

+ #Khởi client QLDB nếu cần
 #qldb_client = boto3.client('qldb')

 def handler(event, context):
    payload = {
        'user': event.get('user', 'anonymous'),
         'action': event.get('action', 'unknown'),
         'timestamp': event.get('timestamp', datetime.utcnow().isoformat())
     }
+    #Ghi vào CloudWatch Logs
    print(json.dumps(payload))
    #Ví dụ ghi vào QLDB:
    #qldb_client.send_command(LedgerName='AuditDemoLedger', Statement="INSERT INTO AuditLogs ?", Parameters=[{'IonBinary': payload}])
    return {'status': 'OK', 'payload': payload}

![Connect](/images/3.connect/004.png)
2. Đóng gói
**zip function.zip audit_logger.py**

