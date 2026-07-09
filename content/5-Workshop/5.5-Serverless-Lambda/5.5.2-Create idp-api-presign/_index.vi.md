---
title : "Tạo hàm idp-api-presign"
date : 2026-07-01
weight : 2
chapter : false
pre : " <b> 5.5.2. </b> "
---

Hàm **idp-api-presign** chịu trách nhiệm tạo ra một URL ký trước (Presigned URL) có thời hạn ngắn, giúp ứng dụng React Frontend có thể tải tài liệu lên S3 một cách bảo mật mà không cần để lộ khóa truy cập AWS.

#### Bước 1: Khởi tạo hàm Lambda
1. Truy cập giao diện **AWS Lambda** và bấm **Create function**.
2. Chọn mục **Author from scratch**.
3. **Function name**: Nhập `idp-api-presign`.
4. **Runtime**: Chọn **Python 3.12**.
5. Bấm nút **Create function**.

#### Bước 2: Cấp quyền ghi S3 cho Execution Role của hàm
Vì hàm này cần thực hiện quyền sinh URL cho phép tải tệp tin lên S3, chúng ta cần cấp thêm chính sách truy cập đầy đủ vào S3 cho vai trò thực thi riêng biệt của nó:
1. Chuyển sang tab **Configuration** và chọn mục **Permissions** ở thực đơn bên trái.
2. Tại mục **Execution role**, nhấn chuột vào liên kết màu xanh có định dạng **idp-api-presign-role-xxxx**.

![Liên kết vai trò thực thi](/images/5-Workshop/5.5-Serverless-Lambda/presign-role.png)

3. Tại tab giao diện quản lý IAM vừa mở rộng, bấm nút **Add permissions** và chọn **Attach policies**.
4. Nhập `AmazonS3FullAccess` vào ô tìm kiếm, tích chọn chính sách này.

![Gắn quyền S3 Full Access](/images/5-Workshop/5.5-Serverless-Lambda/attach-s3-access.png)

5. Cuộn xuống cuối trang và bấm nút **Add permissions** để hoàn tất việc gán quyền.

#### Bước 3: Triển khai mã nguồn
1. Quay lại màn hình giao diện của hàm Lambda **idp-api-presign**, chuyển sang tab **Code**.
2. Mở file **lambda_function.py**, xóa mã nguồn mặc định và dán đoạn mã xử lý dưới đây:

```python
import json
import boto3
import uuid

s3_client = boto3.client('s3')
# ĐẢM BẢO TÊN BUCKET NÀY ĐÚNG VỚI BUCKET CỦA BẠN
BUCKET_NAME = 'idp-ingest-bucket-1'

def lambda_handler(event, context):
    try:
        # 1. Đọc chính xác loại file từ React gửi lên (Hỗ trợ Lambda Proxy)
        query_params = event.get('queryStringParameters') or {}
        content_type = query_params.get('contentType', 'image/jpeg') # Mặc định là jpeg nếu không có
        
        # Tạo tên file ngẫu nhiên
        file_extension = content_type.split('/')[-1]
        file_name = f"uploads/{uuid.uuid4()}.{file_extension}"
        
        # 2. Đóng dấu chữ ký Content-Type chuẩn xác vào vé
        presigned_url = s3_client.generate_presigned_url(
            'put_object',
            Params={
                'Bucket': BUCKET_NAME,
                'Key': file_name,
                'ContentType': content_type # Dòng chốt hạ chống lỗi 403
            },
            ExpiresIn=300
        )
        
        return {
            'statusCode': 200,
            'headers': {
                'Access-Control-Allow-Origin': '*'
            },
            'body': json.dumps({
                'upload_url': presigned_url
            })
        }
    except Exception as e:
        return {
            'statusCode': 500,
            'body': json.dumps({'error': str(e)})
        }
```

3. Nhấn nút Deploy để kích hoạt mã nguồn mới.