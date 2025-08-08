---
title : "Legal Coordination với AWS Artifact"
date :  2025-08-06
weight : 10 
chapter : false
pre : " <b> 10. </b> "
---
### AWS Artifact
Thu thập các báo cáo compliance (như SOC 2, ISO 27001, GDPR) từ AWS Artifact để đối chiếu và chứng minh hệ thống audit của bạn đáp ứng tiêu chuẩn pháp lý.

1. Vào AWS Artifact

- AWS Console → Services → Security, Identity, & Compliance → **Artifact**.
- Trên thanh tab, chọn **Reports**.

![art](/images/10.art/001.png) 

2. Tải về các báo cáo 
-   Trong tab **Reports**:
    + Chọn **SOC 2**, **ISO 27001** rồi **Download** (PDF).
![art](/images/10.art/002.png) 
    + Lưu file PDF vào local folder của dự án.

3. Đối chiếu yêu cầu (Gap Analysis)
- Mở file PDF SOC 2
- Xác định yêu cầu về **logging**, **monitoring**, **retention**.
- Ghi lại mapping giữa tiêu chuẩn và tính năng triển khai.

4. Tập hợp chứng cứ Audit Trail
- **CloudWatch Logs Export**
- **S3 Version List**
- **Athena Query Results**
- **Snapshot QuickSight Dashboard**
- **Compliance PDFs**

5. Chuẩn bị nộp regulator

- Đóng gói file. 

Với bước này, chúng ta đã hoàn thiện vòng đời audit từ kỹ thuật (ghi log, bất biến, báo cáo, dashboard, cảnh báo, SOP) đến chứng cứ pháp lý.


