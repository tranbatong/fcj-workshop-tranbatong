---
title : "Create REST API & Resources"
date : 2026-07-01
weight : 1
chapter : false
pre : " <b> 5.7.1. </b> "
---

#### Step 1: Create a REST API
1. Navigate to the **API Gateway** console.
2. Scroll down to **REST API** (make sure it doesn't say "Private") and click **Build**.
3. Select **New API**.
4. **API name**: Enter `idp-backend-api`.
5. **Endpoint Type**: Choose **Regional**.

![Create API Gateway](/images/5-Workshop/5.7-API-Gateway-WAF/create-api.png)
6. Click **Create API**.

#### Step 2: Create Resources and Methods
We need to map URL paths to our 5 API Lambda functions. We will do this by creating Resources (URLs) and Methods (HTTP Verbs).

Follow this exact process for each of the 5 endpoints:
1. Click on the root path.
2. Click **Create resource**.
3. **Resource Name**: Enter `get-upload-url` (This automatically sets the Resource path to **/get-upload-url**). Click **Create resource**.
4. Select the newly created **/get-upload-url** resource, click **Create method**.

![API Gateway Method](/images/5-Workshop/5.7-API-Gateway-WAF/api-resource.png)
5. **Method type**: Select **GET**.
6. **Integration type**: Select **Lambda function**.
7. **Lambda proxy integration**: **MUST CHECK THIS BOX** (Turn it on).
8. **Lambda function**: Select **idp-api-presign**.
9. Click **Create method**.

![API Gateway Method](/images/5-Workshop/5.7-API-Gateway-WAF/api-method.png)

#### Repeat for all endpoints
Repeat the process above to create the following Resources and GET methods:
* Resource `/invoices` -> GET method -> Lambda: `idp-api-get-invoices`
* Resource `/stats` -> GET method -> Lambda: `idp-api-get-stats`
* Resource `/categories` -> GET method -> Lambda: `idp-api-categories`
* Resource `/payments` -> GET method -> Lambda: `idp-api-payments`

*(Make sure **Lambda proxy integration** is checked for all of them!)*