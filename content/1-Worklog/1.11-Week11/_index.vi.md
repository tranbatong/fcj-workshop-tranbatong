---
title: "Worklog Tuần 11"
date: 2026-06-29
weight: 11
chapter: false
pre: " <b> 1.11. </b> "
---

### Mục tiêu tuần 11:

- Cập nhật lại kiến trúc dự án dựa trên các yêu cầu phát sinh mới: mở rộng Dashboard APIs Layer.
- Triển khai luồng xử lý AI lõi (IDP Processing Workflow) tích hợp Amazon Textract để nhận diện và trích xuất dữ liệu tài liệu tự động.
- Xây dựng tầng API Dashboard (gồm 4 hàm Lambda) và thiết lập Amazon API Gateway để phục vụ dữ liệu cho ứng dụng Frontend.

### Các công việc cần triển khai trong tuần này:

| Thứ | Công việc                                                                                                                                                                                                                                                     | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu                           |
| --- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------ | --------------- | ---------------------------------------- |
| 2   | Đánh giá yêu cầu phát sinh, mở rộng thiết kế Dashboard APIs Layer từ 2 lên 4 hàm Lambda (thêm API-Get-Category và API-Get-Payment).                                           | 29/06/2026   | 29/06/2026      | Yêu cầu dự án, AWS Architecture          |
| 3   | Triển khai hàm AWS Lambda AI-Worker để xử lý tài liệu. Cấu hình cấp quyền (IAM Policy) và thiết lập trigger từ Amazon SQS để tự động kích hoạt AI-Worker khi có thông điệp mới.                                                               | 30/06/2026   | 30/06/2026      | AWS Documentation, Khóa học FCJ          |
| 4   | Tích hợp SDK của Amazon Textract (AnalyzeDocument API) vào hàm AI-Worker. Xử lý dữ liệu văn bản trích xuất được và chuẩn hóa thành định dạng JSON. Viết mã kết nối và lưu trữ file JSON kết quả vào bảng Amazon DynamoDB.                     | 01/07/2026   | 01/07/2026      | Amazon Textract Developer Guide          |
| 5   | Phát triển 4 hàm Lambda thuộc tầng Dashboard APIs Layer: API-Get-Invoices, API-Get-Stats, API-Get-Category, API-Get-Payment. Tối ưu hóa các tác vụ Scan/Query từ DynamoDB để trả về dữ liệu nhanh chóng cho Dashboard.                        | 02/07/2026   | 02/07/2026      | Boto3 Documentation, DynamoDB Best Practices |
| 6   | Khởi tạo Amazon API Gateway (REST API) và tạo các resources/methods (GET /invoices, /stats, v.v.). Tích hợp API Gateway với 4 hàm Lambda tương ứng và bật CORS (Cross-Origin Resource Sharing) để Frontend có thể gọi API.                    | 03/07/2026   | 03/07/2026      | AWS Console, API Gateway Guide           |
| 7   | Kiểm tra toàn bộ luồng (End-to-End): Upload file, SQS, AI-Worker, Textract, DynamoDB, API Gateway. Ghi nhận các lỗi phát sinh (nếu có) và chuẩn bị kế hoạch triển khai bảo mật (Cognito, WAF) cho tuần 12.                                    | 04/07/2026   | 04/07/2026      | <https://cloudjourney.awsstudygroup.com/>|

### Kết quả đạt được tuần 11:

| Thứ | Công việc                                                  | Kết quả đạt được                                                                                                                                                                                                                                                  |
| --- | ---------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 2   | Cập nhật kiến trúc dự án                                   | Đã hoàn thiện sơ đồ kiến trúc mới và thiết kế chi tiết 4 hàm Lambda mới phục vụ cho Dashboard APIs Layer.                                                                                                                        |
| 3   | Triển khai Lambda AI-Worker và SQS Trigger                 | Tạo thành công hàm AI-Worker với các IAM Policy cần thiết (quyền đọc SQS, gọi Textract, ghi DynamoDB). Thiết lập thành công SQS trigger để kích hoạt Lambda ngay khi có file upload.                                                                              |
| 4   | Tích hợp Amazon Textract và DynamoDB                       | AI-Worker đã gọi thành công Amazon Textract để phân tích tài liệu và bóc tách dữ liệu chính xác. Dữ liệu thô được chuyển đổi thành JSON chuẩn và lưu trữ thành công vào bảng Amazon DynamoDB.                                                                    |
| 5   | Xây dựng tầng Dashboard APIs Layer                         | Code và deploy thành công 4 hàm Lambda độc lập. Các hàm này đã thực hiện chính xác các thao tác Scan/Query trên DynamoDB để lấy dữ liệu thống kê, danh mục, thanh toán và danh sách hóa đơn.                                                                      |
| 6   | Thiết lập Amazon API Gateway                               | Xây dựng thành công REST API với đầy đủ các routes cần thiết. Đã cấu hình tích hợp thành công giữa API Gateway và các hàm Lambda, xử lý xong lỗi CORS giúp Frontend lấy được dữ liệu.                                                                             |
| 7   | Kiểm thử End-to-End luồng xử lý và ghi nhận                | Luồng xử lý IDP hoạt động trơn tru từ đầu đến cuối. Textract nhận diện tốt các hóa đơn mẫu. Đã lập danh sách các công việc còn lại (WAF, Cognito) để bảo mật hệ thống trong tuần cuối cùng.                                                                      |

---

### Hình ảnh minh chứng thực tế:

![alt text](image.png)