---
title: "Worklog Tuần 8"
date: 2026-06-08
weight: 8
chapter: false
pre: " <b> 1.8. </b> "
---

### Mục tiêu tuần 8:

- Hoàn thiện các giải pháp an ninh và tối ưu hóa quản lý tài nguyên thuộc Module 05.
- Nghiên cứu chuyên sâu tầng kiến trúc dữ liệu đám mây thuộc Module 06.
- Thực hành triển khai AWS Security Hub, bảo mật cho AWS Lambda và quản trị tài nguyên theo thẻ (Tagging).

### Các công việc cần triển khai trong tuần này:

| Thứ | Công việc                                                                                                                                                                                                                                                                                                                | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu         |
| --- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------ | --------------- | ---------------------- |
| 2   | Kích hoạt dịch vụ AWS Security Hub để liên tục thu thập dữ liệu và quét cấu hình an ninh tự động trên tài khoản (Lab 18). Chấm điểm hạ tầng dựa trên các tiêu chuẩn bảo mật thực hành tốt nhất và các bộ tiêu chuẩn ngành nhằm phát hiện sớm các lỗ hổng.                                                                | 08/06/2026   | 08/06/2026      | Khóa học AWS FCAJ 2026 |
| 3   | Khởi tạo Security Group với các quy tắc Inbound/Outbound nghiêm ngặt để kiểm soát luồng traffic mạng nội bộ VPC cho AWS Lambda (Lab 22). Tạo IAM Execution Role cấp riêng cho AWS Lambda thay thế việc nhúng Access Key cố định. Tích hợp điều kiện ràng buộc vào policy như khung giờ quy định hoặc IP công ty cố định. | 09/06/2026   | 09/06/2026      | Khóa học AWS FCAJ 2026 |
| 4   | Khởi tạo máy chủ EC2 kiểm thử và áp dụng kỹ thuật gán các thẻ định danh (Tags) thông qua cặp Key-Value (Lab 27). Sử dụng AWS CLI và Managing Tags để kiểm soát, tương tác và phân loại nhóm tài nguyên. Thiết lập hệ thống Resource Group dựa trên Tag để nhóm tự động tài nguyên liên quan.                             | 10/06/2026   | 10/06/2026      | Khóa học AWS FCAJ 2026 |
| 5   | Nghiên cứu Khái niệm cơ sở dữ liệu lõi bao gồm cấu trúc Khóa chính, Khóa ngoại để chuẩn hóa dữ liệu. Ứng dụng Index để tăng tốc độ đọc dữ liệu. Tìm hiểu cơ chế ghi log giao dịch phục vụ khôi phục và phân biệt rõ kiến trúc xử lý giao dịch (OLTP) và phân tích dữ liệu (OLAP).                                        | 11/06/2026   | 11/06/2026      | Khóa học AWS FCAJ 2026 |
| 6   | Tìm hiểu Amazon RDS hỗ trợ cấu hình Multi-AZ đồng bộ dữ liệu tức thời và bản sao chỉ đọc. Nghiên cứu Amazon Aurora với hiệu năng đọc/ghi song song cao gấp 3-5 lần DB truyền thống. Tìm hiểu Amazon Redshift (kho dữ liệu cấu trúc cột) và Amazon ElastiCache (dịch vụ bộ nhớ đệm In-memory).                            | 12/06/2026   | 12/06/2026      | Khóa học AWS FCAJ 2026 |
| 7   | Truy cập AWS Security Hub, tiến hành Disable các bộ tiêu chuẩn đánh giá và vô hiệu hóa dịch vụ (Lab 18). Xóa IAM Role đã cấp cho Lambda, xóa hàm Lambda tương ứng và gỡ bỏ Security Group (Lab 22). Xóa bỏ cấu hình Resource Group và Terminate toàn bộ các máy chủ EC2 kiểm thử (Lab 27).                               | 13/06/2026   | 13/06/2026      | Khóa học AWS FCAJ 2026 |

### Kết quả đạt được tuần 8:

| Thứ  | Công việc                        | Kết quả đạt được                                                                                                                                                                                 |
| ---- | -------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| 2    | Đánh giá cấu hình an toàn        | Vận hành thành công công cụ kiểm tra an ninh tự động Security Hub.                                                                                                                               |
| 3    | Bảo mật Điện toán Phi máy chủ    | Thiết lập thành công phân quyền an toàn mạng cho AWS Lambda bằng Security Group và IAM Role.                                                                                                     |
| 4    | Quản trị Tài nguyên theo thẻ     | Tối ưu hóa việc quản lý hạ tầng quy mô lớn thông qua Resource Groups.                                                                                                                            |
| 5, 6 | Nghiên cứu Cơ sở dữ liệu đám mây | Nắm vững tư duy phân bổ kiến trúc dữ liệu: Sử dụng SQL (RDS/Aurora) cho các tác vụ giao dịch hàng ngày (OLTP), Redshift cho kho dữ liệu phân tích (OLAP) và ElastiCache để tăng tốc độ phản hồi. |
| 7    | Tối ưu hóa chi phí và dọn dẹp    | Hoàn tất dừng tiến trình quét của Security Hub, gỡ bỏ thành công IAM Role/Lambda, xóa cấu hình Resource Group và giải phóng dung lượng bộ nhớ lưu trữ EBS.                                       |

---

### Làm các bài lab:

- Tiếp tục thực hiện các bài lab của Module.

#### Lab18

![alt text](image.png)
![alt text](image-1.png)

#### Lab22

![alt text](image-2.png)
![alt text](image-3.png)
![alt text](image-4.png)
![alt text](image-5.png)
![alt text](image-6.png)
![alt text](image-7.png)
![alt text](image-8.png)
![alt text](image-9.png)
![alt text](image-10.png)
![alt text](image-11.png)
![alt text](image-12.png)
![alt text](image-13.png)
![alt text](image-14.png)

#### Lab27

![alt text](image-15.png)
![alt text](image-16.png)
![alt text](image-17.png)
![alt text](image-18.png)
![alt text](image-19.png)
![alt text](image-20.png)
![alt text](image-21.png)
![alt text](image-22.png)
![alt text](image-23.png)
![alt text](image-24.png)
![alt text](image-25.png)
![alt text](image-26.png)

#### Lab28

![alt text](image-27.png)
![alt text](image-28.png)
![alt text](image-29.png)
![alt text](image-30.png)
![alt text](image-31.png)
![alt text](image-32.png)
![alt text](image-33.png)
![alt text](image-34.png)
![alt text](image-35.png)
![alt text](image-36.png)
![alt text](image-37.png)

#### Lab30

![alt text](image-38.png)
![alt text](image-39.png)
![alt text](image-40.png)
![alt text](image-41.png)
