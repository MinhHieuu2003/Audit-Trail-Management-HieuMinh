---
title : "Investigation Tools với Amazon QuickSight"
date :  2025-08-04
weight : 7 
chapter : false
pre : " <b> 7. </b> "
---
### Amazon QuickSight
{{% notice info %}}
Bạn cần tạo 1 account Quicksight để thử hiện demo này 
{{% /notice %}}

![quick](/images/7.quick/001.png)

![quick](/images/7.quick/003.png)

1. Cấp quyền cho QuickSight truy cập dữ liệu

+ Trong QuickSight Home, click **Manage QuickSight** → **Security & permissions**.
+ Phần **QuickSight access to AWS services** → click **Manage** → tick chọn **Athena****** → **Save**.
+ Phần **QuickSight access to AWS services** → click **Select S3 buckets** → chọn `audit-demo-logs` -> và bật ô “Write permission for Athena Workgroup”. -> **Save**.

![quick](/images/7.quick/002.png)

+ QuickSight bây giờ có quyền chạy query lên Athena và đọc kết quả trong S3.

2. Xây dựng Analysis & Visuals

- Từ QuickSight Home → click **Datasets** (menu trái) → **New dataset**.

![quick](/images/7.quick/004.png)

- Chọn **Athena** → **Connecy**.

- Điền Data source name: `AuditLogsAthena` → **Create data source**.

- Trong màn hình chọn dữ liệu:

    + Database: `audit_reports`

    + Table: `audit_logsaudit_demo_logs`

- Click **Select** → sẽ thấy preview bảng.

- Bật **Import to SPICE for quicker analytics** → **Visualize**.

![quick](/images/7.quick/005.png)

3. Xây dựng Analysis & Visuals.

![quick](/images/7.quick/006.png)

- Vẽ Timeline Events:
    + Ở pane **Visuals**, click nút + **ADD** → chọn **Add visual**.
    + Kéo trường `timestamp` từ pane **Data** vào khu vực **X axis** trong pane **Field wells**.
    + Chart sẽ vẽ số events theo thời gian.

![quick](/images/7.quick/007.png)

- Vẽ Heatmap User Activity:
    + Click + ADD → Add visual.
    + Chọn icon **Heat map**.
    Trong **Field wells**:
    + Kéo `user` vào **Rows**.
    + Kéo `timestamp` vào **Columns** → click mũi tên bên phải và chuyển Date granularity sang Day.
    + Kéo Count vào Color intensity.
    Bảng heatmap sẽ hiển thị mật độ event của từng user theo ngày, với màu đậm nhạt thể hiện số lượng.

![quick](/images/7.quick/008.png)

- Vẽ Vẽ Top Users:
    + Click + ADD → Add visual.

    Chọn icon **Horizontal bar chart**.

    Trong Field wells:
    + Kéo `user` vào **Category**.
    + Kéo `Count` vào **Value**.

![quick](/images/7.quick/009.png)

- Thêm Filter theo action.

- Sau khi đã vẽ xong các visual, click **Save** rồi đặt tên `AuditTrailInvestigation`.

4. Xuất bản 

- Trong Analysis, click **Publish dashboard**.

- Dashboard name: `Audit Trail Investigation`.

![quick](/images/7.quick/010.png)

![quick](/images/7.quick/011.png)











