---
title : "Create idp-api-payments"
date : 2026-07-01
weight : 6
chapter : false
pre : " <b> 5.5.6. </b> "
---

The **idp-api-payments** function applies a Filter Expression directly on DynamoDB to scan for and aggregate all invoice records with an **UNPAID** or **PENDING** status. This helps display outstanding expenses on the management dashboard.

#### Step 1: Initialize the Lambda Function
1. Click **Create function** in the AWS Lambda console.
2. Check **Author from scratch**.
3. **Function name**: Enter `idp-api-payments`.
4. **Runtime**: Select the **Python 3.12** environment.
5. **Permissions**: Choose **Use an existing role** and assign the **idp-lambda-ai-role**.

![Create Get Payments Function](/images/5-Workshop/5.5-Serverless-Lambda/get-payments.png)

6. Click **Create function** to complete the initial setup.

#### Step 2: Deploy the Source Code
1. Select the **Code** tab for the **idp-api-payments** function.
2. Paste the following outstanding debt filter code into **lambda_function.py**:

```python
import json
import boto3
from boto3.dynamodb.conditions import Attr

dynamodb = boto3.resource('dynamodb')
TABLE_NAME = 'InvoicesData'

def lambda_handler(event, context):
    try:
        table = dynamodb.Table(TABLE_NAME)
        # Scan and conditionally filter invoices with unpaid or pending status
        response = table.scan(
            FilterExpression=Attr('payment_status').eq('UNPAID') | Attr('payment_status').eq('PENDING')
        )
        unpaid_invoices = response.get('Items', [])
        
        total_debt = 0.0
        formatted_invoices = []
        for inv in unpaid_invoices:
            ext = inv.get('extracted_data', {}) or inv
            amount_str = ext.get('total_amount', 0)
            try:
                amount = float(str(amount_str).replace('.', '').replace(',', ''))
            except:
                amount = 0.0
                
            total_debt += amount
            formatted_invoices.append({
                'documentId': inv.get('documentId'),
                'vendor_name': ext.get('vendor_name', 'Unknown'),
                'total_amount': amount,
                'payment_status': inv.get('payment_status', 'UNPAID')
            })
            
        return {
            'statusCode': 200,
            'headers': {
                'Access-Control-Allow-Origin': '*',
                'Content-Type': 'application/json'
            },
            'body': json.dumps({
                'status': 'success',
                'total_debt': total_debt,
                'invoices': formatted_invoices
            }, ensure_ascii=False)
        }
    except Exception as e:
        return {'statusCode': 500, 'body': json.dumps({'error': str(e)})}

```
3. Don't forget to click the orange **Deploy** button to put the function into an active state.