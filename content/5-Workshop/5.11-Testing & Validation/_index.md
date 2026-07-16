---
title : "Testing & Validation"
date : 2026-07-01
weight : 11
chapter : false
pre : " <b> 5.11. </b> "
---

#### 1. System Testing Strategy

Following the successful CI/CD deployment via AWS Amplify, comprehensive End-to-End (E2E) testing is mandatory. This validation process ensures the integrity of the data flow, the responsiveness of the serverless architecture, and the reliability of our security perimeters (AWS WAF & Amazon Cognito).

#### 2. Functional & Integration Test Cases

The table below outlines the core test scenarios following the exact lifecycle of the intelligent document processing workflow:

| TC ID | Category | Test Scenario | Expected Result |
| :--- | :--- | :--- | :--- |
| **TC-01** | **Auth (Cognito)** | Log in to the system using a verified and valid account. | The browser receives a JWT Token, stores it securely, and successfully redirects the user to the Dashboard. |
| **TC-02** | **Security (AWS WAF)** | Send over 100 continuous requests within 5 minutes to the API Gateway to simulate Spam/DDoS. | The WAF `BlockSpamIP` rate-based rule triggers, blocking the traffic and returning a `403 Forbidden` error. |
| **TC-03** | **Upload (API & S3)** | Upload an invoice file (JPG/PDF). The system calls the `GET /get-upload-url` API. | Lambda successfully generates a Presigned URL. The file is uploaded directly to the S3 bucket's `uploads/` directory without CORS errors. |
| **TC-04** | **AI Logic (Textract)** | Monitor the Event-Driven flow as the file lands in S3, triggering SQS and the Lambda AI-Worker. | Textract accurately extracts `QUERIES` fields (Invoice Number, Vendor, Total Amount, Date), and the JSON structure is successfully stored in DynamoDB. |
| **TC-05** | **Data Privacy** | Invoke the `GET /invoices` API to retrieve the invoice list on the Dashboard. | Sensitive data is successfully masked (e.g., Tax ID is displayed securely as `******xxxx`). |
| **TC-06** | **UI/UX (React)** | Apply various filters (Search, Category Sorting) on the web interface. | The UI responds seamlessly; statistical charts (Monthly Revenue, Top Vendors) update accurately matching the DynamoDB records. |

#### 3. Architecture Evaluation

*   **High Availability & Scalability:** The Serverless infrastructure (AWS Lambda, DynamoDB On-demand, Amazon SQS) automatically scales based on data batches (Batch size: 10), ensuring no bottlenecks occur during concurrent multi-user uploads.
*   **Cost Optimization:** The configured S3 Lifecycle Rule automatically purges raw invoice images after 1 day, significantly reducing long-term storage costs while preserving the highly valuable structured JSON data in DynamoDB.