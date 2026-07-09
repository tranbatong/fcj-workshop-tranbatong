---
title : "Create idp-api-get-invoices"
date : 2026-07-01
weight : 3
chapter : false
pre : " <b> 5.5.3. </b> "
---

The **idp-api-get-invoices** function scans the **InvoicesData** DynamoDB table to retrieve all extracted invoice data, cleans currency formatting, masks sensitive data, and returns the list to the user interface.

#### Step 1: Initialize the Lambda Function
1. In the AWS Lambda console, click **Create function**.
2. Choose **Author from scratch**.
3. **Function name**: Enter `idp-api-get-invoices`.
4. **Runtime**: Select **Python 3.12**.
5. **Permissions**: Select **Use an existing role** and choose **idp-lambda-ai-role**.

![Create Get Invoices Function](/images/5-Workshop/5.5-Serverless-Lambda/get-invoices.png)

6. Click **Create function**.

#### Step 2: Deploy the Source Code
1. Open the **Code** tab of the newly created function and edit **lambda_function.py**.
2. Paste the following data processing code into the editor:

```python
import json
import boto3
from decimal import Decimal

class DecimalEncoder(json.JSONEncoder):
    def default(self, obj):
        if isinstance(obj, Decimal): return float(obj)
        return super(DecimalEncoder, self).default(obj)

dynamodb = boto3.resource('dynamodb')
table = dynamodb.Table('InvoicesData')

def lambda_handler(event, context):
    try:
        response = table.scan()
        items = response.get('Items', [])
        formatted_items = []
        
        for item in items:
            ext = item.get('extracted_data', {})
            if not ext: continue # Skip if no extracted data
            
            # Clean currency (remove dots and commas)
            amount_str = ext.get('total_amount') or '0'
            try:
                clean_amount = float(str(amount_str).replace('.', '').replace(',', ''))
            except:
                clean_amount = 0
                
            # Map keys to match React Frontend expectations
            mapped_item = {
                'VendorName': ext.get('vendor_name') or 'Unknown',
                'InvoiceDate': ext.get('date') or 'N/A',
                'TotalAmount': clean_amount,
                'TaxID': ext.get('tax_id') or 'N/A'
            }
            
            # Data Masking: Mask part of the Tax ID for security
            tax_id = mapped_item['TaxID']
            if tax_id != 'N/A' and len(str(tax_id)) > 4:
                mapped_item['TaxID'] = '******' + str(tax_id)[-4:]
                
            formatted_items.append(mapped_item)
            
        return {
            'statusCode': 200,
            'headers': {'Access-Control-Allow-Origin': '*'},
            'body': json.dumps(formatted_items, cls=DecimalEncoder)
        }
    except Exception as e:
        return {'statusCode': 500, 'body': json.dumps(f"Error: {str(e)}")}
```
3. Click **Deploy** to save and apply the code.