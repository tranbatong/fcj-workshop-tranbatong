---
title : "Tạo hàm idp-api-get-stats"
date : 2026-07-01
weight : 4
chapter : false
pre : " <b> 5.5.4. </b> "
---

Hàm **idp-api-get-stats** thực hiện việc tổng hợp dữ liệu hóa đơn theo từng mốc thời gian (tháng) và gom nhóm theo từng nhà cung cấp (vendor), chuyển đổi cấu trúc phân tích để cung cấp trực tiếp dữ liệu vẽ biểu đồ cho Frontend.

#### Bước 1: Khởi tạo hàm Lambda
1. Nhấn nút **Create function** trong giao diện AWS Lambda.
2. Chọn **Author from scratch**.
3. **Function name**: Nhập `idp-api-get-stats`.
4. **Runtime**: Chọn **Python 3.12**.
5. **Permissions**: Tích chọn mục **Use an existing role** và chỉ định vai trò **idp-lambda-ai-role**.

![Create Get Stats Function](/images/5-Workshop/5.5-Serverless-Lambda/get-stats.png)

6. Bấm nút **Create function**.

#### Bước 2: Triển khai mã nguồn
1. Mở tab **Code** của hàm **idp-api-get-stats**.
2. Dán đoạn mã nguồn phân tích dữ liệu thống kê sau vào tệp `lambda_function.py`:

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
            vendor = ext.get('vendor_name') or 'Chưa xác định'
            
            # Ép kiểu dữ liệu tiền tệ về dạng số thực
            try:
                amount = float(str(amount_str).replace('.', '').replace(',', ''))
            except:
                amount = 0.0
                
            # Định dạng và ép kiểu chuỗi ngày tháng (Từ dạng DD/MM/YYYY sang YYYY-MM để sắp xếp biểu đồ)
            parts = date_str.split('/')
            if len(parts) == 3:
                month = f"{parts[2]}-{parts[1]}"
            else:
                month = "Khác"
                
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
        return {'statusCode': 500, 'body': json.dumps(f"Lỗi: {str(e)}")}

```

3. Nhấn nút Deploy để kích hoạt mã nguồn mới.