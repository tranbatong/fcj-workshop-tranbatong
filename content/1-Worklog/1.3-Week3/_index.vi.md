---
title: "Worklog Tuần 3"
date: 2026-05-01
weight: 3
chapter: false
pre: " <b> 1.3. </b> "
---

### Mục tiêu tuần 3:

- Thiết lập kết nối internet cho các máy chủ nằm trong phân nhánh mạng riêng tư (private subnet) và triển khai các phương thức kết nối bảo mật nâng cao.
- Học cách quản trị hạ tầng mạng lõi trên hệ thống mà không cần tiếp xúc hay mở luồng với internet công cộng.
- Rèn luyện tư duy bài bản về tối ưu hóa chi phí và quy trình dọn dẹp tài nguyên sạch sẽ trên nền tảng AWS.

### Các công việc cần triển khai trong tuần này:

| Thứ | Công việc                                                                                                                                                                                                                                        | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu                            |
| --- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------ | --------------- | ----------------------------------------- |
| 2   | - Nghiên cứu cơ chế triển khai và cấp phát kết nối internet hướng ra ngoài cho vùng mạng private thông qua cổng NAT (NAT Gateway) <br> - Tìm hiểu cách cấp phát địa chỉ IP tĩnh Elastic IP cho các cổng kết nối mạng                             | 01/05/2026   | 01/05/2026      | Khóa học First Cloud AI Journey           |
| 3   | - Học lý thuyết nâng cao về phương thức kết nối bảo mật bằng công cụ EC2 Instance Connect Endpoint (EICE) <br> - Nghiên cứu cách thức truy cập SSH trực tiếp vào máy private mà không cần dùng máy nhảy Bastion Host hay IP Public               | 02/05/2026   | 02/05/2026      | Khóa học First Cloud AI Journey           |
| 4   | - Phân tích cấu hình các nhóm bảo mật (Security Group) phục vụ cho việc cô lập mạng <br> - Nghiên cứu cơ chế lồng nhóm bảo mật và cách xử lý các lỗi mất kết nối thông qua việc cấu hình luật Outbound Rules                                     | 04/05/2026   | 04/05/2026      | Khóa học First Cloud AI Journey           |
| 5   | - Đọc các tài liệu hướng dẫn về tối ưu hóa chi phí và quản lý ngân sách hiệu quả trên AWS <br> - Khảo sát bảng giá tính phí theo giờ của các tài nguyên chạy ngầm như NAT Gateway hay Elastic IP khi không sử dụng                               | 05/05/2026   | 05/05/2026      | <https://cloudjourney.awsstudygroup.com/> |
| 6   | - Lên kế hoạch chi tiết các bước triển khai sơ đồ bài Lab bao gồm dựng NAT Gateway, tạo EICE và chuẩn bị các câu lệnh kiểm tra <br> - Thiết lập sẵn danh sách các tài nguyên cần xóa sau khi thực hành xong để tránh phát sinh chi phí phạt      | 06/05/2026   | 06/05/2026      | Khóa học First Cloud AI Journey           |
| 7   | - Tiến hành thực hành trực tiếp các bước cấu hình hệ thống trên giao diện AWS Console <br> - Cấu hình bảng định tuyến, thực hiện lệnh ping/curl từ máy private để kiểm tra mạng, xử lý các lỗi phát sinh và thực hiện dọn dẹp toàn bộ tài nguyên | 07/05/2026   | 07/05/2026      | <https://cloudjourney.awsstudygroup.com/> |

### Kết quả đạt được tuần 3:

| Thứ | Công việc                              | Kết quả đạt được                                                                                                                                                                                                                             |
| --- | -------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 2   | Quy hoạch kết nối cổng internet NAT    | Nắm vững lý thuyết tạo cổng NAT Gateway tại phân nhánh public subnet, cấp phát thành công Elastic IP tĩnh và trỏ luồng định tuyến cho vùng private ra internet an toàn.                                                                      |
| 3   | Nghiên cứu phương thức kết nối bảo mật | Làm chủ kiến trúc thiết lập dịch vụ EC2 Instance Connect Endpoint trong mạng VPC giúp quản trị trực tiếp terminal của máy chủ private ngay trên giao diện web console.                                                                       |
| 4   | Phân tích quy tắc tường lửa và sửa lỗi | Hiểu sâu cách thiết lập nhóm bảo mật lồng nhau (Nested Security Group), biết cách sửa lỗi mất kết nối SSH bằng việc cấu hình chính xác các luồng ra Inbound/Outbound Rules.                                                                  |
| 5   | Nghiên cứu tư duy tối ưu chi phí cloud | Ý thức rõ trách nhiệm quản lý tài nguyên trên môi trường đám mây thông qua việc phân tích biểu phí cụ thể, ví dụ như mức phí chạy ngầm của NAT Gateway là $0.045 một giờ.                                                                    |
| 6   | Chuẩn bị kịch bản thực hành và dọn dẹp | Hoàn thiện tài liệu các bước cấu hình, chuẩn bị sẵn các câu lệnh kiểm tra kết nối hệ thống (ping, curl) cũng như các bước giải phóng hạ tầng bài bản.                                                                                        |
| 7   | Thực hành Lab và giải phóng tài nguyên | Xác nhận kết nối internet thành công từ máy chủ private qua cổng NAT. Truy cập trực tiếp terminal của EC2-Private và thực hiện tối ưu chi phí bằng cách xóa sạch NAT Gateway, giải phóng Elastic IP, hủy máy chủ ảo và xóa truc-vpc an toàn. |

---

### Hình ảnh minh chứng thực tế bài thực hành:

#### 1. Kết nối SSH vào máy chủ công cộng (EC2-Public) qua MobaXterm

Sử dụng client MobaXterm kết nối thành công qua SSH Session tới máy chủ có IP Public 34.239.227.34 trên nền tảng Amazon Linux 2023.
![Kết nối SSH vào EC2 Public qua MobaXterm](image-1.png)

#### 2. Kiểm tra kết nối Internet và gọi thử dịch vụ trên máy chủ Public

Thực hiện thành công lệnh ping kiểm tra kết nối mạng diện rộng tới Google và sử dụng lệnh curl -I để kiểm tra phản hồi HTTP từ hệ thống Amazon.
![Kiểm tra kết nối mạng từ máy Public](image-2.png)

#### 3. Phân quyền cặp khóa và thực hiện SSH nhảy cấp từ máy Public sang máy Private

Cấu hình phân quyền an toàn cho file key pair (chmod 400) và thực hiện SSH bảo mật từ dải IP của máy Public sang máy Private (10.0.2.157) thành công.
![SSH từ máy Public sang máy Private](image-3.png)

#### 4. Cấp phát địa chỉ IP tĩnh (Elastic IP) cho hệ thống NAT Gateway

Giao diện quản lý VPC cho thấy đã allocate thành công một địa chỉ Elastic IP cố định 32.194.27.77 đặt tên là EIP-NAT-AZ1a phục vụ hạ tầng mạng.
![Cấp phát Elastic IP](image-4.png)

#### 5. Khởi tạo thành công NAT Gateway trên giao diện điều khiển AWS Console

Hệ thống mạng ghi nhận cổng dịch vụ NAT-Gateway-AZ1a đã được liên kết với dải IP tĩnh vừa tạo và chuyển sang trạng thái sẵn sàng hoạt động (Available).
![Khởi tạo NAT Gateway](image-5.png)

#### 6. Thử nghiệm kết nối mạng một chiều thành công từ bên trong vùng kín (Private)

Máy chủ kín EC2-Private sau khi được định tuyến qua NAT Gateway đã có thể thực hiện lệnh ping 8.8.8.8 và nhận đầy đủ dữ liệu phản hồi từ Internet.
![Kiểm tra mạng từ máy Private qua NAT Gateway](image-6.png)

#### 7. Quản trị trực tiếp Terminal thông qua dịch vụ EC2 Instance Connect Endpoint (EICE)

Truy cập bảo mật thành công vào thẳng giao diện dòng lệnh của máy chủ Private trực tiếp từ trình duyệt Web thông qua cổng Endpoint được cấu hình sẵn.
![Truy cập qua EC2 Instance Connect Endpoint](image-7.png)
