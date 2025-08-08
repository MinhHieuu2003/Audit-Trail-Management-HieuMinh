1. Create the source code (audit_logger.py)

+ import json
+ import boto3
+ from datetime import datetime

+ #Initialize QLDB client if needed
 #qldb_client = boto3.client('qldb')

 def handler(event, context):
    payload = {
        'user': event.get('user', 'anonymous'),
         'action': event.get('action', 'unknown'),
         'timestamp': event.get('timestamp', datetime.utcnow().isoformat())
     }
+    #Write to CloudWatch Logs
    print(json.dumps(payload))
    #Example of writing to QLDB:
    #qldb_client.send_command(LedgerName='AuditDemoLedger', Statement="INSERT INTO AuditLogs ?", Parameters=[{'IonBinary': payload}])
    return {'status': 'OK', 'payload': payload}

![Connect](/images/3.connect/004.png)
2. Packaging
**zip function.zip audit_logger.py**