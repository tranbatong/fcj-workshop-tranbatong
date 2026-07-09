---
title : "Tạo S3 Bucket tiếp nhận dữ liệu"
date : 2024-01-01 
weight : 1
chapter : false
pre : " <b> 5.3.1. </b> "
---

#### Khởi tạo Bucket
Bucket này sẽ lưu trữ an toàn các tài liệu thô do người dùng tải lên trước khi chúng được xử lý bằng AI.

1. Truy cập vào giao diện **Amazon S3** và bấm **Create bucket**.
2. **Bucket name**: Nhập **idp-ingest-bucket-1**.
3. **AWS Region**: Chọn **US East (N. Virginia) us-east-1**.
4. **Object Ownership**: Chọn **ACLs disabled**.
5. **Block Public Access settings for this bucket**: Đảm bảo đang tích chọn **Block all public access**.
![Block Public Access](/images/5-Workshop/5.3-Storage-Database/s3-ingest-block-public-1.png)

6. Các tuỳ chọn còn lại giữ nguyên không thay đổi.
![Block Public Access](/images/5-Workshop/5.3-Storage-Database/s3-ingest-block-public-2.png)
![Block Public Access](/images/5-Workshop/5.3-Storage-Database/s3-ingest-block-public-3.png)
![Block Public Access](/images/5-Workshop/5.3-Storage-Database/s3-ingest-block-public-4.png)

7. Bấm **Create bucket**.

#### Cấu hình CORS
Vì Frontend của chúng ta sẽ tải file trực tiếp lên bucket này, chúng ta phải cấu hình Cross-Origin Resource Sharing (CORS).
1. Bấm vào bucket **idp-ingest-bucket-1** vừa tạo.
2. Chuyển sang tab **Permissions**.
3. Cuộn xuống mục **Cross-origin resource sharing (CORS)** và bấm **Edit**.
4. Dán đoạn cấu hình JSON sau và bấm **Save changes**:

```json
[
  {
    "AllowedHeaders": ["*"],
    "AllowedMethods": ["PUT", "POST", "GET"],
    "AllowedOrigins": ["*"],
    "ExposeHeaders": []
  }
]