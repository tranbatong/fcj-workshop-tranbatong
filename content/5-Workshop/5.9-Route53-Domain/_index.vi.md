---
title : "Tên miền với Route 53"
date : 2026-07-01
weight : 9
chapter : false
pre : " <b> 5.9. </b> "
---

#### Cấu hình tên miền tùy chỉnh với Amazon Route 53

Để hệ thống có thể truy cập thông qua tên miền tùy chỉnh thay vì các đường link mặc định, chúng ta sẽ thực hiện cấu hình phân giải DNS (Domain Name System) trên dịch vụ Amazon Route 53.

1. Truy cập dịch vụ **Amazon Route 53** trên AWS Console, điều hướng đến mục **Hosted zones** ở menu bên trái.
2. Nhấn nút **Create hosted zone**.
3. Tại phần cấu hình:
   * **Domain name:** Nhập tên miền bạn đã đăng ký (Ví dụ: `cses2.id.vn`).
   * **Type:** Chọn **Public hosted zone** (vùng lưu trữ công khai trên Internet).
![Custom Domain](/images/5-Workshop/5.9-Route53-Domain/custom-r53-1.png)
4. Nhấn nút **Create hosted zone**.
5. Sau khi tạo thành công, Route 53 sẽ cấp phát cho bạn 4 địa chỉ máy chủ phân giải tên miền (Name Servers - bản ghi loại `NS`).
![Custom Domain](/images/5-Workshop/5.9-Route53-Domain/custom-r53-2.png)
6. Đăng nhập vào trang quản trị của nhà cung cấp tên miền của bạn (ví dụ: P.A Việt Nam, MatBao, v.v.).
7. Tìm đến phần **Thay đổi DNS** (hoặc Name Servers), xóa các bản ghi cũ và cập nhật 4 địa chỉ NS này vào để ủy quyền quản lý tên miền cho AWS.
![Custom Domain](/images/5-Workshop/5.9-Route53-Domain/custom-r53-3.png)