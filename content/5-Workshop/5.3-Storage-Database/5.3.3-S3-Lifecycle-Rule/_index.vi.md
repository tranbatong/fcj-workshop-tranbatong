---
title : "Cấu hình S3 Lifecycle Rule"
date : 2026-07-01
weight : 3
chapter : false
pre : " <b> 5.3.3. </b> "
---

#### Tự động xóa tài liệu thô (Cost & Security Optimization)
Sau khi tài liệu được bóc tách bởi Textract AI và dữ liệu được lưu vào DynamoDB, việc giữ lại file ảnh/PDF gốc trên S3 là không cần thiết và gây tốn kém chi phí lưu trữ. Chúng ta sẽ thiết lập **S3 Lifecycle Rule** để tự động dọn dẹp các tệp tin này sau 1 ngày.

1. Truy cập dịch vụ **Amazon S3**, bấm vào bucket tiếp nhận dữ liệu của bạn: `idp-ingest-bucket-1` (hoặc `idp-ingest-bucket-01`).
2. Chuyển sang tab **Management** và bấm nút **Create lifecycle rule**.
3. **Lifecycle rule name**: Nhập `Auto-Delete-Raw-Invoices`.
4. **Choose a rule scope**: Chọn **Limit the scope of this rule using one or more filters**.
5. **Prefix**: Nhập `uploads/` (Đây là thư mục do Frontend tạo ra khi đẩy file lên).

![Lifecycle Rule](/images/5-Workshop/5.3-Storage-Database/lifecycle-rule-1.png)

6. Cuộn xuống phần **Lifecycle rule actions**, tích chọn mục **Expire current versions of objects**.
7. Tại mục **Expire current versions of objects** vừa hiện ra bên dưới, phần **Days after object creation**: Nhập `1` (Xóa sau 1 ngày).

![Lifecycle Rule](/images/5-Workshop/5.3-Storage-Database/lifecycle-rule-2.png)

8. Bấm nút **Create rule** để hoàn tất.