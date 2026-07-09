---
title : "Create idp-api-categories"
date : 2026-07-01
weight : 5
chapter : false
pre : " <b> 5.5.5. </b> "
---

The **idp-api-categories** function scans the entire invoice data table and performs automatic categorization based on vendor name keywords (e.g., grouping Cloud infrastructure, utility costs, or other operational expenses).

#### Step 1: Initialize the Lambda Function
1. Click **Create function**.
2. Choose **Author from scratch**.
3. **Function name**: Enter exactly `idp-api-categories`.
4. **Runtime**: Use **Python 3.12**.
5. **Permissions**: Select **Use an existing role** and apply **idp-lambda-ai-role**.

![Create Get Categories Function](/images/5-Workshop/5.5-Serverless-Lambda/get-categories.png)

6. Click **Create function**.

#### Step 2: Deploy the Source Code
1. Access the **Code** tab of the newly created function.
2. Replace all default code with the following snippet that executes the categorization logic:

```python
import json
import boto3

dynamodb = boto3.resource('dynamodb')
TABLE_NAME = 'InvoicesData'

def lambda_handler(event, context):
    try:
        table = dynamodb.Table(TABLE_NAME)
        response = table.scan()
        items = response.get('Items', [])
        
        categories_dict = {}
        for item in items:
            ext = item.get('extracted_data', {}) or item
            vendor = ext.get('vendor_name', 'Uncategorized')
            total_str = ext.get('total_amount', 0)
            doc_id = item.get('documentId', '')
            
            try:
                total = float(str(total_str).replace('.', '').replace(',', ''))
            except:
                total = 0.0
                
            # Apply smart categorization logic based on keywords
            if 'amazon' in str(vendor).lower() or 'aws' in str(vendor).lower():
                category = 'Cloud Infrastructure'
            elif 'điện' in str(vendor).lower() or 'electric' in str(vendor).lower():
                category = 'Utility Costs'
            else:
                category = 'Other Operational Costs'
                
            if category not in categories_dict:
                categories_dict[category] = {'count': 0, 'total_value': 0.0, 'documents': []}
                
            categories_dict[category]['count'] += 1
            categories_dict[category]['total_value'] += total
            categories_dict[category]['documents'].append(doc_id)
            
        return {
            'statusCode': 200,
            'headers': {
                'Access-Control-Allow-Origin': '*',
                'Content-Type': 'application/json'
            },
            'body': json.dumps({'status': 'success', 'data': categories_dict}, ensure_ascii=False)
        }
    except Exception as e:
        return {'statusCode': 500, 'body': json.dumps({'error': str(e)})}
```
3. Click the orange **Deploy** button to apply the code changes.