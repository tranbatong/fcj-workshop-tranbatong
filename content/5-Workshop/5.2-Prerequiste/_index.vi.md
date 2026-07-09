---
title : "Yêu cầu chuẩn bị"
date : 2026-07-01 
weight : 2 
chapter : false
pre : " <b> 5.2. </b> "
---

#### Các yêu cầu trước khi bắt đầu
Trước khi bắt tay vào xây dựng Hệ thống IDP Serverless, vui lòng đảm bảo bạn đã chuẩn bị sẵn sàng các yêu cầu sau:

**1. Tài khoản AWS & Phân quyền**
* Bạn cần có một tài khoản AWS đang hoạt động.
* Đảm bảo bạn đang thao tác tại region **US East (N. Virginia) us-east-1** vì toàn bộ cấu hình trong workshop này đều sử dụng region này.
* Tài khoản (IAM User/Role) của bạn cần có quyền quản trị (Administrator) hoặc có đủ quyền để tạo và quản lý các dịch vụ sau:
    * Amazon S3
    * Amazon DynamoDB
    * Amazon SQS
    * AWS Lambda
    * Amazon API Gateway
    * Amazon Cognito
    * Amazon Textract
    * AWS WAF

**2. Môi trường phát triển trên máy cá nhân**
Để xây dựng và chạy ứng dụng giao diện React, bạn cần cài đặt các công cụ sau trên máy tính của mình:
* **Node.js**: Hãy đảm bảo Node.js (phiên bản 18 trở lên) đã được cài đặt để có thể quản lý các gói thư viện (npm) và chạy server phát triển.
* **Trình soạn thảo mã (Code Editor)**: Cài đặt một trình soạn thảo mã, ví dụ như **Visual Studio Code (VS Code)**, để chỉnh sửa mã nguồn Frontend và mở các tệp dự án.

**3. Chính sách thực thi (Dành riêng cho người dùng Windows)**
Nếu bạn sử dụng Windows, bạn có thể gặp lỗi quyền truy cập khi chạy các lệnh `npm` trong terminal. Để khắc phục, hãy mở PowerShell bằng quyền Administrator và chạy lệnh sau:
```powershell
Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser