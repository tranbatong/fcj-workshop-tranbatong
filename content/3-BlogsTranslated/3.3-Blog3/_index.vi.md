---
title: "Bài viết 3"
date: 2026-06-30
weight: 4
chapter: false
pre: " <b> 3.3. </b> "
---

# Sử dụng Generative AI để tự động sinh mã Infrastructure as Code (IaC) tuân thủ Service Control Policies với Amazon Bedrock

**Infrastructure as Code (IaC)** đã trở thành một phương pháp quan trọng trong việc quản lý hạ tầng đám mây, cho phép triển khai và cấu hình tài nguyên thông qua mã nguồn thay vì thao tác thủ công. Các công cụ như **Terraform** và **AWS CloudFormation** giúp việc triển khai hạ tầng trở nên nhất quán, dễ tự động hóa và dễ mở rộng.

Tuy nhiên, đối với các tổ chức sử dụng **AWS Organizations**, mọi tài nguyên được triển khai đều phải tuân thủ các **Service Control Policies (SCPs)**. Đây là các chính sách quy định phạm vi quyền tối đa mà các tài khoản AWS được phép sử dụng. Việc tự viết hoặc rà soát mã IaC để đáp ứng các SCP thường mất nhiều thời gian, dễ xảy ra sai sót và tiềm ẩn nhiều rủi ro về bảo mật.

Để giải quyết vấn đề này, AWS đã giới thiệu một kiến trúc kết hợp **Amazon Bedrock** cùng các dịch vụ serverless nhằm tự động sinh mã Infrastructure as Code từ yêu cầu bằng ngôn ngữ tự nhiên, đồng thời đảm bảo mã được tạo ra luôn tuân thủ các chính sách của tổ chức.

---

# Kiến trúc giải pháp

![Kiến trúc tổng thể tuân thủ Service Control Polices](image.png)

**Hình 1. Kiến trúc tổng thể của hệ thống sinh mã Infrastructure as Code tuân thủ Service Control Policies.**

Giải pháp bao gồm hai quy trình chính:

1. Quy trình đồng bộ Service Control Policies.
2. Quy trình sinh Infrastructure as Code bằng Generative AI.

Hai quy trình này phối hợp với nhau để đảm bảo mọi đoạn mã được tạo ra luôn sử dụng phiên bản chính sách mới nhất của tổ chức.

---

# Quy trình đồng bộ Service Control Policies

Trong thực tế, các **Service Control Policies** thường xuyên được cập nhật khi doanh nghiệp bổ sung các yêu cầu bảo mật hoặc thay đổi quy định quản trị.

Thay vì phải cập nhật thủ công cho hệ thống AI, kiến trúc này tự động đồng bộ các thay đổi thông qua các dịch vụ AWS.

Quy trình hoạt động như sau:

1. Quản trị viên tạo mới hoặc cập nhật một Service Control Policy.
2. AWS CloudTrail ghi nhận sự kiện thay đổi.
3. Amazon EventBridge phát hiện sự kiện này.
4. EventBridge kích hoạt một hàm AWS Lambda.
5. Lambda đọc nội dung Service Control Policy vừa thay đổi.
6. Chính sách mới được lưu vào Amazon S3.

Nhờ vậy, dữ liệu chính sách luôn được cập nhật và sẵn sàng làm nguồn tham chiếu khi sinh mã Infrastructure as Code.

---

# Quy trình sinh Infrastructure as Code

Khi lập trình viên muốn tạo hạ tầng mới, họ chỉ cần mô tả yêu cầu bằng ngôn ngữ tự nhiên.

Ví dụ:

> "Tạo một Amazon S3 Bucket bảo mật để lưu trữ log của ứng dụng."

Quy trình xử lý diễn ra như sau:

1. Người dùng gửi yêu cầu thông qua API được cung cấp bởi Amazon API Gateway.
2. API Gateway gọi đến AWS Lambda.
3. Lambda lấy các Service Control Policies mới nhất từ Amazon S3.
4. Nội dung yêu cầu của người dùng được kết hợp với các chính sách của tổ chức để tạo thành một Prompt hoàn chỉnh.
5. Prompt được gửi tới Amazon Bedrock.
6. Foundation Model phân tích yêu cầu hạ tầng cùng với các quy định bảo mật.
7. Amazon Bedrock sinh ra mã Infrastructure as Code (ví dụ: Terraform) vừa đáp ứng yêu cầu chức năng, vừa tuân thủ Service Control Policies.
8. Đoạn mã được trả về cho người dùng.

Nhờ được cung cấp đầy đủ ngữ cảnh về chính sách của tổ chức, mô hình AI có thể sinh ra các đoạn mã phù hợp ngay từ lần đầu, giúp giảm đáng kể việc chỉnh sửa sau này.

---

# Vai trò của Amazon Bedrock

Amazon Bedrock là dịch vụ cung cấp các **Foundation Models** thông qua API mà không cần người dùng tự quản lý hạ tầng Machine Learning.

Trong kiến trúc này, Amazon Bedrock có nhiệm vụ:

- Hiểu yêu cầu hạ tầng được mô tả bằng ngôn ngữ tự nhiên.
- Phân tích các Service Control Policies của tổ chức.
- Kết hợp yêu cầu của người dùng với các chính sách hiện có.
- Sinh mã Infrastructure as Code theo đúng yêu cầu.
- Đề xuất các cấu hình phù hợp với các thực hành tốt của AWS.

Có thể xem Amazon Bedrock như một trợ lý AI hỗ trợ lập trình viên tạo mã IaC nhanh hơn nhưng vẫn đảm bảo các quy định quản trị của tổ chức.

---

# Lợi ích của việc cập nhật Service Control Policies tự động

Một trong những ưu điểm nổi bật của giải pháp là khả năng tự động đồng bộ các thay đổi của Service Control Policies.

Mỗi khi quản trị viên chỉnh sửa chính sách:

- AWS CloudTrail ghi nhận sự kiện.
- Amazon EventBridge tự động phát hiện.
- AWS Lambda xử lý nội dung chính sách mới.
- Amazon S3 lưu phiên bản mới nhất.

Nhờ đó:

- Mọi yêu cầu sinh mã đều sử dụng các quy định mới nhất.
- Không cần cập nhật thủ công Prompt.
- Giảm nguy cơ sử dụng các chính sách lỗi thời.

---

# Kiến trúc bảo mật

Bảo mật được tích hợp ngay từ đầu trong toàn bộ hệ thống.

## Amazon Cognito

Amazon Cognito chịu trách nhiệm xác thực và quản lý danh tính người dùng trước khi họ có thể sử dụng dịch vụ sinh mã Infrastructure as Code.

Các chức năng chính gồm:

- Xác thực người dùng.
- Quản lý danh tính.
- Kiểm soát quyền truy cập.
- Bảo vệ API.

Chỉ những người dùng được cấp quyền mới có thể gửi yêu cầu tới hệ thống.

---

## AWS WAF

AWS WAF được triển khai phía trước Amazon API Gateway nhằm bảo vệ API khỏi các cuộc tấn công từ Internet.

AWS WAF có khả năng ngăn chặn:

- SQL Injection.
- Cross-site Scripting (XSS).
- Các HTTP Request độc hại.
- Tấn công từ Bot.
- Tấn công từ chối dịch vụ (DDoS).

Nhờ lớp bảo vệ này, hệ thống AI có thể hoạt động an toàn hơn khi được cung cấp dưới dạng dịch vụ công khai.

---

# Lợi ích của giải pháp

So với cách viết Infrastructure as Code thủ công, giải pháp mang lại nhiều lợi ích:

- Tự động sinh mã Infrastructure as Code từ ngôn ngữ tự nhiên.
- Đảm bảo mã sinh ra tuân thủ Service Control Policies.
- Tự động cập nhật khi chính sách thay đổi.
- Giảm thời gian phát triển hạ tầng.
- Hạn chế lỗi do con người.
- Tăng cường khả năng quản trị hệ thống.
- Nâng cao mức độ bảo mật.
- Đẩy nhanh quá trình triển khai hạ tầng.

---

# Một số lưu ý khi triển khai

Để hệ thống hoạt động hiệu quả, cần lưu ý:

- Luôn đồng bộ Service Control Policies để AI sử dụng các chính sách mới nhất.
- Thiết kế Prompt rõ ràng nhằm tăng chất lượng mã sinh ra.
- Kiểm tra và đánh giá mã IaC trước khi triển khai vào môi trường thực tế.
- Áp dụng nguyên tắc **Least Privilege** cho các IAM Role của AWS Lambda.
- Kích hoạt Amazon CloudWatch để theo dõi hoạt động và ghi log.
- Bảo vệ API bằng Amazon Cognito và AWS WAF nhằm hạn chế các cuộc tấn công từ bên ngoài.

---

# Kết luận

Việc kết hợp **Amazon Bedrock** với các dịch vụ serverless của AWS mang đến một giải pháp hiệu quả để tự động sinh mã **Infrastructure as Code** tuân thủ **Service Control Policies**.

Thông qua cơ chế đồng bộ chính sách bằng **AWS CloudTrail**, **Amazon EventBridge**, **AWS Lambda** và **Amazon S3**, hệ thống luôn sử dụng các quy định mới nhất của tổ chức khi sinh mã. Người dùng chỉ cần mô tả yêu cầu bằng ngôn ngữ tự nhiên, Amazon Bedrock sẽ phân tích yêu cầu, kết hợp với các chính sách hiện có và tạo ra đoạn mã IaC phù hợp.

Giải pháp không chỉ giúp tăng năng suất phát triển mà còn góp phần nâng cao khả năng quản trị hạ tầng, giảm thiểu rủi ro triển khai và tích hợp yếu tố bảo mật ngay từ giai đoạn thiết kế.

---

# Các dịch vụ AWS được sử dụng

| Dịch vụ AWS        | Vai trò                                               |
| ------------------ | ----------------------------------------------------- |
| Amazon Bedrock     | Sinh mã Infrastructure as Code bằng Foundation Models |
| AWS Lambda         | Xử lý cập nhật SCP và giao tiếp với Bedrock           |
| AWS CloudTrail     | Ghi nhận các thay đổi của Service Control Policies    |
| Amazon EventBridge | Phát hiện sự kiện cập nhật SCP                        |
| Amazon S3          | Lưu trữ Service Control Policies mới nhất             |
| Amazon API Gateway | Cung cấp API cho người dùng gửi yêu cầu               |
| Amazon Cognito     | Xác thực và phân quyền người dùng                     |
| AWS WAF            | Bảo vệ API khỏi các cuộc tấn công                     |
| Terraform          | Công cụ Infrastructure as Code được AI sinh ra        |

---

# Tài liệu tham khảo

- AWS Infrastructure & Automation Blog. _Using generative AI for proactive IaC code generation that's compliant with Service Control Policies using Amazon Bedrock._  
  https://aws.amazon.com/vi/blogs/infrastructure-and-automation/using-generative-ai-for-proactive-iac-code-generation-thats-compliant-with-service-control-policies-using-amazon-bedrock/
