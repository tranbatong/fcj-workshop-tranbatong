---
title: "Workshop"
date: 2026-07-01
weight: 5
chapter: false
pre: " <b> 5. </b> "
---

# Hệ thống Xử lý Tài liệu Thông minh (IDP) Serverless

#### Tổng quan

**Xử lý Tài liệu Thông minh (Intelligent Document Processing - IDP)** ứng dụng AI và Học máy (Machine Learning) để chuyển đổi dữ liệu phi cấu trúc từ các tài liệu (như hóa đơn, biên lai, thẻ căn cước) thành thông tin có cấu trúc và có thể sử dụng được.

Trong workshop này, bạn sẽ học cách xây dựng một hệ thống IDP hoàn toàn serverless (không máy chủ) và hướng sự kiện (event-driven) trên AWS. Bằng cách sử dụng các dịch vụ được quản lý (managed services), kiến trúc này đảm bảo tính sẵn sàng cao, khả năng tự động mở rộng và xử lý dữ liệu an toàn mà không cần quản trị hạ tầng.

Trong suốt bài thực hành này, bạn sẽ triển khai và cấu hình các dịch vụ AWS ở nhiều tầng khác nhau:
* **Lưu trữ & Cơ sở dữ liệu:** Amazon S3 để tiếp nhận tài liệu và DynamoDB để lưu trữ dữ liệu đã trích xuất.
* **Xử lý bất đồng bộ:** Amazon SQS và AWS Lambda giúp tách biệt (decouple) quá trình tải file với khối lượng công việc trích xuất AI.
* **Trí tuệ Nhân tạo (AI/ML):** Amazon Textract để tự động bóc tách các trường thông tin cụ thể từ hình ảnh và tệp PDF tải lên.
* **Bảo mật & Xác thực:** Amazon Cognito để quản lý người dùng, API Gateway để định tuyến RESTful và AWS WAF để giới hạn tần suất truy cập (rate-limiting) và bảo vệ hệ thống.
* **Giao diện (Frontend):** Một ứng dụng React (SPA) để giao tiếp với các API Backend, tải file lên qua presigned URL và trực quan hóa dữ liệu bằng Dashboard.

#### Nội dung

1. [Tổng quan Workshop](5.1-Workshop-overview/)
2. [Yêu cầu chuẩn bị](5.2-Prerequisite/)
3. [Thiết lập Lưu trữ & Cơ sở dữ liệu](5.3-Storage-Database/)
4. [Cấu hình Hàng đợi & Phân quyền IAM](5.4-Messaging-IAM/)
5. [Backend Serverless với Lambda](5.5-Lambda-Functions/)
6. [Xác thực với Cognito](5.6-Identity-Cognito/)
7. [API Gateway & Bảo mật WAF](5.7-API-Gateway-WAF/)
8. [Triển khai giao diện React](5.8-Frontend-React/)
9. [Kiểm thử & Xác nhận kết quả](5.9-Testing-Validation/)
10. [Dọn dẹp tài nguyên](5.10-Cleanup/)