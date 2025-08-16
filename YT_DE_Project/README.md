# 📊 YouTube Trending Data Pipeline Project
<img width="1536" height="1024" alt="image" src="https://github.com/user-attachments/assets/a6c894f2-8aa1-4df0-a901-5ba266d4b092" />

## 🚀 Project Overview

This project demonstrates a **modern data engineering pipeline** that transforms raw **YouTube Trending Data** into actionable insights using **AWS + Databricks**. The entire workflow automates data ingestion, transformation, and visualization to showcase real-world data engineering skills.

---

## 🔑 Key Highlights

* **Data Source:** YouTube Data API (trending video stats).
* **Ingestion Layer:** AWS Lambda fetches daily data → stored in **AWS S3 (Landing Zone)**.
* **ETL in Databricks:**

  * **Bronze Layer:** Raw JSON stored.
  * **Silver Layer:** Cleaned & structured dataset (video, channel, category stats).
  * **Gold Layer:** Aggregated insights (top videos, engagement ratios, category trends).
* **Scheduling:** Databricks Job triggers daily at **9:30 AM IST**.
* **Visualization:** Interactive dashboards in **Databricks SQL / Power BI**.
* **Storage:** Final curated datasets stored in **Databricks SQL Warehouse**.

---

## 📈 Business Value

* Identify **top trending categories** on YouTube.
* Measure **audience engagement** with likes/comments ratios.
* Track **top-performing channels** by views & engagement.
* Provide **visual insights** for content strategy & marketing.

---

## 🛠️ Tech Stack

* **AWS**: Lambda, S3
* **Databricks**: Delta Lake, SQL, Jobs, Dashboards
* **Visualization**: Databricks SQL Dashboards / Power BI

---

## 🌟 Why This Project Stands Out

✅ End-to-end pipeline (from API → Dashboard)
✅ Real-world **medallion architecture (Bronze-Silver-Gold)**
✅ Automated daily refresh (production-ready)
✅ Business-focused dashboards & KPIs

---

📌 This project is designed to be **portfolio-ready**, demonstrating cloud, big data, and visualization expertise all in one solution.
