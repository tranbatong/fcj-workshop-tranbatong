---
title: "Worklog Tuần 7"
date: 2026-06-01
weight: 7
chapter: false
pre: " <b> 1.7. </b> "
---

### Mục tiêu tuần 7:

- Thực hành chuyên sâu các tính năng lưu trữ doanh nghiệp của Windows trên Cloud thông qua Amazon FSx.
- Nghiên cứu nền tảng bảo mật theo triết lý "Security is Job Zero" của AWS.
- Nắm vững mô hình chia sẻ trách nhiệm, quản trị định danh nâng cao, quản lý tổ chức và mã hóa dữ liệu trung tâm.

### Các công việc cần triển khai trong tuần này:

| Thứ | Công việc                                                                                                                                                                                                                                                                                                        | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu         |
| --- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------ | --------------- | ---------------------- |
| 2   | Khởi tạo hệ thống tệp Multi-AZ chuẩn NTFS với cấu hình SSD và HDD trên Amazon FSx để đảm bảo dự phòng thảm họa. Cấu hình folder chia sẻ chuẩn SMB kết nối trực tiếp với Microsoft Active Directory nhằm quản lý user tập trung.                                                                                  | 01/06/2026   | 01/06/2026      | Khóa học AWS FCAJ 2026 |
| 3   | Thiết lập hạn ngạch lưu trữ cho người dùng (Storage Quotas) và quản lý tập trung các phiên kết nối cùng file đang mở. Thực hành mở rộng linh hoạt dung lượng lưu trữ và băng thông xử lý khi tải tăng cao mà không làm gián đoạn dịch vụ.                                                                        | 02/06/2026   | 02/06/2026      | Khóa học AWS FCAJ 2026 |
| 4   | Nghiên cứu Mô hình chia sẻ trách nhiệm (Shared Responsibility Model), nơi AWS đảm bảo an toàn phần cứng, hạ tầng toàn cầu vật lý và các lớp phần mềm cơ bản.                                                                                                                                                     | 03/06/2026   | 03/06/2026      | Khóa học AWS FCAJ 2026 |
| 5   | Tìm hiểu Root Account Best Practices như khóa tài khoản root và chia đôi thông tin mật khẩu/MFA phần cứng. Cấu hình IAM Policy bằng mã JSON, ưu tiên lệnh cấm tường minh (Deny) và sử dụng IAM Role (AssumeRole) để cấp quyền tạm thời. Tránh nhúng trực tiếp access key cố định vào mã nguồn ứng dụng trên EC2. | 04/06/2026   | 04/06/2026      | Khóa học AWS FCAJ 2026 |
| 6   | Quản lý tập trung tài khoản qua AWS Organizations với hóa đơn gộp và Service Control Policies (SCP). Thiết lập cơ chế Đăng nhập một lần (SSO) qua AWS Identity Center. Nghiên cứu giải pháp xác thực Amazon Cognito và dịch vụ quản lý khóa trung tâm AWS KMS.                                                   | 05/06/2026   | 05/06/2026      | Khóa học AWS FCAJ 2026 |
| 7   | Thực hiện quy trình dọn dẹp tài nguyên (Cost Optimization) bằng lệnh Delete file system trên FSx mà không lưu bản sao lưu cuối cùng. Xóa các điểm phục hồi trong AWS Backup và xóa Stack Lab 25 trên CloudFormation để thu hồi máy chủ EC2 kiểm thử.                                                             | 06/06/2026   | 06/06/2026      | Khóa học AWS FCAJ 2026 |

### Kết quả đạt được tuần 7:

| Thứ | Công việc                         | Kết quả đạt được                                                                                                                                                                     |
| --- | --------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| 2   | Khởi tạo hệ thống lưu trữ Windows | Triển khai đồng thời hệ thống tệp Amazon FSx trên nhiều vùng sẵn sàng (Multi-AZ) và thiết lập thành công các folder chia sẻ chuẩn SMB kết nối với Active Directory.                  |
| 3   | Tối ưu hóa hệ thống FSx           | Làm chủ kỹ năng quản trị, giám sát hiệu năng và tối ưu dung lượng của hệ thống lưu trữ Windows doanh nghiệp quy mô lớn trên Amazon FSx.                                              |
| 4   | Nghiên cứu kiến trúc bảo mật      | Hiểu rõ phạm vi chịu trách nhiệm (Security of the Cloud) của AWS đối với an toàn phần cứng và hạ tầng toàn cầu.                                                                      |
| 5   | Quản trị quyền truy cập (IAM)     | Hiểu sâu sắc và rèn luyện tư duy thiết kế hệ thống "Zero Trust", kiểm soát quyền truy cập nhiều lớp. Nắm vững cách không sử dụng access key trực tiếp và cấp quyền tạm thời qua STS. |
| 6   | Quản lý phân cấp và mã hóa        | Hiểu cách áp dụng Service Control Policies (SCP) để thiết lập giới hạn quyền tối đa trong Organizations và áp dụng cơ chế mã hóa KMS bảo vệ dữ liệu ở trạng thái nghỉ.               |
| 7   | Tối ưu hóa chi phí                | Dọn dẹp thành công các hệ thống tệp FSx, điểm phục hồi AWS Backup và ngăn xếp CloudFormation, tự động thu hồi toàn bộ các tài nguyên phụ thuộc để tiết kiệm chi phí.                 |

---

### Kế hoạch tuần tiếp theo:

- Tiếp tục thực hiện các bài lab của Module.
