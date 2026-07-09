---
title : "Create IAM Role"
date : 2026-07-01 
weight : 2 
chapter : false
pre : " <b> 5.4.2. </b> "
---

AWS Lambda functions require an execution role to interact with other AWS services. We will create a role that grants necessary permissions.

#### Step-by-step instructions:
1. Navigate to the **IAM** (Identity and Access Management) console and click **Create role**.
2. **Trusted entity type**: Select **AWS service**.
3. **Use case**: Select **Lambda**, then click **Next**.

![IAM Trust Entity](/images/5-Workshop/5.4-Messaging-IAM/iam-trust-1.png)

4. On the **Add permissions** page, search for and select (check the box) the following 5 policies:
   * `AWSLambdaSQSQueueExecutionRole`
   * `AmazonS3ReadOnlyAccess`
   * `AmazonDynamoDBFullAccess`
   * `AmazonTextractFullAccess`
   * `AmazonBedrockFullAccess`

![IAM Permissions](/images/5-Workshop/5.4-Messaging-IAM/iam-permissions-2.png)

5. Click **Next**.
6. **Role name**: Enter `idp-lambda-ai-role`.
![IAM Permissions](/images/5-Workshop/5.4-Messaging-IAM/idp-lambda-ai-role.png)
7. Scroll to the bottom and click **Create role**.