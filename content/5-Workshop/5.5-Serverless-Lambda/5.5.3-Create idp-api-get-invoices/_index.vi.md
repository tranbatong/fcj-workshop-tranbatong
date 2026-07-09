---
title : "Tạo hàm idp-api-get-invoices"
date : 2026-07-01
weight : 3
chapter : false
pre : " <b> 5.5.3. </b> "
---

Hàm **idp-api-get-invoices** thực hiện việc quét (scan) bảng **InvoicesData** trên DynamoDB để lấy toàn bộ dữ liệu hóa đơn đã bóc tách, tiến hành làm sạch định dạng tiền tệ, che giấu dữ liệu nhạy cảm (data masking) và trả về danh sách cho giao diện người dùng.

#### Bước 1: Khởi tạo hàm Lambda
1. Tại giao diện quản lý AWS Lambda, chọn **Create function**.
2. Chọn **Author from scratch**.
3. **Function name**: Nhập `idp-api-get-invoices`.
4. **Runtime**: Chọn **Python 3.12**.
5. **Permissions**: Chọn **Use an existing role** và chọn **idp-lambda-ai-role**.

![Create Get Invoices Function](/images/5-Workshop/5.5-Serverless-Lambda/get-invoices.png)

6. Bấm nút **Create function**.

#### Bước 2: Triển khai mã nguồn
1. Mở tab **Code** của hàm vừa tạo, chỉnh sửa tệp tin **lambda_function.py**.
2. Dán nội dung xử lý dữ liệu sau đây vào trình soạn thảo:

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
            if not ext: continue # Bỏ qua nếu không có dữ liệu bóc tách
            
            # Làm sạch tiền tệ (xóa dấu chấm, dấu phẩy)
            amount_str = ext.get('total_amount') or '0'
            try:
                clean_amount = float(str(amount_str).replace('.', '').replace(',', ''))
            except:
                clean_amount = 0
                
            # Đổi tên key cho khớp với cấu trúc React Frontend mong muốn
            mapped_item = {
                'VendorName': ext.get('vendor_name') or 'Chưa xác định',
                'InvoiceDate': ext.get('date') or 'N/A',
                'TotalAmount': clean_amount,
                'TaxID': ext.get('tax_id') or 'N/A'
            }
            
            # Data Masking: Che giấu bớt ký tự mã số thuế để bảo mật thông tin
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
        return {'statusCode': 500, 'body': json.dumps(f"Lỗi: {str(e)}")}
        
```
3. Nhấn nút Deploy để kích hoạt mã nguồn mới.