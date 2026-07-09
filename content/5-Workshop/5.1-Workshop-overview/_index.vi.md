---
title : "Giới thiệu"
date: 2026-07-01
weight : 1 
chapter : false
pre : " <b> 5.1. </b> "
---

#### Xử lý Tài liệu Thông minh (IDP)
**Xử lý Tài liệu Thông minh (Intelligent Document Processing - IDP)** ứng dụng Trí tuệ Nhân tạo (AI) và Học máy (ML) để tự động trích xuất, phân loại và cấu trúc hóa dữ liệu từ các tài liệu thô như hóa đơn và biên lai. Việc sử dụng kiến trúc serverless (không máy chủ) giúp hệ thống tự động mở rộng, giảm thiểu thao tác nhập liệu thủ công và tối ưu chi phí quản trị hạ tầng.

#### Tổng quan Workshop
Trong workshop này, thay vì sử dụng mạng VPC hay môi trường on-premises truyền thống, bạn sẽ xây dựng một kiến trúc IDP hoàn toàn serverless trên AWS. Bạn sẽ khởi tạo và tích hợp các thành phần cốt lõi sau:

* **Lưu trữ & Cơ sở dữ liệu:** Bạn sẽ tạo các bucket Amazon S3 (**idp-ingest-bucket-1** để nhận file thô và **idp-frontend-bucket-1** để lưu trữ mã nguồn web). Bạn cũng sẽ triển khai các bảng Amazon DynamoDB (**InvoicesData**, **InvoicesPayments**, và **UserCategories**) để lưu trữ dữ liệu sau khi bóc tách.

* **Xử lý bất đồng bộ:** Một hàng đợi Amazon SQS (**idp-document-queue**) sẽ đóng vai trò làm bộ đệm kết nối giữa sự kiện tải file lên S3 và logic xử lý.

* **Tính toán & AI:** Các hàm AWS Lambda (**idp-ai-worker**) sẽ xử lý tài liệu đầu vào bằng cách gọi Amazon Textract để truy vấn và trích xuất các trường thông tin cụ thể.

* **Bảo mật & API:** Backend của hệ thống sẽ được giao tiếp thông qua Amazon API Gateway (**idp-rest-api**). Bạn sẽ bảo mật ứng dụng bằng Amazon Cognito (**idp-react-app**) để xác thực người dùng và dùng AWS WAF (**idp-api-waf-shield**) để chặn các yêu cầu spam.

* **Giao diện (Frontend):** Một ứng dụng React (SPA) sẽ được xây dựng để xử lý việc tải file lên qua presigned URL và trực quan hóa dữ liệu đã xử lý thông qua các biểu đồ tương tác.

![overview](/images/5-Workshop/5.1-Workshop-overview/diagram1.png)