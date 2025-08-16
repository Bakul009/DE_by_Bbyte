
---

# 🎬 YouTube Trending Data Pipeline with Databricks
<img width="1536" height="1024" alt="image" src="https://github.com/user-attachments/assets/9e0d97c7-d536-4971-902a-3f793bf95915" />

## 📌 Project Overview

This project extends the **YouTube Data API → AWS Lambda → S3** pipeline by processing the data in **Databricks** using the **Medallion Architecture (Bronze, Silver, Gold)**.
The final processed data is stored in **Databricks SQL Warehouse** and visualized through **Databricks Dashboards / BI tools**.

---

## 🔄 Data Flow Architecture

1. **YouTube Data API** → Fetch trending videos data.
2. **AWS Lambda** → Trigger daily, save raw JSON to **S3**.
3. **Databricks Landing Zone** → Read raw S3 files.
4. **Bronze Layer** → Store raw ingested data (minimal transformations).
5. **Silver Layer** → Clean, normalize, and structure data.
6. **Gold Layer** → Business-ready aggregated tables (top videos, channel stats, category insights).
7. **Databricks SQL Warehouse** → Store processed tables for analytics.
8. **Visualization** → Dashboards in Databricks, Power BI, or Apache Superset.

---

## ⚙️ Setup Instructions

### 1️⃣ Prerequisites

* AWS account (with S3 bucket setup from the Lambda step).
* Databricks workspace (Community or Enterprise).
* SQL Warehouse enabled.
* Proper permissions for **Databricks to access S3**.

---

### 2️⃣ Mount S3 Bucket in Databricks

To access your S3 bucket:

1. Go to **Databricks Workspace** → **Data** → **Add Data** → **S3**.
2. Provide your **AWS Access Key & Secret Key** (or IAM Role if using cross-account).
3. Mount S3 bucket to Databricks `/mnt/youtube-trending/`.

---

### 3️⃣ Medallion Architecture

#### 🔹 Bronze Layer (Raw Data)

* Reads raw JSON from S3.
* Stores as Delta Table.
* Minimal type casting.

#### 🔹 Silver Layer (Cleansed Data)

* Flatten nested JSON (title, description, views, likes, comments).
* Enforce schema, handle null values, deduplication.

#### 🔹 Gold Layer (Business Tables)

* **gold\_trending\_videos** → Top trending videos.
* **gold\_channel\_stats** → Aggregated channel-wise metrics.
* **gold\_category\_stats** → Category-wise engagement (views, likes, comments).
* **gold\_top10\_videos\_per\_category** → Ranking per category.

---

### 4️⃣ Scheduling the Job

1. Open **Databricks Jobs**.
2. Create new job → Select **Bronze/Silver/Gold Notebook**.
3. Set **Schedule**:

   * Timezone: **Asia/Kolkata (UTC+5:30)**
   * Daily at **09:30 AM**.
4. Configure cluster (Serverless or All-purpose).
5. Save & Enable.

---

### 5️⃣ Visualization in Databricks

1. Go to **SQL Editor** in Databricks.
2. Connect to **SQL Warehouse**.
3. Run queries like:

   ```sql
   SELECT category_name, total_views, total_likes, total_comments, like_ratio, comment_ratio
   FROM yt_trending_catalog.gld_sch_yt.gold_category_stats
   ORDER BY total_views DESC;
   ```
4. Click **+ New Visualization** → Choose chart type:

   * **Bar Chart** → Category vs Total Views.
   * **Pie Chart** → Likes % by Category.
   * **Line Chart** → Trends over Published Date.
5. Pin to a **Dashboard**.

---

### 6️⃣ Storing in SQL Warehouse

* All **Gold tables** are stored in **Databricks SQL Warehouse**.
* BI Tools like **Power BI, Tableau, Apache Superset** can connect using **Databricks SQL Connector (JDBC/ODBC)**.

---

## 📊 Example Dashboards

* **Top Categories by Views** (Bar Chart).
* **Like % vs Comment % per Category** (Stacked Bar).
* **Top 10 Trending Videos per Category** (Table + Rank).
* **Channel Performance Leaderboard** (Horizontal Bar).

---

## 🔐 IAM Policy (Databricks → S3 Access)

Attach the following policy to the Databricks IAM Role/User:

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": [
        "s3:GetObject",
        "s3:ListBucket",
        "s3:PutObject"
      ],
      "Resource": [
        "arn:aws:s3:::<your-bucket-name>",
        "arn:aws:s3:::<your-bucket-name>/*"
      ]
    }
  ]
}
```

---

## ✅ Final Deliverables

* **AWS Lambda + S3** → Raw trending video data.
* **Databricks Landing → Bronze → Silver → Gold** pipeline.
* **Daily scheduled job (9:30 AM IST)**.
* **Interactive Dashboards** in Databricks & BI tools.
* **SQL Warehouse storage** for analytics.

---

🚀 With this pipeline, you now have an **end-to-end data engineering + analytics project** showcasing **real-world trending video insights**!

---



