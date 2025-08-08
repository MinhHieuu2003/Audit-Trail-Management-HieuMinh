---
title : "Investigation Tools with Amazon QuickSight"
date :  2025-08-04
weight : 7 
chapter : false
pre : " <b> 7. </b> "
---
### Amazon QuickSight
{{% notice info %}}
You need to create a QuickSight account to try this demo.
{{% /notice %}}

![quick](/images/7.quick/001.png)

![quick](/images/7.quick/003.png)

1. Grant QuickSight access to data

+ In QuickSight Home, click **Manage QuickSight** → **Security & permissions**.
+ In the **QuickSight access to AWS services** section → click **Manage** → check **Athena** → **Save**.
+ In the **QuickSight access to AWS services** section → click **Select S3 buckets** → select `audit-demo-logs` -> and enable “Write permission for Athena Workgroup”. -> **Save**.

![quick](/images/7.quick/002.png)

+ QuickSight now has permission to run queries on Athena and read results in S3.

2. Build Analysis & Visuals

- From QuickSight Home → click **Datasets** (left menu) → **New dataset**.

![quick](/images/7.quick/004.png)

- Select **Athena** → **Connect**.

- Enter Data source name: `AuditLogsAthena` → **Create data source**.

- On the data selection screen:

    + Database: `audit_reports`

    + Table: `audit_logsaudit_demo_logs`

- Click **Select** → you will see a preview of the table.

- Enable **Import to SPICE for quicker analytics** → **Visualize**.

![quick](/images/7.quick/005.png)

3. Build Analysis & Visuals.

![quick](/images/7.quick/006.png)

- Draw Timeline Events:
    + In the **Visuals** pane, click the + **ADD** button → select **Add visual**.
    + Drag the `timestamp` field from the **Data** pane to the **X axis** area in the **Field wells** pane.
    + The chart will show the number of events over time.

![quick](/images/7.quick/007.png)

- Draw Heatmap User Activity:
    + Click + ADD → Add visual.
    + Select the **Heat map** icon.
    In **Field wells**:
    + Drag `user` to **Rows**.
    + Drag `timestamp` to **Columns** → click the right arrow and change Date granularity to Day.
    + Drag Count to Color intensity.
    The heatmap will show the density of events per user per day, with color intensity representing the count.

![quick](/images/7.quick/008.png)

- Draw Top Users:
    + Click + ADD → Add visual.

    Select the **Horizontal bar chart** icon.

    In Field wells:
    + Drag `user` to **Category**.
    + Drag `Count` to **Value**.

![quick](/images/7.quick/009.png)

- Add a Filter by action.

- After creating all visuals, click **Save** and name it `AuditTrailInvestigation`.

4. Publish

- In Analysis, click **Publish dashboard**.

- Dashboard name: `Audit Trail Investigation`.

![quick](/images/7.quick/010.png)

![quick](/images/7.quick/011.png)