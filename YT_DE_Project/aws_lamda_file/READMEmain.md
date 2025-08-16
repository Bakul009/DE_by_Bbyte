
# 📺 YouTube Data API → AWS Lambda → S3

<img width="1536" height="1024" alt="image" src="https://github.com/user-attachments/assets/48962274-be89-4b47-9c8b-36788020535a" />


## 1. Project Overview

This project automatically fetches trending YouTube data using the YouTube Data API, processes it via AWS Lambda, and stores it in **Amazon S3** as JSON files.

**Architecture:**

```
YouTube Data API → AWS Lambda → S3 (Raw/Trending Data)
```

**Key Features:**

* Automated daily data fetch
* Stores structured JSON in S3
* Ready for ETL pipelines (Databricks, analytics)

---

## 2. Prerequisites

* AWS Account with permissions to create:

  * Lambda function
  * S3 bucket
  * IAM role
  * EventBridge (CloudWatch) rule
* YouTube Data API key
* Lambda ZIP file (code and dependencies)
* Git repository with project structure

---

## 3. AWS S3 Setup

1. Create an S3 bucket (example: `my-api-data-lambda`)
2. Optional: Organize data by folder structure (date-based):

```
my-api-data-lambda/
    └── 2025/
        └── 08/
            └── 15/
```

---

## 4. IAM Role for Lambda

Create a role with permissions to write to S3 and log to CloudWatch.

**Example IAM Policy:**

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": [
        "s3:PutObject",
        "s3:GetObject",
        "s3:ListBucket"
      ],
      "Resource": [
        "arn:aws:s3:::my-api-data-lambda",
        "arn:aws:s3:::my-api-data-lambda/*"
      ]
    },
    {
      "Effect": "Allow",
      "Action": [
        "logs:CreateLogGroup",
        "logs:CreateLogStream",
        "logs:PutLogEvents"
      ],
      "Resource": "*"
    }
  ]
}
```

Attach this policy to the Lambda execution role.

---

## 5. AWS Lambda Setup

1. Navigate to **AWS Lambda → Create function → Upload .zip file**
2. Runtime: **Python 3.x**
3. Assign the IAM role from Step 4
4. Set **Environment Variables**:

| Key              | Value                |
| ---------------- | -------------------- |
| `YT_API_KEY`     | `YOUR_API_KEY_HERE`  |
| `S3_BUCKET_NAME` | `my-api-data-lambda` |

5. Set the **Handler** (e.g., `lambda_function.lambda_handler`)

---

## 6. Schedule Lambda Execution (Daily)

1. Go to **EventBridge (CloudWatch Events) → Create rule**
2. Select **Schedule → Cron expression**

   * Example: **9:20 AM IST** → 03:50 UTC
   * Cron: `cron(50 3 * * ? *)`
3. Target: Your Lambda function
4. Enable the rule

---

## 7. Testing

* Manually invoke the Lambda function in the console
* Verify JSON files in S3, organized by timestamped folders

---

## 8. Next Steps

* Integrate with **Databricks** for ETL pipeline (bronze → silver → gold)
* Schedule **automated dashboards** with Power BI or Superset
* Add **notifications** for failures using AWS SNS

---

✅ **Result:** Automated daily ingestion of trending YouTube data, stored in S3, ready for analytics and visualization.

---


