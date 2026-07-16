---
title: "Đề xuất Dự án"
date: 2026-06-17
weight: 2
chapter: false
pre: " <b> 2. </b> "
---
Phần này trình bày ý tưởng đề xuất và kế hoạch triển khai cho dự án sẽ được phát triển trong suốt chương trình **AWS First Cloud AI Journey 2026**.

# Hệ thống Xử lý Tài liệu Thông minh (IDP) Serverless

## Giải pháp Xử lý Tài liệu Thông minh trên AWS Serverless

---

## 1. Tóm tắt Dự án (Executive Summary)

**Hệ thống Xử lý Tài liệu Thông minh (IDP) Serverless** là một ứng dụng web cho phép người dùng tải lên các tài liệu như hóa đơn GTGT, biên lai thanh toán và giấy tờ hành chính. Ngay khi được tải lên, hệ thống sẽ tự động tận dụng các dịch vụ Trí tuệ nhân tạo (AI) của AWS để nhận diện, bóc tách và tổ chức các thông tin quan trọng thành dữ liệu có cấu trúc phục vụ cho mục đích tìm kiếm, báo cáo và quản lý.

Toàn bộ giải pháp được xây dựng trên **Kiến trúc Serverless**, loại bỏ hoàn toàn việc duy trì máy chủ Amazon EC2. Kiến trúc này giúp giảm chi phí vận hành, tự động mở rộng theo khối lượng công việc và đơn giản hóa việc quản lý hạ tầng.

---

## 2. Đặt vấn đề (Problem Statement)
### Thách thức hiện tại
Nhiều tổ chức hiện nay vẫn đang thực hiện nhập liệu thủ công từ hóa đơn và tài liệu kinh doanh. Quá trình này tiêu tốn nhiều thời gian, dễ xảy ra sai sót do con người, và làm cho việc tìm kiếm, báo cáo và phân tích thông tin trở nên khó khăn hơn.

Bên cạnh đó, các hệ thống OCR truyền thống thường yêu cầu máy chủ chuyên dụng, cài đặt phần mềm và bảo trì hạ tầng liên tục, dẫn đến chi phí triển khai và vận hành cao.

### Giải pháp Đề xuất

Nhóm chúng tôi đề xuất một hệ thống Xử lý Tài liệu Thông minh hoàn toàn serverless, được xây dựng 100% trên các dịch vụ đám mây AWS.

Người dùng tương tác với ứng dụng web React được lưu trữ an toàn trên AWS Amplify. Khi tải tài liệu lên, hệ thống sẽ tạo ra các đường dẫn **Amazon S3 Presigned URLs**, cho phép đẩy file trực tiếp vào Amazon S3. Sau khi quá trình tải lên hoàn tất, một luồng xử lý bất đồng bộ (event-driven) sẽ được kích hoạt thông qua Amazon SQS và AWS Lambda. Hàm Lambda AI Worker sẽ gọi dịch vụ Amazon Textract để bóc tách thông tin tài liệu và lưu kết quả có cấu trúc vào Amazon DynamoDB.

Giao diện Frontend giao tiếp với các REST API được đặt trên Amazon API Gateway — được bảo vệ bởi lớp tường lửa AWS WAF — để hiển thị lịch sử hóa đơn, bảng điều khiển thống kê và báo cáo phân tích.

### Lợi ích và Tỷ suất hoàn vốn (ROI)

Giải pháp đề xuất mang lại nhiều ưu điểm vượt trội:

- Tự động hóa hoàn toàn quy trình xử lý tài liệu.
- Giảm thiểu thời gian nhập liệu thủ công.
- Cải thiện độ chính xác của dữ liệu nhờ AI.
- Loại bỏ gánh nặng quản lý máy chủ và tối ưu hóa triển khai nhờ CI/CD.
- Chi phí vận hành thấp với mô hình tính tiền theo mức sử dụng (pay-as-you-go).
- Dễ dàng mở rộng quy mô khi lưu lượng tài liệu tăng cao.

---

## 3. Kiến trúc Giải pháp (Solution Architecture)

Hệ thống được thiết kế theo **Kiến trúc Serverless Điều khiển bằng Sự kiện (Event-Driven)**.

Giao diện React được lưu trữ trên **AWS Amplify**, cung cấp tính năng tự động hóa CI/CD và phân phối bảo mật qua HTTPS. Dịch vụ **Amazon Route 53** được sử dụng để phân giải DNS cho tên miền tùy chỉnh. Để bảo vệ hạ tầng cốt lõi, tường lửa **AWS WAF (Regional)** được đính kèm trực tiếp vào Amazon API Gateway nhằm bảo vệ các API Backend khỏi lưu lượng truy cập độc hại và giới hạn các luồng spam request.

Người dùng xác thực thông qua Amazon Cognito. Sau khi đăng nhập thành công, Amazon API Gateway sẽ kiểm tra tính hợp lệ của JWT token trước khi chuyển tiếp yêu cầu đến các hàm AWS Lambda.

Đối với luồng tải tài liệu, AWS Lambda tạo ra một Presigned URL, cho phép người dùng tải file trực tiếp vào Ingest Bucket của Amazon S3. Mỗi khi có một đối tượng mới được tạo, Amazon S3 sẽ phát ra sự kiện **ObjectCreated** và gửi thông báo vào Amazon SQS. Hàm Lambda AI Worker sẽ lấy tài liệu từ hàng đợi, gửi sang Amazon Textract để phân tích bằng tính năng QUERIES nâng cao, và lưu kết quả JSON bóc tách được vào Amazon DynamoDB.

Nhóm Dashboard APIs sẽ truy xuất hồ sơ hóa đơn và dữ liệu thống kê từ DynamoDB để hiển thị trực quan trên ứng dụng web.

![Architecture Diagram](/images/2-Proposal/diagram2.png)

### Các Dịch vụ AWS Sử dụng

- AWS Amplify
- Amazon Route 53
- AWS WAF
- Amazon S3
- Amazon API Gateway
- Amazon Cognito
- AWS Lambda
- Amazon SQS
- Amazon Textract
- Amazon DynamoDB
- AWS Identity and Access Management (IAM)
- AWS Key Management Service (KMS)
- AWS Budgets

### Thiết kế Thành phần (Component Design)

**Giao diện & Máy chủ lưu trữ (Frontend & Hosting)**
- Ứng dụng React (SPA)
- AWS Amplify (Hosting & CI/CD)
- Amazon Route 53 (DNS)
**Xác thực (Authentication)**
- Amazon Cognito User Pool
- Xác thực JWT
**API Phía sau (Backend API)**
- Amazon API Gateway
- AWS Lambda
**Dịch vụ Tải lên (Upload Service)**
- Amazon S3
- S3 Presigned URL
**Xử lý AI (AI Processing)**
- Amazon SQS
- AWS Lambda AI Worker
- Amazon Textract
**Cơ sở dữ liệu (Database)**
- Amazon DynamoDB
**Bảo mật (Security)**
- AWS WAF (Bảo vệ API)
- AWS IAM
- AWS KMS
**Giám sát (Monitoring)**
- AWS Budgets
---

## 4. Triển khai Kỹ thuật (Technical Implementation)
### Các Giai đoạn Triển khai
Dự án được chia thành 4 giai đoạn chính.
**Giai đoạn 1**
- Phân tích yêu cầu
- Thiết kế kiến trúc AWS
- Phân tích luồng xử lý dữ liệu
**Giai đoạn 2**
- Phát triển Frontend và triển khai lên AWS Amplify
- Tích hợp Amazon Cognito
- Phát triển REST API bằng Amazon API Gateway và AWS Lambda
**Giai đoạn 3**
- Xây dựng luồng tải tài liệu qua Presigned URLs
- Xử lý tài liệu bằng Amazon Textract
- Lưu trữ dữ liệu bóc tách vào Amazon DynamoDB
**Giai đoạn 4**
- Phát triển các tính năng bảng điều khiển (dashboard) và báo cáo
- Kiểm thử hệ thống
- Tối ưu hóa chi phí
- Triển khai phiên bản cuối cùng

### Yêu cầu Kỹ thuật

Các công nghệ bắt buộc bao gồm:

- AWS Lambda
- AWS Amplify
- Amazon Route 53
- Amazon S3
- Amazon API Gateway
- Amazon Cognito
- Amazon Textract
- Amazon DynamoDB
- Amazon SQS
- AWS IAM
- AWS WAF
- ReactJS
- JavaScript
- AWS SDK

---

## 5. Lộ trình & Cột mốc Dự án (Project Roadmap)

- **Trước kỳ thực tập (Tháng 0)**
  - Xác định mục tiêu dự án.
  - Thiết kế kiến trúc AWS tổng thể.
  - Phân tích các dịch vụ AWS và ước tính chi phí hạ tầng.

- **Trong kỳ thực tập (Tháng 1–3)**
  - **Tháng 1**
    - Nghiên cứu các dịch vụ AWS Serverless.
    - Cụ thể hóa kiến trúc hệ thống.
    - Phát triển Frontend và triển khai qua AWS Amplify.

  - **Tháng 2**
    - Xây dựng tính năng tải tài liệu an toàn.
    - Phát triển luồng xử lý AI bất đồng bộ.
    - Tích hợp Amazon Textract và Amazon DynamoDB.

  - **Tháng 3**
    - Xây dựng tính năng bảng điều khiển và báo cáo.
    - Cấu hình AWS WAF và kiểm thử toàn bộ hệ thống.
    - Tối ưu hóa chi phí hạ tầng.
    - Triển khai hệ thống hoàn chỉnh.

- **Sau khi triển khai**
  - Đánh giá hiệu suất hệ thống.
  - Khảo sát các dịch vụ AI khác của AWS để nâng cấp trong tương lai.

---

## 6. Ước tính Ngân sách (Budget Estimation)

Để đảm bảo giải pháp đề xuất có mức chi phí hợp lý trong khi vẫn đáp ứng được các yêu cầu về hiệu suất, khả năng mở rộng và tính sẵn sàng, nhóm đã ước tính chi phí hạ tầng bằng **AWS Pricing Calculator**.

Do sử dụng kiến trúc hoàn toàn serverless, chi phí chỉ phát sinh khi các dịch vụ thực sự được sử dụng. So với việc triển khai dựa trên EC2 truyền thống, điều này giúp giảm đáng kể chi phí hạ tầng.

Bảng tính AWS Pricing Calculator sẽ được cập nhật lại khi kiến trúc môi trường thực tế (production) hoàn thiện.

### Ước tính Chi phí Hạ tầng Hàng tháng

| Dịch vụ AWS | Mục đích | Chi phí Hàng tháng (Ước tính) |
|--------------|---------------------------------------------|----------------:|
| AWS Amplify | Lưu trữ Frontend & CI/CD | 1.00 USD |
| Amazon Route 53 | Quản lý DNS tên miền tùy chỉnh | 0.50 USD |
| Amazon S3 | Lưu trữ tài liệu tải lên | 1.00 USD |
| AWS WAF | Bảo vệ Backend APIs (Regional) | 2.50 USD |
| Amazon API Gateway | Định tuyến REST API | 0.80 USD |
| AWS Lambda | Xử lý Backend và luồng AI | 1.00 USD |
| Amazon Cognito | Xác thực người dùng | 0.00 USD *(Free Tier)* |
| Amazon Textract | OCR và phân tích tài liệu | 4.50 USD |
| Amazon DynamoDB | Lưu trữ dữ liệu hóa đơn | 0.60 USD |
| Amazon SQS | Hàng đợi sự kiện | 0.10 USD |
| AWS KMS | Mã hóa dữ liệu | 0.15 USD |
| AWS Budgets | Giám sát chi phí | 0.00 USD |

### Tổng Chi phí Ước tính

| Khoản mục | Chi phí Ước tính |
|-----------------------------|----------------|
| Chi phí Hạ tầng Hàng tháng | **≈ 12.15 USD / tháng** |
| Chi phí Hạ tầng Hàng năm | **≈ 145.80 USD / năm** |

Vì giải pháp áp dụng mô hình giá **Serverless Pay-as-you-go** (Dùng bao nhiêu trả bấy nhiêu), nó cực kỳ phù hợp cho các dự án nghiên cứu của sinh viên và các đợt triển khai quy mô vừa và nhỏ.

---

## 7. Đánh giá Rủi ro (Risk Assessment)

### Ma trận Rủi ro

- Amazon Textract bóc tách thông tin không chính xác.
- Tải tài liệu thất bại do kết nối Internet không ổn định.
- Chi phí Amazon Textract tăng cao khi khối lượng tài liệu lớn.
- AWS Lambda bị quá thời gian (timeout) khi xử lý các tài liệu quá nặng.

### Chiến lược Giảm thiểu

- Xác thực dữ liệu bóc tách trước khi lưu trữ.
- Sử dụng Amazon SQS để xử lý bất đồng bộ.
- Cấu hình AWS Budgets để giám sát chi phí hạ tầng chặt chẽ.
- Giới hạn kích thước tệp tải lên tối đa.

### Kế hoạch Dự phòng

- Cho phép người dùng tải lại các tài liệu bị lỗi.
- Bật tính năng thử lại tự động (automatic retry) qua Amazon SQS.
- Theo dõi log lỗi bằng Amazon CloudWatch Logs.
- Mã hóa các thông tin nhạy cảm bằng AWS KMS.

---

## 8. Kết quả Mong đợi (Expected Outcomes)

### Cải tiến Kỹ thuật

- Tự động hóa hoàn toàn luồng xử lý tài liệu.
- Giảm đáng kể thời gian nhập liệu thủ công.
- Độ chính xác trích xuất cao nhờ sử dụng Amazon Textract.
- Kiến trúc Serverless có khả năng mở rộng cao tích hợp CI/CD tự động.

### Giá trị Dài hạn

Hệ thống đề xuất có thể được mở rộng để xử lý nhiều loại tài liệu khác nhau như hóa đơn điện tử, giấy phép kinh doanh, căn cước công dân, hợp đồng và các tài liệu có cấu trúc khác.

Hơn thế nữa, nền tảng này cung cấp một cơ sở vững chắc để tích hợp các dịch vụ AI tiên tiến khác của AWS như **Amazon Comprehend** và **Amazon Bedrock** trong tương lai, mở ra khả năng phân tích tài liệu thông minh hơn và thu thập những hiểu biết sâu sắc hơn cho doanh nghiệp.