---
title : "Tạo User Pool & App Client"
date : 2026-07-01
weight : 1
chapter : false
pre : " <b> 5.6.1. </b> "
---

#### Khởi tạo User Pool
1. Truy cập dịch vụ **Amazon Cognito** trên AWS Console và chọn **Create user pool**.
2. **Options for sign-in identifiers**: Tích chọn **Email**.
3. Tại bước cấu hình đăng ký, cuộn đến phần **Self-registration** và **Bỏ tích** mục *Enable self-registration* (Việc này giúp bảo mật hệ thống, ngăn chặn người lạ tự do đăng ký tài khoản).
4. **Required attributes for sign-up**: Mở danh sách thả xuống và chọn **email** cùng với **name**.

#### Khởi tạo App Client
1. Di chuyển đến bước Integrate your app (Tích hợp ứng dụng).
2. **Application type**: Chọn **Single-page application (SPA)** (Vì chúng ta đang sử dụng ReactJS).
3. **Name your application**: Điền `idp-react-app`.
4. Cuộn xuống cuối trang và bấm **Create user pool**.

![Create UserPool](/images/5-Workshop/5.6-identity-Cognito/user-pool.png)

Sau khi tạo xong, hãy copy `User pool ID` và `Client ID` để dán vào file cấu hình `cognitoConfig.js` trên mã nguồn React.

#### Tạo tài khoản người dùng thử nghiệm
Vì hệ thống không cho phép tự do đăng ký, bạn cần cấp phát tài khoản thủ công cho nhân viên:
1. Truy cập vào User Pool vừa tạo, chuyển sang tab **Users** (trong mục User management) và bấm **Create user**.
2. Điền tên tài khoản, địa chỉ email của người dùng.
3. Nhập một mật khẩu tạm thời (Temporary password).
4. Tích chọn ô **Mark email as verified** để xác nhận email hợp lệ.

![Create User](/images/5-Workshop/5.6-identity-Cognito/create-user.png)

5. Bấm **Create user**. (Khi đăng nhập lần đầu vào Frontend, người dùng sẽ được yêu cầu đổi mật khẩu tạm thời này thành mật khẩu mới và bổ sung thông tin Họ tên).