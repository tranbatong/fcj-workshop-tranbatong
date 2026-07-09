---
title : "Cấu hình Cognito Authorizer"
date : 2026-07-01
weight : 2
chapter : false
pre : " <b> 5.7.2. </b> "
---

#### Bước 1: Khởi tạo bộ xác thực Authorizer
Để đảm bảo chỉ những người dùng đã đăng nhập hợp lệ mới có thể gọi API, chúng ta liên kết API Gateway với Cognito User Pool.

1. Truy cập dịch vụ **API Gateway** -> Chọn REST API `idp-rest-api`.
2. Ở menu cột bên trái, tìm và bấm vào mục **Authorizers**.
3. Bấm nút **Create authorizer** ở góc phải màn hình.
4. Thiết lập các thông số chi tiết như sau:
   * **Authorizer name**: Nhập `CognitoUserPoolAuthorizer`.
   * **Authorizer type**: Tích chọn mục **Cognito**.
   * **Cognito user pool**: Chọn vùng `us-east-1` và chọn đúng tên User Pool `idp-user-pool` bạn đã tạo ở phần trước.
   * **Token source**: Nhập cụm từ `Authorization` (Đây là header mà React Frontend sẽ dùng để đính kèm JWT Token khi gửi request).
   * **Token validation**: Để trống.
![Cognito API](/images/5-Workshop/5.7-API-Gateway-WAF/cognito-api-1.png)
5. Bấm nút **Create authorizer**.

#### Bước 2: Gắn bộ xác thực vào các phương thức GET
Chúng ta cần áp dụng bộ lọc bảo mật này lên các đường dẫn tài nguyên để bảo vệ dữ liệu.

1. Quay lại mục **Resources** ở menu bên trái.
2. Tìm đến nhánh **/get-upload-url** và bấm vào chữ **GET** nằm ngay phía dưới.
3. Chuyển sang tab **Method request**.
4. Tại mục *Method request settings*, bấm **Edit**.
5. Tại ô **Authorization** (mặc định đang hiển thị là *NONE*), bấm vào danh sách thả xuống và chọn đúng tên bộ xác thực **CognitoUserPoolAuthorizer** vừa tạo.
![Cognito API](/images/5-Workshop/5.7-API-Gateway-WAF/cognito-api-2.png)
6. Bấm **Save** để lưu lại cấu hình.

#### Bước 3: Áp dụng hàng loạt cho các tài nguyên còn lại
Thực hiện lặp lại chính xác các thao tác tại *Bước 2* để gắn `CognitoUserPoolAuthorizer` vào phương thức **GET** của các Resource còn lại bao gồm:
* Phương thức **GET** của `/invoices`
* Phương thức **GET** của `/stats`
* Phương thức **GET** của `/categories`
* Phương thức **GET** của `/payments`

*(Lưu ý: Giữ nguyên phương thức OPTIONS ở trạng thái Authorization là NONE để trình duyệt có thể kiểm tra CORS một cách tự do).*