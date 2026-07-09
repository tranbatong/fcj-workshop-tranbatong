---
title : "Cấu hình Hàng đợi & Phân quyền IAM"
date : 2026-07-01
weight : 4
chapter : false
pre : " <b> 5.4. </b> "
---

#### Cấu hình Hàng đợi & Phân quyền IAM

Trong phần này, bạn sẽ thiết lập lớp nhắn tin bất đồng bộ (asynchronous messaging) và các quyền bảo mật cần thiết để backend serverless của bạn hoạt động chính xác.

Thay vì xử lý tài liệu đồng bộ ngay lập tức (dễ gây ra lỗi timeout), chúng ta sẽ sử dụng **Amazon SQS** làm bộ đệm chứa lệnh. Hơn nữa, tuân thủ nguyên tắc đặc quyền tối thiểu, bạn sẽ tạo một **AWS IAM Role** cụ thể để cấp cho các hàm Lambda vừa đủ quyền tương tác với S3, DynamoDB, SQS và các dịch vụ AI.

#### Nội dung

- [Tạo hàng đợi SQS](1-sqs/)
- [Tạo IAM Role](2-iam-role/)