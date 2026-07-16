---
title : "Giới thiệu"
date: 2026-07-01
weight : 1 
chapter : false
pre : " <b> 5.1. </b> "
---

#### Xử lý Tài liệu Thông minh (IDP)
**Xử lý Tài liệu Thông minh (IDP)** tận dụng Trí tuệ nhân tạo (AI) và Học máy (ML) để tự động trích xuất, phân loại và cấu trúc hóa dữ liệu từ các tài liệu thô như hóa đơn và biên lai. Bằng cách sử dụng kiến trúc serverless, hệ thống này tự động mở rộng, giảm thiểu nhập liệu thủ công và tối ưu hóa chi phí quản lý hạ tầng.

#### Tổng quan Workshop
Trong workshop này, bạn sẽ xây dựng một kiến trúc IDP serverless hoàn toàn dựa trên sự kiện (event-driven) trên AWS. Bạn sẽ triển khai và tích hợp các thành phần cốt lõi sau:

* **Lưu trữ & Cơ sở dữ liệu:** Bạn sẽ tạo một Amazon S3 bucket (**idp-ingest-bucket**) để tiếp nhận tài liệu. Bạn cũng sẽ triển khai các bảng Amazon DynamoDB (**InvoicesData**, **InvoicesPayments** và **UserCategories**) để lưu trữ dữ liệu đã được bóc tách.
* **Hàng đợi Bất đồng bộ:** Amazon SQS queue (**idp-document-queue**) sẽ đóng vai trò là bộ đệm giữa quá trình upload lên S3 và logic xử lý AI.
* **Tính toán & AI:** Các hàm AWS Lambda (**idp-ai-worker**) sẽ xử lý tài liệu bằng cách gọi Amazon Textract để truy vấn và trích xuất các trường văn bản cụ thể.
* **Bảo mật & API:** Backend hệ thống sẽ được cung cấp thông qua Amazon API Gateway (**idp-rest-api**). Bạn sẽ bảo mật ứng dụng bằng Amazon Cognito để xác thực người dùng và AWS WAF (**idp-api-waf-shield**) để chặn các request spam và tấn công.
* **Giao diện & Triển khai:** Ứng dụng React Single-Page Application (SPA) sẽ được triển khai thông qua **AWS Amplify** với quy trình CI/CD tự động. Cấu hình tên miền tùy chỉnh sử dụng **Amazon Route 53** để tương tác an toàn với Backend API thông qua HTTPS.

![overview](/images/5-Workshop/5.1-Workshop-overview/diagram2.png)