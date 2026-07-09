---
title: "Worklog Week 10"
date: 2026-06-22
weight: 10
chapter: false
pre: " <b> 1.10. </b> "
---

### Week 10 Objectives:

- Revise and finalize the official architecture diagram for the Serverless Intelligent Document Processing (IDP) project based on feedback from Admin mentors in the First Cloud Journey group.
- Conduct in-depth research on the core Serverless services in the project: Amazon API Gateway, AWS Lambda, Amazon S3, Amazon SQS, Amazon Textract, Amazon DynamoDB, and Amazon Cognito.
- Begin deploying the first foundational infrastructure components on the real AWS environment (Region us-east-1).

### Tasks to Deploy This Week:

| Day | Task                                                                                                                                                                                                                                                                                  | Start Date | Completion Date | Documentation Source                      |
| --- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------- | --------------- | ----------------------------------------- |
| Mon | - Consolidate and analyze feedback from Admin mentors on the v1 architecture diagram of the IDP system <br> - Revise the diagram: optimize the document processing flow (S3 → SQS → Lambda AI-Worker → Textract → DynamoDB), improve the Shared Services & Security Zone segmentation | 22/06/2026 | 22/06/2026      | Feedback from FCJ Admin Mentors           |
| Tue | - Finalize the official architecture diagram (final version) with all 9 processing steps <br> - Determine the deployment order: IAM/KMS first → S3 Buckets → DynamoDB → Lambda Functions → API Gateway → Cognito → WAF                                                                | 23/06/2026 | 23/06/2026      | draw.io, AWS Well-Architected Framework   |
| Wed | - Study detailed technical documentation: Amazon API Gateway (REST API), AWS Lambda (Execution Role, Timeout, Memory), Amazon S3 (Presigned URL, Event Notification) <br> - Research Amazon SQS (Standard Queue, Trigger Lambda), Amazon Textract (AnalyzeDocument, Queries)          | 24/06/2026 | 24/06/2026      | AWS Documentation, FCJ Course             |
| Thu | - Deploy the Shared Services & Security Zone: create IAM Roles for each Lambda Function, configure AWS KMS for data encryption, set up AWS Budgets for cost monitoring <br> - Initialize 2 S3 Buckets: S3 Upload (document storage) and S3 Frontend (static website hosting)          | 25/06/2026 | 25/06/2026      | AWS Console, FCJ Course                   |
| Fri | - Create the Amazon DynamoDB table for storing processed JSON data <br> - Deploy the first Lambda Function: the Presigned URL generator allowing users to upload documents directly to S3 Upload <br> - Configure S3 Event Notification (ObjectCreated) to send events to Amazon SQS  | 26/06/2026 | 26/06/2026      | AWS Console, AWS Documentation            |
| Sat | - Test the basic upload flow: Lambda generates Presigned URL → Client uploads file to S3 → S3 Event triggers SQS <br> - Document any issues encountered with IAM Policy, S3 CORS, or SQS Permissions, and create an action plan for the following week                                | 27/06/2026 | 27/06/2026      | <https://cloudjourney.awsstudygroup.com/> |

### Week 10 Achievements:

| Day | Task                                                     | Achievement                                                                                                                                                                                                                                                                     |
| --- | -------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Mon | Analyzing feedback and revising the architecture diagram | Thoroughly consolidated all feedback from Admin mentors, optimized the document processing pipeline (S3 → SQS → Lambda AI-Worker → Textract → DynamoDB) and improved the Shared Services & Security Zone segmentation (IAM, KMS, Budgets).                                      |
| Tue | Finalizing the official architecture diagram (final)     | Completed the final version of the IDP system architecture diagram with all 9 processing steps. Determined a logical deployment sequence: IAM/KMS → S3 → DynamoDB → Lambda → API Gateway → Cognito → WAF.                                                                       |
| Wed | Studying technical documentation of Serverless services  | Mastered the configurations of API Gateway REST API, Lambda Execution Roles, S3 Presigned URL and Event Notification, SQS Standard Queue triggering Lambda, and the Textract AnalyzeDocument API. Estimated the expected costs to optimize the deployment budget.               |
| Thu | Deploying Shared Services and S3 Buckets                 | Successfully set up dedicated IAM Roles for each Lambda Function following the Least Privilege principle, configured KMS keys for data encryption, and established Budgets. Initialized 2 S3 Buckets: Upload (for source documents) and Frontend (for static website hosting).  |
| Fri | Deploying DynamoDB, Lambda Presigned URL, and SQS        | Successfully created the DynamoDB table for JSON data storage. Deployed the Lambda Function for generating Presigned URLs for document uploads. Configured S3 Event Notification (ObjectCreated) to trigger notifications into the Amazon SQS queue.                            |
| Sat | Testing the upload flow and documenting issues           | Confirmed the basic upload flow works: Lambda generates Presigned URL → Client successfully uploads file to S3 → S3 Event sends notification to SQS. Identified and resolved IAM Policy and S3 CORS issues. Created a detailed plan to deploy the AI Processing tier next week. |

---

### Practical Evidence Images:

![alt text](image-1.png)
