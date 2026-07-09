---
title : "Create idp-api-get-stats"
date : 2026-07-01
weight : 4
chapter : false
pre : " <b> 5.5.4. </b> "
---

The `idp-api-get-stats` function aggregates invoice data by time periods (months) and groups them by vendor. It transforms the analytical structure to provide charting data directly to the Frontend.

#### Step 1: Initialize the Lambda Function
1. Click **Create function** in the AWS Lambda console.
2. Choose **Author from scratch**.
3. **Function name**: Enter `idp-api-get-stats`.
4. **Runtime**: Select **Python 3.12**.
5. **Permissions**: Check **Use an existing role** and specify the **idp-lambda-ai-role**.

![Create Get Stats Function](/images/5-Workshop/5.5-Serverless-Lambda/get-stats.png)

6. Click **Create function**.

#### Step 2: Deploy the Source Code
1. Open the **Code** tab for **idp-api-get-stats**.
2. Paste the following statistical analysis code into **lambda_function.py**:

```python
import json
import boto3
from collections import defaultdict
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
        monthly_revenue = defaultdict(float)
        vendor_stats = defaultdict(float)
        
        for item in items:
            ext = item.get('extracted_data', {})
            if not ext: continue
            
            date_str = ext.get('date') or ''
            amount_str = ext.get('total_amount') or '0'
            vendor = ext.get('vendor_name') or 'Unknown'
            
            # Cast currency data to float
            try:
                amount = float(str(amount_str).replace('.', '').replace(',', ''))
            except:
                amount = 0.0
                
            # Format and cast date strings (From DD/MM/YYYY to YYYY-MM for chart sorting)
            parts = date_str.split('/')
            if len(parts) == 3:
                month = f"{parts[2]}-{parts[1]}"
            else:
                month = "Other"
                
            monthly_revenue[month] += amount
            vendor_stats[vendor] += amount
            
        monthly_chart_data = [{"month": k, "total": v} for k, v in monthly_revenue.items()]
        monthly_chart_data.sort(key=lambda x: x["month"])
        vendor_chart_data = [{"vendor": k, "total": v} for k, v in vendor_stats.items()]
        
        return {
            'statusCode': 200,
            'headers': {'Access-Control-Allow-Origin': '*'},
            'body': json.dumps({"monthly": monthly_chart_data, "vendors": vendor_chart_data}, cls=DecimalEncoder)
        }
    except Exception as e:
        return {'statusCode': 500, 'body': json.dumps(f"Error: {str(e)}")}
```
3. Click the orange **Deploy** button to save and finish the configuration.