---
title : "Create Frontend S3 Bucket"
date : 2024-01-01 
weight : 2
chapter : false
pre : " <b> 5.3.2. </b> "
---

#### Create the Bucket
This bucket will be used to host your compiled React web application.

1. Go back to the **Amazon S3** buckets list and click **Create bucket**.
2. **Bucket name**: Enter **idp-frontend-bucket-1**.
3. **AWS Region**: Select **US East (N. Virginia) us-east-1**.
![Unblock Public Access](/images/5-Workshop/5.3-Storage-Database/s3-frontend-public-1.png)

4. **Object Ownership**: Select **ACLs disabled**.
5. **Block Public Access settings for this bucket**: **Uncheck** the box for **Block all public access**.
![Unblock Public Access](/images/5-Workshop/5.3-Storage-Database/s3-frontend-public-2.png) 

6. Check the acknowledgment box stating you understand the bucket might become public.
![Unblock Public Access](/images/5-Workshop/5.3-Storage-Database/s3-frontend-public-3.png)

7. Leave all other options as default. Click **Create bucket**.