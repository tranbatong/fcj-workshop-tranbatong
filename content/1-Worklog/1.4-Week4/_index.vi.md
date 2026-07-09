---
title: "Worklog Tuần 4"
date: 2026-05-11
weight: 4
chapter: false
pre: " <b> 1.4. </b> "
---

### Mục tiêu tuần 4:

- Tối ưu hóa khả năng kết nối và phân giải tên miền trong các mô hình hạ tầng mạng phức tạp.
- Thiết lập giải pháp Hybrid DNS bằng Route 53 Resolver để đồng bộ môi trường AWS và On-Premises.
- Khởi tạo kết nối ngang hàng VPC Peering để các mạng ảo giao tiếp nội bộ an toàn mà không cần đi qua internet.
- Áp dụng các nguyên tắc bảo mật Zero Trust và quản trị tài nguyên chặt chẽ để tối ưu ngân sách.

### Các công việc cần triển khai trong tuần này:

| Thứ | Công việc                                                                                                                                                                                 | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu                            |
| --- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------ | --------------- | ----------------------------------------- |
| 2   | - Nghiên cứu cơ chế phân giải tên miền lai Hybrid DNS giữa môi trường đám mây và truyền thống <br> - Tìm hiểu dịch vụ Route 53 Resolver và cách tạo các điểm cuối Inbound/Outbound        | 11/05/2026   | 11/05/2026      | Khóa học First Cloud AI Journey           |
| 3   | - Thực hành Lab 10: Sử dụng CloudFormation tạo hạ tầng và triển khai AWS Managed Microsoft AD giả lập DNS On-Premises <br> - Cấu hình Resolver Rules và kiểm tra phân giải bằng nslookup  | 12/05/2026   | 12/05/2026      | Khóa học First Cloud AI Journey           |
| 4   | - Học lý thuyết Lab 19 về kết nối ngang hàng VPC Peering <br> - Lên phương án quy hoạch hai dải IP không trùng lặp cho My VPC và HG VPC để chuẩn bị kết nối                               | 13/05/2026   | 13/05/2026      | Khóa học First Cloud AI Journey           |
| 5   | - Cập nhật Network ACL để giới hạn truy cập ở tầng subnet <br> - Thực hành gửi yêu cầu Peering Connection và chấp nhận kết nối giữa hai VPC                                               | 14/05/2026   | 14/05/2026      | Khóa học First Cloud AI Journey           |
| 6   | - Cấu hình bảng định tuyến Route Tables trỏ lưu lượng qua Peering Connection <br> - Kích hoạt tính năng Cross-Peer DNS để phân giải ra địa chỉ Private IP giữa các máy chủ                | 15/05/2026   | 15/05/2026      | Khóa học First Cloud AI Journey           |
| 7   | - Thiết lập luật Inbound cho Security Group và áp dụng IAM Policies giới hạn vùng thực hành theo mô hình Zero Trust <br> - Dọn dẹp toàn bộ tài nguyên để tránh phí phát sinh ngoài ý muốn | 16/05/2026   | 16/05/2026      | <https://cloudjourney.awsstudygroup.com/> |

### Kết quả đạt được tuần 4:

| Thứ | Công việc                                | Kết quả đạt được                                                                                                                                                                          |
| --- | ---------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 2   | Nghiên cứu lý thuyết Hybrid DNS          | Hiểu rõ nguyên lý hoạt động của Route 53 Resolver, cách thức chuyển tiếp truy vấn DNS hai chiều giữa hạ tầng AWS và hệ thống mạng máy chủ nội bộ On-Premises.                             |
| 3   | Triển khai Lab 10 và kiểm tra hệ thống   | Cấu hình thành công điểm cuối Inbound/Outbound và quy tắc chuyển tiếp cho tên miền on-prem.example.com; xác nhận phân giải mượt mà qua IP nội bộ bằng lệnh nslookup trên máy chủ Windows. |
| 4   | Quy hoạch hạ tầng VPC Peering            | Chuẩn bị thành công hai môi trường mạng My VPC (172.31.0.0/16) và HG VPC (10.10.0.0/16) đảm bảo không xung đột địa chỉ IP khi thiết lập đường truyền riêng.                               |
| 5   | Thiết lập luồng kết nối ngang hàng       | Gửi yêu cầu và kích hoạt thành công trạng thái Active cho Peering Connection. Đồng thời thắt chặt bảo mật qua việc tinh chỉnh Network ACLs chỉ cho phép dải IP chỉ định.                  |
| 6   | Định tuyến liên mạng và Cross-Peer DNS   | Hoàn tất khai báo bảng định tuyến hai chiều để các máy chủ EC2 giao tiếp được với nhau. Kích hoạt thành công Cross-Peer DNS để tối ưu tốc độ phân giải nội bộ.                            |
| 7   | Quản trị bảo mật và tối ưu hóa ngân sách | Nắm vững kỹ năng sửa lỗi mạng. Hoàn thành dọn dẹp sạch sẽ tài nguyên bằng cách hủy máy chủ EC2, xóa Peering Connection, Route 53 Endpoints và thu hồi CloudFormation Stacks.              |

---

### Hình ảnh minh chứng thực tế bài thực hành:

#### 1. Khởi tạo máy chủ Windows Server (RDGW-Server)

Giao diện quản lý EC2 ghi nhận máy chủ RDGW-Server chạy nền tảng Windows đã được khởi tạo thành công và đang ở trạng thái Running, sẵn sàng làm môi trường kiểm tra định tuyến.
![alt text](image.png)

#### 2. Cấu hình bảo mật mạng (Security Groups)

Thiết lập và chỉnh sửa thành công các luật truy cập đầu vào (Inbound Rules) cho nhóm bảo mật RDGW-SG, cho phép các luồng dữ liệu cần thiết phục vụ cho việc kiểm tra DNS và điều khiển máy chủ.
![alt text](image-1.png)

#### 3. Tạo điểm cuối Inbound (Route 53 Resolver Inbound Endpoint)

Hệ thống báo cáo cấu hình thành công điểm cuối Inbound (R53-InboundEndpoint) trên Route 53, cho phép môi trường On-Premises có thể truy vấn ngược lại các tên miền được lưu trữ trên hạ tầng AWS.
![alt text](image-2.png)

#### 4. Tạo điểm cuối Outbound (Route 53 Resolver Outbound Endpoint)

Khởi tạo trạng thái Operational cho điểm cuối Outbound (R53-OutboundEndpoint), đóng vai trò cầu nối chuyển tiếp các gói tin truy vấn DNS từ AWS sang mạng nội bộ.
![alt text](image-3.png)

#### 5. Thiết lập quy tắc chuyển tiếp (Resolver Rules)

Bảng quy tắc điều hướng DNS ghi nhận luật ForwardToOnPremAD đã được tạo hoàn chỉnh. Luật này chịu trách nhiệm bắt các truy vấn tới tên miền corp.internal và đẩy qua Outbound endpoint.
![alt text](image-4.png)

#### 6. Kiểm tra phân giải tên miền Hybrid DNS bằng nslookup

Truy cập vào máy chủ Windows (RDGW-Server) và chạy lệnh nslookup. Kết quả cho thấy hệ thống đã phân giải thành công tên miền nội bộ corp.internal ra địa chỉ IP 10.0.4.201 thông qua máy chủ DNS trung gian 10.0.0.2.
![alt text](image-5.png)
