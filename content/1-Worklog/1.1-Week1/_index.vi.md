---
title: "Worklog Tuần 1"
date: 2026-04-17
weight: 1
chapter: false
pre: " <b> 1.1. </b> "
---

### Mục tiêu tuần 1:

- Tham gia buổi Kickoff chương trình AWS First Cloud AI Journey: Tìm hiểu các quy định, văn hóa làm việc và kết nối, làm quen với các thành viên trong đội ngũ kỹ thuật của First Cloud Journey.
- Khởi tạo thành công tài khoản AWS cá nhân: Thiết lập phương thức thanh toán và cấu hình quản lý ngân sách (AWS Free Tier account) để phục vụ cho việc học tập, nghiên cứu, nắm vững cách sử dụng AWS Console & CLI.
- Hoàn thành các nhiệm vụ được giao trên AWS Console: Nhận tổng cộng 200 USD Credit, giúp tối ưu hóa chi phí khi thực hành các dịch vụ có tính phí.
- Chủ động tìm hiểu tổng quan về AWS: Nắm rõ danh mục dịch vụ (Compute, Storage, Networking, Database,...), kiến trúc hoạt động cùng mô hình tính phí của AWS để đảm bảo việc triển khai hệ thống sau này vừa hiệu quả vừa tiết kiệm.

### Các công việc cần triển khai trong tuần này:

| Thứ | Công việc                                                                                                                                                                                                                 | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu                            |
| --- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------ | --------------- | ----------------------------------------- |
| 2   | - Tham gia buổi Kickoff chương trình AWS First Cloud AI Journey <br> - Làm quen với các thành viên FCJ <br> - Đọc và lưu ý các nội quy, quy định, văn hóa làm việc tại đơn vị                                             | 17/04/2026   | 17/04/2026      |                                           |
| 3   | - Tìm hiểu tổng quan về AWS và mô hình tính phí <br> - Nghiên cứu sơ bộ các nhóm dịch vụ cốt lõi: <br>&emsp; + Compute, Storage, Networking, Database, ...                                                                | 18/04/2026   | 18/04/2026      | <https://cloudjourney.awsstudygroup.com/> |
| 4   | - Khởi tạo tài khoản AWS Free Tier cá nhân <br> - Thiết lập phương thức thanh toán và cấu hình quản lý ngân sách (Budget) chống phát sinh chi phí <br> - Thực hiện nhiệm vụ trên AWS Console để nhận 200 USD Credit       | 20/04/2026   | 20/04/2026      | <https://cloudjourney.awsstudygroup.com/> |
| 5   | - Tìm hiểu giao diện AWS Management Console <br> - Cài đặt và cấu hình AWS CLI trên máy tính cá nhân (Access Key, Secret Key, Default Region) <br> - Thực hành: Sử dụng các lệnh AWS CLI cơ bản                           | 21/04/2026   | 21/04/2026      | <https://cloudjourney.awsstudygroup.com/> |
| 6   | - Tìm hiểu dịch vụ Amazon EC2 cơ bản: <br>&emsp; + Instance types, AMI, EBS, Elastic IP <br> - Nghiên cứu các phương thức kết nối SSH từ máy trạm vào EC2                                                                 | 22/04/2026   | 22/04/2026      | <https://cloudjourney.awsstudygroup.com/> |
| 7   | - Thực hành triển khai hệ thống (Lab kỹ thuật): br>&emsp; + Khởi tạo EC2 instance hoàn chỉnh <br>&emsp; + Tạo và gắn thêm EBS volume <br>&emsp; + Thực hiện kết nối SSH và quản lý tài nguyên song song qua Console & CLI | 23/04/2026   | 23/04/2026      | <https://cloudjourney.awsstudygroup.com/> |

### Kết quả đạt được tuần 1:

| Thứ | Công việc                                 | Kết quả đạt được                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| --- | ----------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 2   | Tham gia Kickoff & hòa nhập môi trường    | Nắm rõ nội quy, quy chế thực tập và văn hóa làm việc tại dự án; kết nối thành công với các thành viên trong đội ngũ kỹ thuật.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| 3   | Nghiên cứu cốt lõi Cloud & hạ tầng AWS    | Học Module 1 (Phần 1: Các Khái Niệm Cốt Lõi & Hạ Tầng AWS): <br> - Điện toán đám mây: Thuê tài nguyên IT qua Internet với mô hình Pay-as-you-go thay vì mua phần cứng on-premises. Tối ưu chi phí đầu tư, tăng tốc độ phát triển và dễ mở rộng toàn cầu. <br> - Hạ tầng toàn cầu: <br>&emsp; + Data Center: Trung tâm dữ liệu vật lý tối ưu của AWS. <br>&emsp; + Availability Zone (AZ): Cụm trung tâm dữ liệu cách xa nhau để cô lập lỗi (luôn nên chạy ứng dụng trên tối thiểu 2 AZ). <br>&emsp; + Region: Khu vực địa lý lớn chứa tối thiểu 3 AZ. <br>&emsp; + Edge Location & Local Zone: Máy chủ biên đặt gần người dùng (đã có tại VN) làm bộ nhớ đệm giúp tải dữ liệu cực nhanh qua CloudFront. |
| 4   | Khởi tạo tài khoản & Cloud Explorer Tasks | Đăng ký thành công tài khoản AWS cá nhân; cấu hình AWS Budgets để kiểm soát chi phí. Hoàn thành chuỗi tác vụ AWS Cloud Explorer Tasks để làm quen với hạ tầng đám mây và nhận AWS Activate Credits thành công.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| 5   | Tìm hiểu cách tương tác & cấu hình CLI    | Học Module 1 (Phần 2: Cách Thức Tương Tác Với AWS): <br> Hiểu rõ 3 cách điều khiển dịch vụ của AWS: <br> - AWS Management Console: Giao diện Web. Phân biệt tài khoản Root User (bảo mật với MFA, không dùng hằng ngày) và IAM User (tài khoản phụ dùng hằng ngày với ID riêng - đã thực hành ở Task 1). <br> - AWS CLI: Giao diện dòng lệnh giúp thao tác nhanh. Đã cài đặt hoàn chỉnh trên máy, cấu hình Access Key và Secret Key an toàn (không push lên GitHub). <br> - AWS SDK: Bộ công cụ lập trình (Python, Java...) gọi API trực tiếp từ code.                                                                                                                                                  |
| 6   | Tìm hiểu kiến trúc máy chủ EC2            | Nắm vững lý thuyết về Instance types, các loại AMI, ổ lưu trữ EBS và các cơ chế định tuyến IP, bảo mật hệ thống thông qua SSH Key Pair.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| 7   | Thực hành Lab triển khai hệ thống         | Khởi tạo thành công máy chủ EC2, tạo và gắn thêm EBS volume, kết nối SSH từ máy cá nhân ổn định; kết hợp quản lý tài nguyên song song qua cả Console & CLI.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |

---

### Hình ảnh minh chứng thực tế:

**Thứ 2: Tham gia Kickoff & hòa nhập môi trường**

**Thứ 3: Nghiên cứu cốt lõi Cloud & hạ tầng AWS**

**Thứ 4: Khởi tạo tài khoản & Cloud Explorer Tasks**
![AWS Billing](image.png?width=400px)

**Thứ 5: Tìm hiểu cách tương tác & cấu hình CLI**

**Thứ 6: Tìm hiểu kiến trúc máy chủ EC2**

**Thứ 7: Thực hành Lab triển khai hệ thống**
