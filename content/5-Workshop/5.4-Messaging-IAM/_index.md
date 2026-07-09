---
title : "Messaging & IAM Configuration"
date : 2026-07-01
weight : 4
chapter : false
pre : " <b> 5.4. </b> "
---

#### Messaging & IAM Configuration

In this section, you will set up the asynchronous messaging layer and the security permissions required for your serverless backend to operate correctly. 

Instead of processing documents synchronously (which can cause timeouts), we will use **Amazon SQS** as a buffer. Furthermore, adhering to the principle of least privilege, you will create a specific **AWS IAM Role** that grants your Lambda functions just enough access to interact with S3, DynamoDB, SQS, and AWS AI services.

#### Content

- [Create SQS Queue](1-sqs/)
- [Create IAM Role](2-iam-role/)