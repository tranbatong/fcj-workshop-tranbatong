---
title : "Storage & Database Setup"
date : 2026-07-01
weight : 3
chapter : false
pre : " <b> 5.3. </b> "
---

#### Storage & Database Setup

In this section, you will provision the foundational data layers for the IDP system. This involves creating storage for raw documents and static web hosting, as well as configuring NoSQL databases for the AI-extracted data.

* **Amazon S3**: Used for storing raw uploaded documents (ingestion) and hosting the static frontend assets.
* **Amazon DynamoDB**: A NoSQL database used to store the structured data extracted by AI, user payment statuses, and categorization rules.

#### Content

- [Create Ingestion S3 Bucket](1-s3-ingest/)
- [Create Frontend S3 Bucket](2-s3-frontend/)
- [Configure S3 Lifecycle Rule](3-s3-lifecycle/)
- [Create DynamoDB Tables](4-dynamodb/)