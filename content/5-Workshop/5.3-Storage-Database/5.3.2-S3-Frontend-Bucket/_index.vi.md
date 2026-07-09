---
title : "Tạo S3 Bucket cho Frontend"
date : 2024-01-01 
weight : 2
chapter : false
pre : " <b> 5.3.2. </b> "
---

#### Khởi tạo Bucket
Bucket này sẽ được sử dụng để lưu trữ (hosting) mã nguồn ứng dụng web React của bạn.

1. Quay lại danh sách **Amazon S3** bucket và bấm **Create bucket**.
2. **Bucket name**: Nhập **idp-frontend-bucket-1**.
3. **AWS Region**: Chọn **US East (N. Virginia) us-east-1**.
![Unblock Public Access](/images/5-Workshop/5.3-Storage-Database/s3-frontend-public-1.png)

4. **Object Ownership**: Chọn **ACLs disabled**.
5. **Block Public Access settings for this bucket**: **Bỏ tích** ở ô **Block all public access**. 
![Unblock Public Access](/images/5-Workshop/5.3-Storage-Database/s3-frontend-public-2.png)

6. Tích vào ô xác nhận cảnh báo màu vàng để đồng ý rằng bucket này có thể truy cập công khai.
![Unblock Public Access](/images/5-Workshop/5.3-Storage-Database/s3-frontend-public-3.png)

7. Các tuỳ chọn còn lại giữ nguyên không thay đổi. Bấm **Create bucket**.