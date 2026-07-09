---
title : "Kiểm thử & Đánh giá"
date : 2026-07-01
weight : 9
chapter : false
pre : " <b> 5.9. </b> "
---

#### Kiểm thử & Đánh giá hệ thống
Sau khi hoàn tất triển khai, chúng ta cần thực hiện các kịch bản kiểm thử (Test Cases) để đảm bảo luồng xử lý từ Frontend, qua API Gateway đến các dịch vụ AWS hoạt động trơn tru.

| Test Case | Mô tả | Kết quả mong đợi |
| :--- | :--- | :--- |
| **TC01** | Đăng nhập hệ thống | Chuyển hướng thành công tới Dashboard |
| **TC02** | Upload hóa đơn | File xuất hiện trong S3 & Lambda worker xử lý không lỗi |
| **TC03** | Lọc/Tìm kiếm | Danh sách hóa đơn cập nhật đúng theo từ khóa |
| **TC04** | Cảnh báo ngân sách | Hiển thị cảnh báo UI khi chi tiêu vượt ngưỡng |