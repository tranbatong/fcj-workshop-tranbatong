---
title: "Proposal"
date: 2026-06-17
weight: 2
chapter: false
pre: " <b> 2. </b> "
---

This section presents the proposed idea and implementation plan for the project that will be developed during the **AWS First Cloud AI Journey 2026** program.

# Serverless Intelligent Document Processing (IDP) System

## Intelligent Document Processing Solution on AWS Serverless

---

## 1. Executive Summary

The **Serverless Intelligent Document Processing (IDP) System** is a web application that enables users to upload documents such as VAT invoices, payment receipts, and administrative forms. Once uploaded, the system automatically leverages AWS Artificial Intelligence services to recognize, extract, and organize important information into structured data for searching, reporting, and management purposes.

The entire solution is built on a **Serverless Architecture**, eliminating the need for Amazon EC2 instances. This architecture reduces operational costs, automatically scales according to workload, and simplifies infrastructure management.

---

## 2. Problem Statement

### Current Challenges

Many organizations still perform manual data entry from invoices and business documents. This process is time-consuming, prone to human error, and makes searching, reporting, and analyzing information more difficult.

In addition, traditional OCR systems typically require dedicated servers, software installation, and continuous infrastructure maintenance, resulting in higher deployment and operational costs.

### Proposed Solution

Our team proposes a fully serverless Intelligent Document Processing system built entirely on AWS cloud services.

Users upload documents through a web application. The system generates **Amazon S3 Presigned URLs**, allowing documents to be uploaded directly to Amazon S3. After the upload is completed, an asynchronous processing workflow is triggered using Amazon SQS and AWS Lambda. The Lambda function invokes Amazon Textract to extract document information and stores the structured results in Amazon DynamoDB.

The frontend communicates with REST APIs hosted on Amazon API Gateway to display invoice history, statistical dashboards, and analytical reports.

### Benefits and ROI

The proposed solution offers several advantages:

- Fully automates document processing.
- Reduces manual data entry time.
- Improves data accuracy through AI.
- Eliminates server management.
- Low operational cost with a pay-as-you-go pricing model.
- Easily scales as document volume increases.

---

## 3. Solution Architecture

The system is designed using an **Event-Driven Serverless Architecture**.

The React frontend is hosted on Amazon S3. AWS WAF is integrated to protect the web application from malicious traffic and common web attacks.

Users authenticate through Amazon Cognito. After successful authentication, Amazon API Gateway validates JWT tokens before forwarding requests to AWS Lambda functions.

For document uploads, AWS Lambda generates a Presigned URL, allowing users to upload documents directly to Amazon S3. Whenever a new object is created, Amazon S3 generates an **ObjectCreated** event and sends a message to Amazon SQS. The Lambda AI Worker retrieves documents from the queue, submits them to Amazon Textract for document analysis, and stores the extracted JSON results in Amazon DynamoDB.

Dashboard APIs retrieve invoice records and statistical data from DynamoDB for visualization on the web application.

![alt text](image-1.png)

### AWS Services Used

- AWS WAF
- Amazon S3
- Amazon API Gateway
- Amazon Cognito
- AWS Lambda
- Amazon SQS
- Amazon Textract
- Amazon DynamoDB
- AWS Identity and Access Management (IAM)
- AWS Key Management Service (KMS)
- AWS Budgets

### Component Design

**Frontend**

- React Single Page Application (SPA)
- Amazon S3

**Authentication**

- Amazon Cognito User Pool
- JWT Authentication

**Backend API**

- Amazon API Gateway
- AWS Lambda

**Upload Service**

- Amazon S3
- S3 Presigned URL

**AI Processing**

- Amazon SQS
- AWS Lambda AI Worker
- Amazon Textract

**Database**

- Amazon DynamoDB

**Security**

- AWS WAF
- AWS IAM
- AWS KMS

**Monitoring**

- AWS Budgets

---

## 4. Technical Implementation

### Implementation Phases

The project is divided into four major phases.

**Phase 1**

- Requirement analysis
- AWS architecture design
- Data processing workflow analysis

**Phase 2**

- Frontend development
- Amazon Cognito integration
- REST API development using Amazon API Gateway and AWS Lambda

**Phase 3**

- Implement document upload workflow
- Process documents using Amazon Textract
- Store extracted data in Amazon DynamoDB

**Phase 4**

- Develop dashboard and reporting features
- System testing
- Cost optimization
- Final deployment

### Technical Requirements

Required technologies include:

- AWS Lambda
- Amazon S3
- Amazon API Gateway
- Amazon Cognito
- Amazon Textract
- Amazon DynamoDB
- Amazon SQS
- AWS IAM
- AWS WAF
- ReactJS
- JavaScript
- AWS SDK

---

## 5. Project Roadmap & Milestones

- **Pre-Internship (Month 0)**
  - Define project objectives.
  - Design the overall AWS architecture.
  - Analyze AWS services and estimate infrastructure costs.

- **Internship Period (Months 1–3)**
  - **Month 1**
    - Learn AWS Serverless services.
    - Design the system architecture.
    - Develop the frontend and backend APIs.

  - **Month 2**
    - Implement document upload functionality.
    - Develop the AI processing workflow.
    - Integrate Amazon Textract and Amazon DynamoDB.

  - **Month 3**
    - Build dashboard and reporting features.
    - Perform testing and debugging.
    - Optimize infrastructure costs.
    - Deploy the completed system.

- **Post Deployment**
  - Evaluate system performance.
  - Explore additional AWS AI services for future enhancements.

---

## 6. Budget Estimation

To ensure that the proposed solution remains affordable while meeting the requirements for performance, scalability, and availability, the team estimated the infrastructure cost using the **AWS Pricing Calculator**.

Since the architecture is fully serverless, charges are incurred only when services are actually used. Compared with traditional EC2-based deployments, this significantly reduces infrastructure costs.

The AWS Pricing Calculator will be updated once the final production architecture has been completed.

### Estimated Monthly Infrastructure Cost

| AWS Service        | Purpose                                      | Estimated Monthly Cost |
| ------------------ | -------------------------------------------- | ---------------------: |
| Amazon S3          | Store frontend assets and uploaded documents |               1.20 USD |
| AWS WAF            | Protect the web application                  |               2.50 USD |
| Amazon API Gateway | REST API                                     |               0.80 USD |
| AWS Lambda         | Backend processing and AI workflow           |               1.00 USD |
| Amazon Cognito     | User authentication                          | 0.00 USD _(Free Tier)_ |
| Amazon Textract    | OCR and document analysis                    |               4.50 USD |
| Amazon DynamoDB    | Invoice data storage                         |               0.60 USD |
| Amazon SQS         | Event queue                                  |               0.10 USD |
| AWS KMS            | Data encryption                              |               0.15 USD |
| AWS Budgets        | Cost monitoring                              |               0.00 USD |

### Estimated Total Cost

| Item                        | Estimated Cost          |
| --------------------------- | ----------------------- |
| Monthly Infrastructure Cost | **≈ 12.35 USD / month** |
| Annual Infrastructure Cost  | **≈ 148 USD / year**    |

Because the solution adopts a **Serverless Pay-as-you-go** pricing model, it is highly suitable for student research projects and small-to-medium-scale deployments.

---

## 7. Risk Assessment

### Risk Matrix

- Incorrect information extraction by Amazon Textract.
- Document upload failures due to unstable Internet connections.
- Increased Amazon Textract costs as document volume grows.
- AWS Lambda timeout when processing very large documents.

### Mitigation Strategy

- Validate extracted data before storing it.
- Use Amazon SQS for asynchronous processing.
- Configure AWS Budgets to monitor infrastructure costs.
- Restrict the maximum upload file size.

### Contingency Plan

- Allow users to re-upload failed documents.
- Enable automatic retry through Amazon SQS.
- Monitor errors using Amazon CloudWatch Logs.
- Encrypt sensitive information using AWS KMS.

---

## 8. Expected Outcomes

### Technical Improvements

- Fully automated document processing workflow.
- Significant reduction in manual data entry time.
- Higher extraction accuracy using Amazon Textract.
- Highly scalable Serverless architecture.

### Long-term Value

The proposed system can be extended to process various document types such as electronic invoices, business licenses, national ID cards, contracts, and other structured documents.

Furthermore, the platform provides a solid foundation for integrating advanced AWS AI services such as **Amazon Comprehend** and **Amazon Bedrock** in the future, enabling more intelligent document analysis and richer business insights.
