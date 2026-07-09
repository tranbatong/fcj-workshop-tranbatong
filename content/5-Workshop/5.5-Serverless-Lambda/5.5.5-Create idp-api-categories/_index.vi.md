---
title : "Tạo hàm idp-api-categories"
date : 2026-07-01
weight : 5
chapter : false
pre : " <b> 5.5.5. </b> "
---

Hàm **idp-api-categories** quét toàn bộ bảng dữ liệu hóa đơn và thực hiện phân loại danh mục tự động dựa trên từ khóa tên nhà cung cấp (chẳng hạn như phân nhóm hạ tầng Cloud, chi phí tiện ích điện nước, hoặc các chi phí vận hành khác).

#### Bước 1: Khởi tạo hàm Lambda
1. Chọn nút **Create function**.
2. Chọn mục **Author from scratch**.
3. **Function name**: Điền chính xác `idp-api-categories`.
4. **Runtime**: Sử dụng **Python 3.12**.
5. **Permissions**: Chọn **Use an existing role** và áp dụng **idp-lambda-ai-role**.

![Create Get Categories Function](/images/5-Workshop/5.5-Serverless-Lambda/get-categories.png)

6. Nhấn nút **Create function**.

#### Bước 2: Triển khai mã nguồn
1. Truy cập tab **Code** của hàm vừa tạo.
2. Thay thế toàn bộ mã mặc định bằng đoạn mã nguồn thực thi logic gom nhóm danh mục dưới đây:

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
            vendor = ext.get('vendor_name', 'Chưa phân loại')
            total_str = ext.get('total_amount', 0)
            doc_id = item.get('documentId', '')
            
            try:
                total = float(str(total_str).replace('.', '').replace(',', ''))
            except:
                total = 0.0
                
            # Áp dụng logic phân loại thông minh dựa theo các từ khóa xuất hiện
            if 'amazon' in str(vendor).lower() or 'aws' in str(vendor).lower():
                category = 'Hạ tầng Cloud'
            elif 'điện' in str(vendor).lower() or 'electric' in str(vendor).lower():
                category = 'Chi phí Tiện ích'
            else:
                category = 'Chi phí Vận hành khác'
                
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

3. Nhấn nút Deploy để kích hoạt mã nguồn mới.