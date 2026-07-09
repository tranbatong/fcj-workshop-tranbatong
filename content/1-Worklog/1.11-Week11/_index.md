---
title: "Worklog Week 11"
date: 2026-06-29
weight: 11
chapter: false
pre: " <b> 1.11. </b> "
---

### Week 11 Objectives:

- Update the project architecture based on newly emerged requirements: expanding the Dashboard APIs Layer.
- Deploy the core AI Processing Workflow (IDP) integrating Amazon Textract for automated document recognition and data extraction.
- Build the Dashboard APIs Layer (consisting of 4 Lambda functions) and set up Amazon API Gateway to serve data to the Frontend application.

### Tasks to Deploy This Week:

| Day | Task                                                                                                                                                                                                                                            | Start Date | Completion Date | Documentation Source                         |
| --- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------- | --------------- | -------------------------------------------- |
| Mon | Evaluate the newly emerged requirements, expand the Dashboard APIs Layer design from 2 to 4 Lambda functions (adding API-Get-Category and API-Get-Payment).                                                                                     | 29/06/2026 | 29/06/2026      | Project Requirements, AWS Architecture       |
| Tue | Deploy the AWS Lambda AI-Worker function for document processing. Configure IAM Policies and set up a trigger from Amazon SQS to automatically invoke the AI-Worker when a new message arrives.                                                 | 30/06/2026 | 30/06/2026      | AWS Documentation, FCJ Course                |
| Wed | Integrate the Amazon Textract SDK (AnalyzeDocument API) into the AI-Worker function. Process the extracted text data and normalize it into JSON format. Write code to connect and store the resulting JSON file into the Amazon DynamoDB table. | 01/07/2026 | 01/07/2026      | Amazon Textract Developer Guide              |
| Thu | Develop 4 Lambda functions within the Dashboard APIs Layer: API-Get-Invoices, API-Get-Stats, API-Get-Category, API-Get-Payment. Optimize Scan/Query operations from DynamoDB to return data quickly for the Dashboard.                          | 02/07/2026 | 02/07/2026      | Boto3 Documentation, DynamoDB Best Practices |
| Fri | Initialize Amazon API Gateway (REST API) and create resources/methods (GET /invoices, /stats, etc.). Integrate API Gateway with the 4 corresponding Lambda functions and enable CORS (Cross-Origin Resource Sharing) for Frontend API calls.    | 03/07/2026 | 03/07/2026      | AWS Console, API Gateway Guide               |
| Sat | Test the complete End-to-End flow: File Upload, SQS, AI-Worker, Textract, DynamoDB, API Gateway. Document any issues and prepare the deployment plan for the security layer (Cognito, WAF) for Week 12.                                         | 04/07/2026 | 04/07/2026      | <https://cloudjourney.awsstudygroup.com/>    |

### Week 11 Achievements:

| Day | Task                                       | Achievement                                                                                                                                                                                              |
| --- | ------------------------------------------ | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Mon | Updating project architecture              | Finalized the new architecture diagram and detailed the design of the 4 new Lambda functions for the Dashboard APIs Layer.                                                                               |
| Tue | Deploying Lambda AI-Worker and SQS Trigger | Successfully created the AI-Worker function with the necessary IAM Policies (SQS read, Textract invoke, DynamoDB write). Established the SQS trigger to invoke Lambda immediately upon file upload.      |
| Wed | Integrating Amazon Textract and DynamoDB   | The AI-Worker successfully called Amazon Textract to analyze documents and accurately extract data. Raw data was converted into standard JSON and successfully stored in the Amazon DynamoDB table.      |
| Thu | Building the Dashboard APIs Layer          | Successfully coded and deployed 4 independent Lambda functions. These functions precisely executed Scan/Query operations on DynamoDB to retrieve statistics, categories, payments, and invoice lists.    |
| Fri | Setting up Amazon API Gateway              | Successfully built the REST API with all required routes. Configured the integration between API Gateway and the Lambda functions, resolving CORS issues to allow the Frontend to fetch data seamlessly. |
| Sat | End-to-End flow testing and documentation  | The IDP processing flow operated smoothly from start to finish. Textract performed well on sample invoices. Compiled a list of remaining tasks (WAF, Cognito) to secure the system in the final week.    |

---

### Practical Evidence Images:

![alt text](image-1.png)
