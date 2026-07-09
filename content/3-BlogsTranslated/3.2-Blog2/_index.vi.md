---
title: "Bài viết 2"
date: 2026-06-16
weight: 3
chapter: false
pre: " <b> 3.2. </b> "
---

# Tùy chỉnh luồng đăng nhập liên kết (Federated Sign-in) với Inbound Federation Lambda Trigger trong Amazon Cognito

Khi xây dựng hệ thống cho phép người dùng đăng nhập bằng các nhà cung cấp danh tính bên thứ ba (Identity Provider - IdP) như **Google**, **Facebook**, **OIDC** hoặc **SAML**, một trong những vấn đề thường gặp là dữ liệu người dùng từ các IdP không đồng nhất. Điều này dễ dẫn đến việc tạo ra nhiều tài khoản cho cùng một người dùng hoặc lưu trữ những thuộc tính không cần thiết.

Để giải quyết vấn đề này, AWS đã giới thiệu **Inbound Federation Lambda Trigger** cho Amazon Cognito. Trigger này cho phép lập trình viên can thiệp vào luồng xác thực ngay sau khi Cognito nhận được thông tin từ IdP nhưng trước khi hồ sơ người dùng được tạo hoặc cập nhật.

---

## Luồng hoạt động

![Sequence flow of a federated login configured with the inbound federation Lambda trigger](image.png)

**Hình 1. Luồng xác thực sử dụng Inbound Federation Lambda Trigger.**

Quy trình hoạt động gồm các bước sau:

1. Người dùng truy cập ứng dụng và lựa chọn đăng nhập bằng một nhà cung cấp danh tính (Google, Facebook, SAML, OIDC...).
2. Amazon Cognito chuyển hướng người dùng sang IdP để thực hiện xác thực.
3. Sau khi xác thực thành công, IdP trả về các thông tin định danh (claims/attributes) cho Cognito.
4. Trước khi Cognito tạo hoặc cập nhật tài khoản người dùng, **Inbound Federation Lambda Trigger** được kích hoạt.
5. Hàm Lambda có thể:
   - Thêm thuộc tính mới.
   - Chỉnh sửa giá trị thuộc tính.
   - Chuẩn hóa dữ liệu.
   - Loại bỏ những thuộc tính không cần thiết.
   - Liên kết danh tính với tài khoản đã tồn tại.
6. Cognito tiếp tục hoàn thành quá trình đăng nhập và trả về Authorization Code hoặc Access Token cho ứng dụng.

Nhờ vị trí thực thi này, lập trình viên có toàn quyền kiểm soát dữ liệu trước khi chúng được lưu trong User Pool.

---

## Vai trò của Inbound Federation Lambda Trigger

Khác với các Lambda Trigger truyền thống chỉ xử lý sau khi người dùng đã được tạo, Inbound Federation Lambda Trigger hoạt động ngay trong quá trình liên kết danh tính (Federation).

Điều này giúp giải quyết nhiều bài toán mà trước đây phải xử lý thủ công hoặc xây dựng thêm service trung gian.

Một số khả năng chính gồm:

- Chuẩn hóa dữ liệu từ nhiều IdP khác nhau.
- Thêm hoặc ghi đè thuộc tính người dùng.
- Loại bỏ các thuộc tính không cần thiết.
- Kiểm tra và liên kết tài khoản đã tồn tại.
- Giảm dữ liệu dư thừa trong Cognito User Pool.

---

# Ứng dụng trong hệ thống B2B

Đối với các doanh nghiệp sử dụng **SAML Identity Provider** như Microsoft Entra ID (Azure AD), Okta hoặc ADFS, người dùng thường được trả về rất nhiều thuộc tính và danh sách Group Membership.

Ví dụ:

- Department
- Organization
- Hundreds of Security Groups
- Cost Center
- Region
- Employee Type

Nếu toàn bộ dữ liệu này được lưu trực tiếp vào Cognito, tổng kích thước thuộc tính có thể vượt quá giới hạn **2048 ký tự**, khiến quá trình đăng nhập thất bại.

Inbound Federation Lambda Trigger cho phép:

- Lọc bỏ những nhóm không cần thiết.
- Chuẩn hóa tên Group.
- Chỉ giữ lại những quyền phục vụ phân quyền trong hệ thống.

Nhờ đó:

- Giảm dung lượng dữ liệu.
- Tránh lỗi đăng nhập.
- Đơn giản hóa việc quản lý quyền.

---

# Ứng dụng trong hệ thống B2C

Một tình huống phổ biến trong các hệ thống B2C là người dùng từng đăng ký bằng Email/Password nhưng sau đó lại đăng nhập bằng Google hoặc Facebook.

Ví dụ:

- Tài khoản A:
  - Email: example@gmail.com
  - Đăng ký bằng Email

Sau đó người dùng chọn:

- Sign in with Google

Nếu không xử lý, Cognito sẽ tạo thêm:

- Tài khoản B
  - Email: example@gmail.com
  - Provider: Google

Điều này dẫn đến:

- Hai tài khoản cho cùng một người dùng.
- Lịch sử giao dịch bị phân tán.
- Khó quản lý dữ liệu khách hàng.

Inbound Federation Lambda Trigger có thể:

- Kiểm tra email đã tồn tại hay chưa.
- Tìm User tương ứng trong User Pool.
- Thực hiện liên kết (Account Linking) giữa tài khoản hiện tại và danh tính mới.

Sau khi liên kết:

- Người dùng chỉ còn một tài khoản duy nhất.
- Có thể đăng nhập bằng nhiều phương thức khác nhau.
- Toàn bộ lịch sử giao dịch và thông tin cá nhân được quản lý tập trung.

---

# Các thao tác có thể thực hiện trong Lambda Trigger

Trong quá trình xử lý, Lambda có thể:

- Thêm thuộc tính mới.
- Ghi đè giá trị thuộc tính.
- Loại bỏ thuộc tính không cần thiết.
- Chuẩn hóa tên hiển thị.
- Chuẩn hóa Email.
- Chuyển đổi định dạng dữ liệu.
- Liên kết tài khoản với người dùng đã tồn tại.

Ví dụ:

| Thuộc tính từ IdP    | Sau khi xử lý      |
| -------------------- | ------------------ |
| John DOE             | John Doe           |
| SALES-HCM            | Sales              |
| employee@gmail.com   | employee@gmail.com |
| 350 Group Membership | 5 Group quan trọng |

---

# Lợi ích của Inbound Federation Lambda Trigger

Việc bổ sung Lambda Trigger mới mang lại nhiều lợi ích:

- Đồng bộ dữ liệu người dùng giữa nhiều Identity Provider.
- Giảm tình trạng tạo tài khoản trùng lặp.
- Kiểm soát hoàn toàn dữ liệu trước khi lưu vào Cognito.
- Hỗ trợ Account Linking một cách tự động.
- Chuẩn hóa dữ liệu phục vụ phân quyền và báo cáo.
- Nâng cao trải nghiệm đăng nhập của người dùng.

---

# Lưu ý khi triển khai

Khi triển khai thực tế cần lưu ý một số điểm sau:

- Hàm Lambda phải hoàn thành xử lý trong khoảng **5 giây** để tránh làm gián đoạn quá trình đăng nhập.
- Cần xây dựng cơ chế xử lý ngoại lệ (Error Handling) cẩn thận nhằm đảm bảo lỗi trong Lambda không vô tình chặn các yêu cầu đăng nhập hợp lệ.
- Chỉ nên chỉnh sửa các thuộc tính thực sự cần thiết để giảm thời gian xử lý.
- Nếu thực hiện Account Linking, cần kiểm tra chính xác danh tính người dùng nhằm tránh liên kết nhầm giữa các tài khoản.

---

# Kết luận

Inbound Federation Lambda Trigger là một cải tiến đáng chú ý của Amazon Cognito dành cho các hệ thống sử dụng Federated Identity. Tính năng này cho phép lập trình viên can thiệp trực tiếp vào dữ liệu người dùng trước khi Cognito tạo hoặc cập nhật tài khoản, từ đó giải quyết hiệu quả các vấn đề như dữ liệu không đồng nhất, tài khoản trùng lặp và lưu trữ các thuộc tính dư thừa.

Đối với các hệ thống B2B, Trigger giúp lọc và chuẩn hóa thông tin từ các nhà cung cấp SAML. Trong khi đó, với các hệ thống B2C, đây là giải pháp hữu ích để tự động liên kết nhiều phương thức đăng nhập vào cùng một tài khoản người dùng, đảm bảo dữ liệu được quản lý tập trung và nhất quán.

---

## Tài liệu tham khảo

- AWS Security Blog. _Customize federated sign-in with the new Amazon Cognito Inbound Federation Lambda Trigger._ https://aws.amazon.com/vi/blogs/security/customize-federated-sign-in-with-new-amazon-cognito-lambda-trigger/
