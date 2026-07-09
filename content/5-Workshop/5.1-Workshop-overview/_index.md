---
title : "Introduction"
date: 2026-07-01
weight : 1 
chapter : false
pre : " <b> 5.1. </b> "
---

#### Intelligent Document Processing (IDP)
**Intelligent Document Processing (IDP)** leverages Artificial Intelligence (AI) and Machine Learning (ML) to automatically extract, categorize, and structure data from raw documents such as invoices and receipts. By utilizing a serverless architecture, this system scales automatically, reduces manual entry, and minimizes infrastructure management overhead.

#### Workshop overview
In this workshop, you will build a fully serverless IDP architecture on AWS rather than traditional VPC or on-premises networks. You will provision and integrate the following core components:

* **Storage & Database:** You will create Amazon S3 buckets (**idp-ingest-bucket-1** for raw file ingestion and **idp-frontend-bucket-1** for frontend hosting). You will also deploy Amazon DynamoDB tables (**InvoicesData**, **InvoicesPayments**, and **UserCategories**) to store the extracted data.
* **Asynchronous Messaging:** An Amazon SQS queue (**idp-document-queue**) will act as a buffer between S3 uploads and the processing logic.
* **Compute & AI:** AWS Lambda functions (**idp-ai-worker**) will process incoming documents by calling Amazon Textract to query and extract specific text fields.
* **Security & APIs:** The system's backend will be exposed via Amazon API Gateway (**idp-rest-api**). You will secure the application using Amazon Cognito (**idp-react-app**) for user authentication and AWS WAF (**idp-api-waf-shield**) to block spam requests.
* **Frontend:** A React Single-Page Application (SPA) will be developed to handle file uploads via presigned URLs and visualize the processed data using interactive dashboards.

![overview](/images/5-Workshop/5.1-Workshop-overview/diagram1.png)