---
title : "Analyze Trail with Amazon OpenSearch Service"
date :  2025-08-03 
weight : 5 
chapter : false
pre : " <b> 5. </b> "
---

Collect, index, and visualize audit logs for analysis and investigation.

#### Amazon OpenSearch Service
![FWD](/images/5.fwd/001.png)
1. Create OpenSearch Domain
- AWS Console → **OpenSearch Service** → **Create domain**.

- Select **Deployment type**: Development and testing.

- Set **Domain name**: `audit-trail-demo`.

- Set capacity: 1 instance, type `c7g.xlarge.search`.

- **Network configuration**:
  + VPC: `AuditDemo-VPC`
  + Subnet: `AuditDemo-PublicSubnet`
  (Go to Route tables -> Edit **subnet associations** -> select both Subnets -> click Save)
  + Security Group: `AuditDemo-SG`
  + Fine-grained access control: **Create master user** (Create your own username and password)
![FWD](/images/5.fwd/002.png)

![FWD](/images/5.fwd/003.png)
- **Access policy** (allow Lambda and you to access):

  {
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Principal": {
        "AWS": [
          "arn:aws:iam::<ACCOUNT_ID>:role/AuditLoggerLambdaRole",
          "arn:aws:iam::<ACCOUNT_ID>:user/<YourIAMUser>"
        ]
      },
      "Action": "es:*",
      "Resource": "arn:aws:es:<REGION>:<ACCOUNT_ID>:domain/audit-trail-demo/*"
    }
  ]
}

- Click **Create domain** and wait for the status to become **Active**.

{{% notice info %}}
I tried but still don't know how to create the domain correctly.
{{% /notice %}}

2. On the **Kinesis** page, select **Create data stream**

  + Console → **Kinesis Data Firehose** → **Create Firehose stream**.
![FWD](/images/5.fwd/004.png)
  + Source: select **Amazon Kinesis Data Stream** `AuditStream` (or Direct PUT if not using buffer).
  + Destination: **Amazon OpenSearch Service** → Domain `audit-trail-demo` → enter Index name `audit-logs`.

{{% notice info %}}
Step 1 must be completed.
{{% /notice %}}

![FWD](/images/5.fwd/005.png)

  + Role: select (or create) IAM Role `FirehoseDeliveryRole` with `es:ESHttpPost` and `s3:PutObject` permissions (if backup is enabled).
  + (Optional) enable S3 backup to save a copy of logs to a bucket like `audit-demo-backup`.
  + Click **Create delivery stream**.
- Connect CloudWatch Logs to Firehose:
  + Console → **CloudWatch** → **Log groups** → select **/aws/lambda/AuditLoggerDemo** → Actions → **Stream to AWS service**.
  + Select **Kinesis Firehose** → select **stream AuditStream** → Save.
![FWD](/images/5.fwd/006.png)

3. Create Index Pattern & Visualizations on OpenSearch Dashboards

- Open **OpenSearch Dashboards** from the link in the OpenSearch Console.

- Go to **Stack Management** → **Index Patterns** → **Create index pattern**:

  + Index pattern: `audit-logs*`
  + Select the timestamp field (`timestamp` or `@timestamp`) to filter by time.

- **Visualize Library** → **Create visualization**:

  + **Bar chart**: count of documents by action field.
  + **Date histogram**: timeline of events by time frame.
  + **Data table**: top 10 users with the most events (group by user).

- **Dashboard** → **Create dashboard** `Audit Trail Dashboard` → Add the visualizations you just created.
 

4. Test & Verify

- Send some test events via Lambda (step 2) to generate logs.

- Wait a few minutes, Firehose will push data to OpenSearch.

- **Discover**: on Dashboards, go to the **Discover** tab to view raw logs.

- Dashboard: open `Audit Trail Dashboard`, check:
  + Bar chart displays the correct number of events by `action`.
  + Timeline displays continuously by timestamp.
  + Data table correctly lists the top users.

![FWD](/images/5.fwd/007.png)

{{% notice info %}}
Completing all steps will display the results.
{{% /notice %}}