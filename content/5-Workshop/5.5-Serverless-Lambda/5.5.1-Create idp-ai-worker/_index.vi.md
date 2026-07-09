---
title : "Tạo hàm idp-ai-worker"
date : 2026-07-01
weight : 1
chapter : false
pre : " <b> 5.5.1. </b> "
---

Hàm **idp-ai-worker** chịu trách nhiệm xử lý không đồng bộ. Khi có tệp tin tải lên S3, một thông báo được đẩy vào hàng SQS và kích hoạt hàm này để bóc tách thông tin bằng Amazon Textract AI rồi lưu kết quả vào DynamoDB.

#### Bước 1: Khởi tạo hàm Lambda
1. Truy cập giao diện **AWS Lambda**, chọn **Functions** ở menu bên trái và bấm **Create function**.
2. Chọn mục **Author from scratch**.
3. **Function name**: Nhập `idp-ai-worker`.
4. **Runtime**: Chọn **Python 3.12**.
5. **Permissions**: Mở mục *Change default execution role*, tích chọn **Use an existing role** và chọn **idp-lambda-ai-role** từ danh sách.

![Khởi tạo Lambda](/images/5-Workshop/5.5-Serverless-Lambda/create-worker.png)

6. Bấm nút **Create function**.

#### Bước 2: Thay đổi cấu hình RAM và Timeout
Vì tác vụ gọi AI bóc tách tài liệu tiêu tốn thời gian hơn các xử lý thông thường, cần tăng giới hạn mặc định:
1. Chuyển sang tab **Configuration** và chọn mục **General configuration** ở menu bên trái.
2. Bấm nút **Edit**.
3. **Memory**: Thay đổi từ `128 MB` thành `256 MB`.
4. **Timeout**: Thay đổi từ `0 min 3 sec` thành `1 min 0 sec`.

![Cấu hình RAM và Timeout](/images/5-Workshop/5.5-Serverless-Lambda/worker-config.png)

5. Bấm **Save**.

#### Bước 3: Thêm Trigger từ SQS
1. Tại phần **Function overview** ở đầu trang, bấm nút **Add trigger**.
2. **Select a source**: Tìm kiếm và chọn **SQS**.
3. **SQS queue**: Chọn đúng ARN của hàng đợi **idp-document-queue**.
4. **Batch size**: Giữ nguyên giá trị mặc định là `10`.

![Cấu hình Trigger SQS](/images/5-Workshop/5.5-Serverless-Lambda/worker-trigger.png)

5. Giữ nguyên các tùy chọn khác và bấm **Add**.

#### Bước 4: Triển khai mã nguồn
1. Chuyển sang tab **Code**, mở tệp tin **.lambda_function.py**..
2. Xóa toàn bộ đoạn mã mặc định và dán đoạn mã nguồn dưới đây:

```python
import json
import boto3
import urllib.parse
import uuid
import datetime

# Khởi tạo client
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
            
            print(f"Bắt đầu xử lý file bằng Textract AI: {object_key} từ {bucket_name}")
            
            # Gọi Textract AI (Tính năng Queries để đặt câu hỏi trực tiếp vào hóa đơn)
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
            
            # Cấu trúc lại kết quả json
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
                                        
            print(f"Kết quả bóc tách thành công: {json.dumps(extracted_data, ensure_ascii=False)}")
            
            # Lưu vào DynamoDB
            item = {
                'documentId': str(uuid.uuid4()),
                'original_filename': object_key,
                'upload_time': datetime.datetime.now().isoformat(),
                'extracted_data': extracted_data
            }
            
            table.put_item(Item=item)
            print("Đã lưu thành công dữ liệu vào DynamoDB!")
            
        return {
            'statusCode': 200,
            'body': json.dumps('Xử lý hoàn tất!')
        }
    except Exception as e:
        print(f"Lỗi: {str(e)}")
        raise e
```
3. Nhấn nút Deploy để kích hoạt mã nguồn mới.
