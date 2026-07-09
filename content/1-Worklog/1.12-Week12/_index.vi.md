---
title: "Worklog Tuần 12"
date: 2026-07-06
weight: 12
chapter: false
pre: " <b> 1.12. </b> "
---

### Mục tiêu tuần 12:

- Hoàn thiện hệ thống bảo mật cho kiến trúc IDP bằng Amazon Cognito (Xác thực người dùng) và AWS WAF (Tường lửa ứng dụng web).
- Tích hợp toàn diện Frontend giao tiếp an toàn với API Gateway và S3.
- Hoàn thiện báo cáo Worklog, viết bài Blog chia sẻ quá trình làm dự án và chuẩn bị tài liệu Event/Workshop.
- Nộp bài tổng kết và xin nhận xét, đánh giá từ các anh chị Admin FCJ để rút kinh nghiệm.

### Các công việc cần triển khai trong tuần này:

| Thứ | Công việc                                                                                                                                                                                                                                                        | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu                            |
| --- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------ | --------------- | ----------------------------------------- |
| 2   | Thiết lập User Pool trên Amazon Cognito để quản lý xác thực người dùng. Cấu hình tích hợp JWT Token Validation giữa Cognito và Amazon API Gateway để bảo vệ các Dashboard APIs, đảm bảo chỉ người dùng đăng nhập hợp lệ mới được truy cập dữ liệu.               | 06/07/2026   | 06/07/2026      | Amazon Cognito Guide, API Gateway Auth    |
| 3   | Triển khai AWS WAF ở tầng Global để bảo vệ hệ thống khỏi các cuộc tấn công web phổ biến (như SQL Injection, XSS) và giới hạn tỷ lệ (Rate Limiting) cho các request gọi vào API. Hoàn thiện kết nối Frontend với S3 để upload file và API Gateway để lấy số liệu. | 07/07/2026   | 07/07/2026      | AWS WAF Documentation                     |
| 4   | Rà soát lại toàn bộ hệ thống từ đầu đến cuối (End-to-End) với các kịch bản thực tế. Dọn dẹp code, tối ưu cấu hình và chốt sơ đồ kiến trúc Serverless Intelligent Document Processing (IDP) phiên bản cuối cùng.                                                  | 08/07/2026   | 08/07/2026      | Sơ đồ kiến trúc tổng thể                  |
| 5   | Tổng hợp lại toàn bộ nội dung từ tuần 1 đến tuần 12 để hoàn thiện trang Worklog. Đảm bảo các thông tin cấu hình, hình ảnh minh chứng và kết quả đạt được qua mỗi tuần đều được ghi nhận đầy đủ, rõ ràng và logic.                                                | 09/07/2026   | 09/07/2026      | Nội dung các tuần Worklog                 |
| 6   | Viết bài Blog chia sẻ về hành trình xây dựng dự án IDP trên AWS, các khó khăn gặp phải và bài học rút ra. Thiết kế slide thuyết trình cho phần Event/Workshop để chia sẻ lại kiến thức cho cộng đồng.                                                            | 10/07/2026   | 10/07/2026      | Template Blog, Slide Workshop             |
| 7   | Đóng gói toàn bộ sản phẩm (Worklog, Blog, Slide Event) để nộp bài tổng kết khóa học. Gửi thông tin dự án vào nhóm cộng đồng để xin nhận xét, góp ý từ các anh chị Admin FCJ nhằm hoàn thiện kỹ năng và sửa đổi các điểm còn thiếu sót.                           | 11/07/2026   | 11/07/2026      | <https://cloudjourney.awsstudygroup.com/> |

### Kết quả đạt được tuần 12:

| Thứ | Công việc                                      | Kết quả đạt được                                                                                                                                                                                           |
| --- | ---------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 2   | Tích hợp Amazon Cognito và bảo vệ API          | Ứng dụng đã có màn hình đăng nhập an toàn. API Gateway tự động từ chối các request không có JWT Token hợp lệ, tăng cường bảo mật cho hệ thống dữ liệu.                                                     |
| 3   | Triển khai AWS WAF và hoàn thiện Frontend      | AWS WAF đã hoạt động để chặn các IP độc hại và chống spam request. Frontend hoàn thiện giao diện upload hóa đơn lên S3 và hiển thị biểu đồ, danh sách hóa đơn lấy từ API Gateway.                          |
| 4   | Kiểm thử tổng thể và tối ưu hệ thống           | Kiến trúc IDP hoạt động ổn định và trơn tru. Sơ đồ kiến trúc final đã được lưu lại để phục vụ cho báo cáo. Các lỗ hổng nhỏ trong cấu hình IAM đã được fix hoàn toàn.                                       |
| 5   | Hoàn thiện trang Worklog                       | Hệ thống Worklog Hugo hiển thị đẹp mắt, đầy đủ nội dung từ tuần 1 đến tuần 12. Hình ảnh minh chứng và các bước thực hành được trình bày chuyên nghiệp, sẵn sàng cho việc nộp bài.                          |
| 6   | Hoàn thiện tài liệu Blog và Event/Workshop     | Hoàn thành 1 bài Blog chất lượng tổng kết toàn bộ hành trình làm dự án AWS Serverless. File slide thuyết trình Workshop được thiết kế trực quan, dễ hiểu để trình bày trước hội đồng.                      |
| 7   | Nộp bài tổng kết và ghi nhận phản hồi từ Admin | Toàn bộ dự án đã được nộp đúng hạn. Đã nhận được những phản hồi rất giá trị từ các anh chị Admin FCJ, ghi chú lại các điểm cần cải thiện (như CI/CD, Monitoring nâng cao) để định hướng học tập tiếp theo. |
