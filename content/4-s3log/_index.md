---
title : "Implementing Immutable Logging with (AWS S3)"
date :  2025-08-03 
weight : 4 
chapter : false
pre : " <b> 4. </b> "
---

### Implementing Immutable Logging
Use S3 with Object Lock and Versioning support, suitable for projects.

1. S3 Bucket
- Console → S3 → Create bucket  
  • **Bucket name**: `audit-demo-logs`  
  • **Region**: ap-southeast-1  
  • Enable **Bucket Versioning**.  
  • Check **Enable Object Lock** before creating the bucket.  
- Click **Create bucket** and wait for completion.
![S3](/images/4.s3/001.png)

![S3](/images/4.s3/002.png)

2. Configure Default Retention
 
- Go to bucket `audit-demo-logs` → **Properties** → **Object Lock** → **Edit**  
  • Select **Default retention**: Mode = **Compliance**, Retention period = **365 days** (or shorter for demo, e.g. 7 days)  
- Save changes.
![S3](/images/4.s3/003.png)

3. IAM Policy for S3 Write
  Create a JSON policy and attach it to the role `AuditLoggerLambdaRole`:

{
  "Version":"2012-10-17",
  "Statement":[
    {
      "Effect":"Allow",
      "Action":[
        "s3:PutObject",
        "s3:ListBucket",
        "s3:GetObject"
      ],
      "Resource":[
        "arn:aws:s3:::audit-demo-logs",
        "arn:aws:s3:::audit-demo-logs/*"
      ]
    }
  ]
}
 
![S3](/images/4.s3/004.png)
 
4. Write Audit Log to S3 from Lambda

- The Lambda role (**AuditLoggerLambdaRole**) must have the appropriate policy:

+ In AWS Console → Lambda → AuditLoggerDemo → Configuration → Environment variables → Edit:
+ Key: **BUCKET_NAME** = Value: `audit-demo-logs`
+ Key: **LOG_PREFIX** = Value: `logs/` (optional, to group logs by folder)
+ Deploy 
![S3](/images/4.s3/005.png)

5. Testing & Verification

![S3](/images/4.s3/006.png)

![S3](/images/4.s3/007.png)

![S3](/images/4.s3/008.png)