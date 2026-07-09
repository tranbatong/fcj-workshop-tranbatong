---
title : "Tạo REST API & Resources"
date : 2026-07-01
weight : 1
chapter : false
pre : " <b> 5.7.1. </b> "
---

#### Bước 1: Khởi tạo REST API
1. Truy cập giao diện **API Gateway**.
2. Tìm đến mục **REST API** (đảm bảo không chọn nhầm loại Private) và bấm **Build**.
3. Chọn **New API**.
4. **API name**: Nhập `idp-backend-api`.
5. **Endpoint Type**: Chọn **Regional**.

![Create API Gateway](/images/5-Workshop/5.6-API-Gateway/create-api.png)

6. Bấm **Create API**.

#### Bước 2: Tạo Resources và Methods
Chúng ta cần tạo các đường dẫn URL để gọi tới 5 hàm Lambda API.

Hãy làm theo quy trình sau cho điểm cuối (endpoint) đầu tiên:
1. Bấm vào đường dẫn gốc.
2. Bấm **Create resource**.
3. **Resource Name**: Nhập `get-upload-url` (Hệ thống sẽ tự tạo đường dẫn **./get-upload-url**.). Bấm **Create resource**.
4. Bấm chọn resource **./get-upload-url**. vừa tạo, sau đó bấm **Create method**.

![API Gateway Method](/images/5-Workshop/5.7-API-Gateway-WAF/api-resource.png)

5. **Method type**: Chọn **GET**.
6. **Integration type**: Chọn **Lambda function**.
7. **Lambda proxy integration**: **BẮT BUỘC TÍCH CHỌN** (Bật tính năng này).
8. **Lambda function**: Chọn hàm `idp-api-presign`.
9. Bấm **Create method**.

![API Gateway Method](/images/5-Workshop/5.7-API-Gateway-WAF/api-method.png)

#### Lặp lại cho các endpoint còn lại
Thực hiện lặp lại quy trình trên để tạo các Resource và Method GET tương ứng:
* Resource `/invoices` -> Method GET -> Lambda: `idp-api-get-invoices`
* Resource `/stats` -> Method GET -> Lambda: `idp-api-get-stats`
* Resource `/categories` -> Method GET -> Lambda: `idp-api-categories`
* Resource `/payments` -> Method GET -> Lambda: `idp-api-payments`

*(Đảm bảo tất cả đều được tích chọn **Lambda proxy integration**!)*