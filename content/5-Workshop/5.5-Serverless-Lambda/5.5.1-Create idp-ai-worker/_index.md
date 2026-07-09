---
title : "Create idp-ai-worker"
date : 2026-07-01
weight : 1
chapter : false
pre : " <b> 5.5.1. </b> "
---

The **idp-ai-worker** function is responsible for asynchronous processing. When a file is uploaded to S3, a message is pushed to the SQS queue, triggering this function to extract information using Amazon Textract AI and save the results into DynamoDB.

#### Step 1: Initialize the Lambda Function
1. Navigate to the **AWS Lambda** console, select **Functions** on the left menu, and click **Create function**.
2. Choose **Author from scratch**.
3. **Function name**: Enter `idp-ai-worker`.
4. **Runtime**: Select **Python 3.12**.
5. **Permissions**: Expand *Change default execution role*, select **Use an existing role**, and choose **idp-lambda-ai-role** from the dropdown list.

![Create Lambda](/images/5-Workshop/5.5-Serverless-Lambda/create-worker.png)

6. Click **Create function**.

#### Step 2: Configure Memory and Timeout
Since invoking AI for document extraction consumes more time and resources than standard processes, you need to increase the default limits:
1. Go to the **Configuration** tab and select **General configuration** from the left menu.
2. Click **Edit**.
3. **Memory**: Change from `128 MB` to `256 MB`.
4. **Timeout**: Change from `0 min 3 sec` to `1 min 0 sec`.

![Memory and Timeout Config](/images/5-Workshop/5.5-Serverless-Lambda/worker-config.png)

5. Click **Save**.

#### Step 3: Add SQS Trigger
1. In the **Function overview** section at the top of the page, click **Add trigger**.
2. **Select a source**: Search for and select **SQS**.
3. **SQS queue**: Select the ARN of the `idp-document-queue`.
4. **Batch size**: Keep the default value of `10`.

![SQS Trigger Config](/images/5-Workshop/5.5-Serverless-Lambda/worker-trigger.png)

5. Leave the other options as default and click **Add**.

#### Step 4: Deploy the Source Code
1. Switch to the **Code** tab and open the `lambda_function.py` file.
2. Delete all the default code and paste the following source code:

```python
import json
import boto3
import urllib.parse
import uuid
import datetime

# Initialize clients
textract = boto3.client('textract', region_name='us-east-1')
dynamodb = boto3.resource('dynamodb', region_name='us-east-1')
table = dynamodb.Table('InvoicesData')

def lambda_handler(event, context):
    try:
        for record in event['Records']:
            message_body = json.loads(record['body'])
            if 'Records' not in message_body:
                continue
                
            s3_event = message_body['Records'][0]
            bucket_name = s3_event['s3']['bucket']['name']
            object_key = urllib.parse.unquote_plus(s3_event['s3']['object']['key'])
            
            print(f"Starting Textract AI processing for: {object_key} from {bucket_name}")
            
            # Call Textract AI (Using Queries feature)
            response = textract.analyze_document(
                Document={'S3Object': {'Bucket': bucket_name, 'Name': object_key}},
                FeatureTypes=["QUERIES"],
                QueriesConfig={
                    "Queries": [
                        {"Text": "What is the invoice number?", "Alias": "invoice_number"},
                        {"Text": "What is the date?", "Alias": "date"},
                        {"Text": "What is the total amount?", "Alias": "total_amount"},
                        {"Text": "What is the vendor name or company name?", "Alias": "vendor_name"}
                    ]
                }
            )
            
            # Restructure JSON results
            extracted_data = {
                "invoice_number": None,
                "date": None,
                "total_amount": None,
                "vendor_name": None
            }
            
            blocks = response['Blocks']
            for block in blocks:
                if block['BlockType'] == 'QUERY':
                    alias = block['Query']['Alias']
                    if 'Relationships' in block:
                        for rel in block['Relationships']:
                            if rel['Type'] == 'ANSWER':
                                answer_id = rel['Ids'][0]
                                for answer_block in blocks:
                                    if answer_block['Id'] == answer_id:
                                        extracted_data[alias] = answer_block['Text']
                                        
            print(f"Extraction successful: {json.dumps(extracted_data, ensure_ascii=False)}")
            
            # Save to DynamoDB
            item = {
                'documentId': str(uuid.uuid4()),
                'original_filename': object_key,
                'upload_time': datetime.datetime.now().isoformat(),
                'extracted_data': extracted_data
            }
            
            table.put_item(Item=item)
            print("Successfully saved data to DynamoDB!")
            
        return {
            'statusCode': 200,
            'body': json.dumps('Processing complete!')
        }
    except Exception as e:
        print(f"Error: {str(e)}")
        raise e

```
3. Click the orange **Deploy** button to apply the new source code to the system.