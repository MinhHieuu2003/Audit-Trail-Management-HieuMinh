---
title : "Legal Coordination with AWS Artifact"
date :  2025-08-06
weight : 10 
chapter : false
pre : " <b> 10. </b> "
---
### AWS Artifact
Collect compliance reports (such as SOC 2, ISO 27001, GDPR) from AWS Artifact to compare and demonstrate that your audit system meets legal standards.

1. Access AWS Artifact

- AWS Console → Services → Security, Identity, & Compliance → **Artifact**.
- On the tab bar, select **Reports**.

![art](/images/10.art/001.png) 

2. Download reports 
-   In the **Reports** tab:
    + Select **SOC 2**, **ISO 27001** then **Download** (PDF).
![art](/images/10.art/002.png) 
    + Save the PDF files to your project's local folder.

3. Compare requirements (Gap Analysis)
- Open the SOC 2 PDF file
- Identify requirements for **logging**, **monitoring**, **retention**.
- Record the mapping between the standards and the implemented features.

4. Gather Audit Trail evidence
- **CloudWatch Logs Export**
- **S3 Version List**
- **Athena Query Results**
- **Snapshot QuickSight Dashboard**
- **Compliance PDFs**

5. Prepare for submission to regulator

- Package the files.

With this step, we have completed the audit lifecycle from technical (logging, immutability, reporting, dashboard, alerting, SOP) to legal evidence.