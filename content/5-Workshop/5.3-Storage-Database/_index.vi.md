---
title : "Thiết lập Storage & Database"
date : 2026-07-01
weight : 3
chapter : false
pre : " <b> 5.3. </b> "
---

#### Thiết lập Storage & Database

Trong phần này, bạn sẽ khởi tạo các lớp dữ liệu nền tảng cho hệ thống IDP. Quá trình này bao gồm việc tạo nơi lưu trữ cho các tài liệu thô, lưu trữ mã nguồn web tĩnh và cấu hình cơ sở dữ liệu NoSQL để lưu kết quả bóc tách từ AI.

* **Amazon S3**: Sử dụng để lưu trữ tài liệu người dùng tải lên (ingestion) và lưu trữ các tệp tĩnh của giao diện Frontend.
* **Amazon DynamoDB**: Cơ sở dữ liệu NoSQL dùng để lưu trữ dữ liệu có cấu trúc do AI bóc tách, trạng thái thanh toán và quy tắc phân loại danh mục.

#### Nội dung

- [Tạo Ingestion S3 Bucket](1-s3-ingest/)
- [Tạo Frontend S3 Bucket](2-s3-frontend/)
- [Cấu hình S3 Lifecycle Rule](3-s3-lifecycle/)
- [Khởi tạo bảng DynamoDB](4-dynamodb/)