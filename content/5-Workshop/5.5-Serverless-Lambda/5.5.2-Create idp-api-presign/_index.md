---
title : "Create idp-api-presign"
date : 2026-07-01
weight : 2
chapter : false
pre : " <b> 5.5.2. </b> "
---

The **idp-api-presign** function is responsible for generating a short-lived Presigned URL. This allows the React Frontend application to securely upload documents directly to S3 without exposing AWS access keys.

#### Step 1: Initialize the Lambda Function
1. Navigate to the **AWS Lambda** console and click **Create function**.
2. Choose **Author from scratch**.
3. **Function name**: Enter `idp-api-presign`.
4. **Runtime**: Select **Python 3.12**.
5. Click **Create function**.

#### Step 2: Grant S3 Write Permissions to the Execution Role
Because this function needs to generate URLs that permit file uploads to S3, we must attach full S3 access policies to its specific execution role:
1. Go to the **Configuration** tab and select **Permissions** from the left menu.
2. Under **Execution role**, click the blue link formatted as **idp-api-presign-role-xxxx**.

![Execution Role Link](/images/5-Workshop/5.5-Serverless-Lambda/presign-role.png)

3. In the IAM console that opens, click **Add permissions** and select **Attach policies**.
4. Type `AmazonS3FullAccess` in the search box and check the box next to this policy.

![Attach S3 Full Access](/images/5-Workshop/5.5-Serverless-Lambda/attach-s3-access.png)

5. Scroll to the bottom and click **Add permissions** to complete the process.

#### Step 3: Deploy the Source Code
1. Return to the Lambda console for **idp-api-presign** and switch to the **Code** tab.
2. Open **lambda_function.py**, delete the default code, and paste the following snippet:

```python
import json
import boto3
import uuid

s3_client = boto3.client('s3')
# MAKE SURE THIS BUCKET NAME MATCHES YOURS
BUCKET_NAME = 'idp-ingest-bucket-1'

def lambda_handler(event, context):
    try:
        # 1. Read the exact file type sent by React (Supports Lambda Proxy)
        query_params = event.get('queryStringParameters') or {}
        content_type = query_params.get('contentType', 'image/jpeg') # Default to jpeg
        
        # Generate random file name
        file_extension = content_type.split('/')[-1]
        file_name = f"uploads/{uuid.uuid4()}.{file_extension}"
        
        # 2. Stamp the exact Content-Type onto the signature
        presigned_url = s3_client.generate_presigned_url(
            'put_object',
            Params={
                'Bucket': BUCKET_NAME,
                'Key': file_name,
                'ContentType': content_type # Crucial to prevent 403 errors
            },
            ExpiresIn=300
        )
        
        return {
            'statusCode': 200,
            'headers': {
                'Access-Control-Allow-Origin': '*'
            },
            'body': json.dumps({
                'upload_url': presigned_url
            })
        }
    except Exception as e:
        return {
            'statusCode': 500,
            'body': json.dumps({'error': str(e)})
        }
```
3. Click the **Deploy** button to activate the new code.