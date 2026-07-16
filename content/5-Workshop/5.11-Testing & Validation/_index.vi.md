---
title : "Kiểm thử & Đánh giá"
date : 2026-07-01
weight : 11
chapter : false
pre : " <b> 5.11. </b> "
---

#### 1. Chiến lược Kiểm thử Hệ thống (Testing Strategy)

Sau khi hoàn tất quá trình triển khai CI/CD qua AWS Amplify, việc kiểm thử toàn diện từ đầu đến cuối (End-to-End Testing) là bắt buộc. Quá trình đánh giá này nhằm đảm bảo tính toàn vẹn của dòng chảy dữ liệu (Data Flow), khả năng phản hồi của kiến trúc Serverless, cũng như độ tin cậy của các rào chắn bảo mật (WAF & Cognito).

#### 2. Kịch bản Kiểm thử Chức năng & Tích hợp (Functional & Integration Test Cases)

Bảng dưới đây trình bày các kịch bản kiểm thử cốt lõi đi theo đúng vòng đời của một luồng xử lý tài liệu thông minh:

| Mã TC | Hạng mục | Kịch bản kiểm thử (Test Scenario) | Kết quả mong đợi (Expected Result) |
| :--- | :--- | :--- | :--- |
| **TC-01** | **Xác thực (Cognito)** | Đăng nhập hệ thống bằng tài khoản hợp lệ đã xác minh. | Trình duyệt nhận được JWT Token, lưu trữ an toàn và chuyển hướng thành công vào trang Dashboard. |
| **TC-02** | **Bảo mật (AWS WAF)** | Gửi liên tục hơn 100 requests trong vòng 5 phút vào API Gateway để giả lập Spam/DDoS. | Rule `BlockSpamIP` của WAF được kích hoạt, chặn request và trả về mã lỗi `403 Forbidden`. |
| **TC-03** | **Upload (API & S3)** | Tải lên một file hóa đơn (JPG/PDF). Hệ thống gọi API `GET /get-upload-url`. | Lambda sinh Presigned URL thành công. File được đẩy trực tiếp vào thư mục `uploads/` của S3 Bucket mà không bị lỗi CORS. |
| **TC-04** | **Xử lý AI (Textract)** | Giám sát luồng Event-Driven khi file vừa vào S3, kích hoạt SQS và Lambda AI-Worker. | AI bóc tách chính xác các trường `QUERIES` (Mã hóa đơn, Tên nhà cung cấp, Tổng tiền, Ngày tháng) và lưu thành công cấu trúc JSON vào DynamoDB. |
| **TC-05** | **Bảo mật Dữ liệu** | Gọi API `GET /invoices` để truy xuất danh sách hóa đơn lên Dashboard. | Dữ liệu nhạy cảm được che giấu (Data Masking) thành công (VD: Mã số thuế hiển thị dưới dạng `******xxxx`). |
| **TC-06** | **Giao diện (React)** | Thay đổi các bộ lọc (Tìm kiếm, Sắp xếp theo danh mục) trên giao diện Web. | UI phản hồi tức thời, biểu đồ thống kê (Doanh thu theo tháng, Nhà cung cấp) cập nhật số liệu khớp với cơ sở dữ liệu DynamoDB. |

#### 3. Đánh giá Khả năng Đáp ứng (Validation & Evaluation)

*   **Tính sẵn sàng cao (High Availability):** Hạ tầng Serverless (Lambda, DynamoDB On-demand, SQS) tự động mở rộng (auto-scale) theo từng batch dữ liệu (Batch size: 10), đảm bảo không xảy ra hiện tượng thắt cổ chai (bottleneck) khi có nhiều người dùng tải hóa đơn cùng lúc.
*   **Chi phí tối ưu (Cost Optimization):** S3 Lifecycle Rule tự động dọn dẹp các bản chụp hóa đơn gốc (Raw Invoices) sau 1 ngày, giúp nhóm tiết kiệm tối đa chi phí lưu trữ dài hạn trong khi vẫn giữ lại được dữ liệu JSON giá trị trên DynamoDB.