---
title : "Backend Serverless với Lambda"
date : 2026-07-01
weight : 5
chapter : false
pre : " <b> 5.5. </b> "
---

#### Backend Serverless với Lambda

Trong phần này, bạn sẽ cấu hình và triển khai lớp xử lý logic trung tâm (Backend Serverless) bằng dịch vụ **AWS Lambda**. Hệ thống bóc tách tài liệu tự động (IDP) sẽ sử dụng các hàm Lambda chạy trên môi trường Python 3.12 để tiếp nhận thông điệp, bóc tách văn bản bằng AI và cung cấp dữ liệu cho giao diện người dùng qua API.

#### Nội dung

- [Tạo hàm idp-ai-worker](1-ai-worker/)
- [Tạo hàm idp-api-presign](2-api-presign/)
- [Tạo hàm idp-api-get-invoices](3-api-get-invoices/)
- [Tạo hàm idp-api-get-stats](4-api-get-stats/)
- [Tạo hàm idp-api-categories](5-api-categories/)
- [Tạo hàm idp-api-payments](6-api-payments/)