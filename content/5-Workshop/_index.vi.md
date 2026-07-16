---
title: "Workshop"
date: 2026-07-01
weight: 5
chapter: false
pre: " <b> 5. </b> "
---

# Hệ thống Xử lý Tài liệu Thông minh (IDP) Serverless

#### Tổng quan

**Xử lý Tài liệu Thông minh (Intelligent Document Processing - IDP)** tận dụng Trí tuệ nhân tạo (AI) và Học máy (Machine Learning) để chuyển đổi dữ liệu phi cấu trúc từ các tài liệu (như hóa đơn, biên lai và giấy tờ tùy thân) thành thông tin có cấu trúc và có thể trích xuất được.

Trong workshop này, bạn sẽ học cách xây dựng một hệ thống IDP hoàn toàn serverless (không máy chủ) và điều khiển bằng sự kiện (event-driven) trên AWS. Bằng cách sử dụng các dịch vụ đám mây được quản lý toàn phần (managed services), kiến trúc này đảm bảo tính sẵn sàng cao, tự động mở rộng và xử lý dữ liệu an toàn mà không phải chịu gánh nặng quản lý hạ tầng cơ sở.

Xuyên suốt bài thực hành này, bạn sẽ triển khai và cấu hình nhiều dịch vụ AWS ở các tầng kiến trúc khác nhau:
* **Lưu trữ & Cơ sở dữ liệu:** Amazon S3 để tiếp nhận tài liệu và DynamoDB để lưu trữ dữ liệu có cấu trúc sau khi bóc tách.
* **Xử lý Bất đồng bộ:** Amazon SQS và AWS Lambda để tách biệt khối lượng công việc tải file khỏi quá trình xử lý bóc tách của AI.
* **Trí tuệ nhân tạo / Học máy (AI/ML):** Amazon Textract để tự động truy vấn và bóc tách các trường thông tin cụ thể từ hình ảnh và file PDF được tải lên.
* **Bảo mật & Xác thực:** Amazon Cognito để quản lý định danh người dùng, API Gateway để định tuyến các RESTful API, và AWS WAF để giới hạn lưu lượng (rate-limiting) bảo vệ hệ thống khỏi các cuộc tấn công.
* **Giao diện (Frontend) & CI/CD:** Ứng dụng React Single-Page Application (SPA) được lưu trữ trên AWS Amplify tích hợp sẵn luồng CI/CD tự động, kết hợp cùng tên miền tùy chỉnh quản lý bởi Amazon Route 53 để tương tác an toàn với Backend API thông qua HTTPS.

#### Nội dung

1. [Tổng quan Workshop](5.1-Workshop-overview/)
2. [Điều kiện tiên quyết](5.2-Prerequisite/)
3. [Thiết lập Lưu trữ & Cơ sở dữ liệu](5.3-Storage-Database/)
4. [Cấu hình Hàng đợi Messaging & IAM](5.4-Messaging-IAM/)
5. [Thiết lập Serverless Backend với Lambda](5.5-Lambda-Functions/)
6. [Xác thực người dùng với Cognito](5.6-Identity-Cognito/)
7. [Bảo mật hệ thống với API Gateway & WAF](5.7-API-Gateway-WAF/)
8. [Triển khai React Frontend](5.8-Frontend-React/)
9. [Cấu hình tên miền tùy chỉnh với Amazon Route 53](5.9-Route53-Domain/)
10. [Tích hợp CI/CD & Triển khai Giao diện với AWS Amplify](5.10-Amplify-Hosting/)
11. [Kiểm thử & Xác thực](5.11-Testing-Validation/)