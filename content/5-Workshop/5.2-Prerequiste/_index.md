---
title : "Prerequisite"
date : 2026-07-01 
weight : 2 
chapter : false
pre : " <b> 5.2. </b> "
---

#### What you need before starting
Before diving into building the Serverless IDP System, please ensure you have the following prerequisites ready:

**1. AWS Account & Permissions**
* You will need an active AWS account.
* Ensure you are operating in the **US East (N. Virginia) us-east-1** region, as specified in this workshop.
* Your IAM user or role must have administrative privileges or sufficient permissions to create and manage the following services:
    * Amazon S3
    * Amazon DynamoDB
    * Amazon SQS
    * AWS Lambda
    * Amazon API Gateway
    * Amazon Cognito
    * Amazon Textract
    * AWS WAF

**2. Local Development Environment**
To build and run the frontend React application, you need to set up your local machine with the following tools:
* **Node.js**: Ensure Node.js (version 18 or later) is installed on your machine to manage packages (npm) and run the local development server.
* **Code Editor**: Install a code editor such as **Visual Studio Code (VS Code)** to edit the frontend code and configure project files.

**3. Execution Policy (Windows Users Only)**
If you are using Windows, you might encounter permission issues when running `npm` scripts in the terminal. To prevent this, open PowerShell as an Administrator and run:
```powershell
Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser