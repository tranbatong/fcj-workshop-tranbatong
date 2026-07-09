---
title: "Worklog Tuần 6"
date: 2026-05-25
weight: 6
chapter: false
pre: " <b> 1.6. </b> "
---

### Mục tiêu tuần 6:

- Nghiên cứu đi sâu vào các công nghệ quản lý tầng dữ liệu và các phương thức tăng tốc truyền tải nội dung toàn cầu.
- Thiết lập kiến trúc dự phòng thảm họa (Disaster Recovery) dựa trên các mô hình cam kết dịch vụ (SLA) và hai chỉ số kỹ thuật RTO, RPO.
- Thực hành cấu hình Amazon S3 Advanced Features, tích hợp mạng phân phối nội dung CDN (Amazon CloudFront) và tính năng Versioning chống ransomware.

### Các công việc cần triển khai trong tuần này:

| Thứ | Công việc                                                                                                                                                                                                               | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu                                  |
| --- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------ | --------------- | ----------------------------------------------- |
| 2   | Nghiên cứu lý thuyết Module 04 về bản chất Object Storage và tự động chuyển đổi lớp lưu trữ với S3 Lifecycle Management. Tìm hiểu giải pháp Hybrid qua AWS Storage Gateway và vận chuyển dữ liệu bằng AWS Snow Family.  | 25/05/2026   | 25/05/2026      | Khóa học AWS First Cloud AI Journey (FCAJ) 2026 |
| 3   | Thực hành Lab 57 cấu hình Static Website Hosting trên S3 Bucket và tải lên source code cho ứng dụng đơn trang (SPA). Thiết lập Bucket Policy sử dụng JSON để cấp quyền đọc công khai.                                   | 26/05/2026   | 26/05/2026      | Khóa học AWS First Cloud AI Journey (FCAJ) 2026 |
| 4   | Tích hợp Amazon CloudFront (CDN) để tăng tốc độ tải trang. Cấu hình che giấu S3 Bucket gốc và chặn toàn bộ public access trực tiếp tại Bucket nhằm tối ưu bảo mật.                                                      | 27/05/2026   | 27/05/2026      | Khóa học AWS First Cloud AI Journey (FCAJ) 2026 |
| 5   | Kích hoạt Bucket Versioning lưu trữ nhiều phiên bản để bảo vệ dữ liệu khỏi ransomware, chống ghi đè hoặc vô tình xóa. Cấu hình Cross-Region Replication (CRR) để sao chép bất đồng bộ sang Region khác dự phòng địa lý. | 28/05/2026   | 28/05/2026      | Khóa học AWS First Cloud AI Journey (FCAJ) 2026 |
| 6   | Nghiên cứu 4 chiến lược Disaster Recovery trên AWS. Phân tích chi tiết các mô hình: Backup & Restore, Pilot Light, Warm Standby và Multi-Site.                                                                          | 29/05/2026   | 29/05/2026      | Khóa học AWS First Cloud AI Journey (FCAJ) 2026 |
| 7   | Thực hiện quy trình dọn dẹp tài nguyên (Cost Optimization) trên Amazon CloudFront bằng cách Disable và Delete các Distribution. Thực hiện lệnh Empty và Delete để xóa hoàn toàn các S3 Buckets.                         | 30/05/2026   | 30/05/2026      | Khóa học AWS First Cloud AI Journey (FCAJ) 2026 |

### Kết quả đạt được tuần 6:

| Thứ | Công việc                                 | Kết quả đạt được                                                                                                                                    |
| --- | ----------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------- |
| 2   | Nghiên cứu công nghệ lưu trữ dữ liệu      | Hiểu rõ S3 lưu trữ dạng đối tượng ngang hàng không phân cấp thư mục và các loại Storage Gateway (File, Volume, Tape) kết nối On-Premises lên Cloud. |
| 3   | Triển khai Static Website                 | Khởi tạo thành công S3 Bucket và kích hoạt tính năng host ứng dụng đơn trang (SPA) với quyền đọc công khai.                                         |
| 4   | Tích hợp mạng CDN CloudFront              | Làm chủ quy trình xây dựng website tĩnh hiệu năng cao, kết hợp bảo mật hạ tầng CDN CloudFront bảo vệ máy chủ gốc S3.                                |
| 5   | Triển khai các tính năng lưu trữ nâng cao | Thiết lập thành công lưu trữ nhiều phiên bản đối tượng và tự động sao chép dự phòng địa lý sang một AWS Region khác.                                |
| 6   | Thiết lập chính sách Khắc phục sự cố      | Nắm vững kỹ năng thiết kế và phân bổ giải pháp phục hồi dữ liệu đám mây toàn diện theo tiêu chuẩn an ninh mạng.                                     |
| 7   | Tối ưu hóa chi phí và dọn dẹp tài nguyên  | Xóa sạch hoàn toàn các đối tượng, phiên bản bên trong Bucket và các Distribution đã tạo khỏi hệ thống AWS.                                          |

---

### Làm các bài lab

#### Lab13

![alt text](image.png)
![alt text](image-1.png)
![alt text](image-2.png)
![alt text](image-3.png)
![alt text](image-4.png)
![alt text](image-5.png)
