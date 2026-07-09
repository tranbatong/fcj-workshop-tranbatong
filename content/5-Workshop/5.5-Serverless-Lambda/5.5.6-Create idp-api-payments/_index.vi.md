---
title : "Tạo hàm idp-api-payments"
date : 2026-07-01
weight : 6
chapter : false
pre : " <b> 5.5.6. </b> "
---

Hàm **idp-api-payments** thực hiện bộ lọc có điều kiện (Filter Expression) trực tiếp trên DynamoDB để quét tìm và thống kê toàn bộ những bản ghi hóa đơn có trạng thái chưa thanh toán (**UNPAID**) hoặc đang chờ duyệt (**PENDING**), giúp hiển thị nợ đọng chi phí lên bảng giao diện quản lý.

#### Bước 1: Khởi tạo hàm Lambda
1. Chọn mục **Create function** trong giao diện AWS Lambda.
2. Tích chọn **Author from scratch**.
3. **Function name**: Điền tên hàm là `idp-api-payments`.
4. **Runtime**: Lựa chọn phiên bản môi trường **Python 3.12**.
5. **Permissions**: Chọn cấu hình vai trò **Use an existing role** và gán role `idp-lambda-ai-role`.

![Create Get Payments Function](/images/5-Workshop/5.5-Serverless-Lambda/get-payments.png)

6. Bấm **Create function** để hoàn tất khởi tạo ban đầu.

#### Bước 2: Triển khai mã nguồn
1. Chọn tab **Code** của hàm **idp-api-payments**.
2. Dán đoạn mã nguồn lọc điều kiện nợ đọng chi phí dưới đây vào file **lambda_function.py**:

```python
import json
import boto3
from boto3.dynamodb.conditions import Attr

dynamodb = boto3.resource('dynamodb')
TABLE_NAME = 'InvoicesData'

def lambda_handler(event, context):
    try:
        table = dynamodb.Table(TABLE_NAME)
        # Quét và lọc có điều kiện các hóa đơn có trạng thái chưa thanh toán hoặc đang chờ duyệt
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
                'vendor_name': ext.get('vendor_name', 'Không rõ'),
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

3. Nhấn nút Deploy để kích hoạt mã nguồn mới.