---
title : "Create Ingestion S3 Bucket"
date : 2024-01-01 
weight : 1
chapter : false
pre : " <b> 5.3.1. </b> "
---

#### Create the Bucket
This bucket will securely store the raw documents uploaded by users before they are processed by the AI.

1. Navigate to the **Amazon S3** console and click **Create bucket**.
2. **Bucket name**: Enter **idp-ingest-bucket-1**.
3. **AWS Region**: Select **US East (N. Virginia) us-east-1**.
4. **Object Ownership**: Select **ACLs disabled**.
5. **Block Public Access settings for this bucket**: Check **Block all public access**.
![Block Public Access](/images/5-Workshop/5.3-Storage-Database/s3-ingest-block-public-1.png)

6. Leave all other options as default.
![Block Public Access](/images/5-Workshop/5.3-Storage-Database/s3-ingest-block-public-2.png)
![Block Public Access](/images/5-Workshop/5.3-Storage-Database/s3-ingest-block-public-3.png)
![Block Public Access](/images/5-Workshop/5.3-Storage-Database/s3-ingest-block-public-4.png)

7. Click **Create bucket**.

#### Configure CORS
Since our frontend will upload files directly to this bucket, we must configure Cross-Origin Resource Sharing (CORS).
1. Click on your newly created **idp-ingest-bucket-1**.
2. Go to the **Permissions** tab.
3. Scroll down to **Cross-origin resource sharing (CORS)** and click **Edit**.
4. Paste the following JSON configuration and click **Save changes**:

```json
[
  {
    "AllowedHeaders": ["*"],
    "AllowedMethods": ["PUT", "POST", "GET"],
    "AllowedOrigins": ["*"],
    "ExposeHeaders": []
  }
]