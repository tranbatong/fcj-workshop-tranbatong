---
title: "Workshop"
date: 2026-07-01
weight: 5
chapter: false
pre: " <b> 5. </b> "
---

# Serverless Intelligent Document Processing (IDP) System 

#### Overview

**Intelligent Document Processing (IDP)** leverages AI and Machine Learning to transform unstructured data from documents (such as invoices, receipts, and identity cards) into structured, actionable information. 

In this workshop, you will learn how to build a fully serverless, event-driven IDP system on AWS. By utilizing managed services, this architecture ensures high availability, automatic scaling, and secure data processing without the overhead of managing underlying infrastructure.

Throughout this lab, you will deploy and configure various AWS services across different layers:
* **Storage & Database:** Amazon S3 for document ingestion and DynamoDB for storing extracted structured data.
* **Asynchronous Processing:** Amazon SQS and AWS Lambda to decouple the ingestion from the AI extraction workload.
* **AI/ML:** Amazon Textract to automatically query and extract specific fields from uploaded images and PDFs.
* **Security & Authentication:** Amazon Cognito for user management, API Gateway for RESTful routing, and AWS WAF for rate-limiting and threat protection.
* **Frontend & CI/CD:** A React Single-Page Application (SPA) hosted on AWS Amplify with an automated CI/CD pipeline, utilizing a custom domain managed by Amazon Route 53 to interact securely with backend APIs via HTTPS.

#### Content

1. [Workshop overview](5.1-Workshop-overview/)
2. [Prerequisite](5.2-Prerequisite/)
3. [Storage & Database Setup](5.3-Storage-Database/)
4. [Messaging & IAM Configuration](5.4-Messaging-IAM/)
5. [Serverless Backend with Lambda](5.5-Lambda-Functions/)
6. [Authentication with Cognito](5.6-Identity-Cognito/)
7. [API Gateway & WAF Security](5.7-API-Gateway-WAF/)
8. [React Frontend Implementation](5.8-Frontend-React/)
9. [Custom Domain with Amazon Route 53](5.9-Route53-Domain/)
10. [CI/CD & Hosting with AWS Amplify](5.10-Amplify-Hosting/)
11. [Testing & Validation](5.11-Testing-Validation/)
