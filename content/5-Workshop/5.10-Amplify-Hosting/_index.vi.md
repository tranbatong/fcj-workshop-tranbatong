---
title : "CI/CD với AWS Amplify"
date : 2026-07-01
weight : 10
chapter : false
pre : " <b> 5.10. </b> "
---

#### Tích hợp CI/CD và Triển khai Giao diện với AWS Amplify

Chúng ta sử dụng AWS Amplify để tự động hóa quy trình triển khai (CI/CD) cho giao diện Web tĩnh React SPA, đồng thời tự động cấp phát chứng chỉ bảo mật SSL (HTTPS).

**Tích hợp Mã nguồn & Khởi tạo Build**
1. Truy cập dịch vụ **AWS Amplify**, cuộn xuống mục "Start building with Amplify" và nhấn nút **Create new app**.
2. Chọn nguồn lưu trữ mã nguồn là **GitHub** và nhấn **Next** (Thực hiện ủy quyền xác thực tài khoản GitHub nếu hệ thống yêu cầu).
3. Chọn Repository chứa mã nguồn dự án của bạn (`serverless-idp-project`) và chỉ định nhánh cần triển khai (ví dụ: nhánh `main`). 
4. Tích chọn mục **My app is a monorepo** và nhập đường dẫn thư mục gốc chứa Frontend (ví dụ: `idp-frontend`). Nhấn **Next**.
![Amplify](/images/5-Workshop/5.10-Amplify-Hosting/amplify-1.png)
5. Tại bước **App settings**, hệ thống sẽ tự nhận diện framework. Hãy đảm bảo cấu hình khớp với dự án React:
   * **Frontend build command:** `npm run build`
   * **Build output directory:** `dist`
![Amplify](/images/5-Workshop/5.10-Amplify-Hosting/amplify-2.png)
6. Nhấn **Next** và 
![Amplify](/images/5-Workshop/5.10-Amplify-Hosting/amplify-3.png)
7. Chọn **Save and deploy**. Amplify sẽ tự động kéo mã nguồn, chạy lệnh build và xuất bản giao diện Web.

**Cấu hình Tên miền Tùy chỉnh (Custom Domain)**
1. Sau khi Deploy thành công, chuyển sang mục **Hosting** ở menu bên trái, chọn **Custom domains**.
![Amplify](/images/5-Workshop/5.10-Amplify-Hosting/amplify-4.png)
2. Nhấn nút **Add domain** ở góc phải phía trên.
![Amplify](/images/5-Workshop/5.10-Amplify-Hosting/amplify-5.png)
3. Chọn tên miền đã thiết lập ở Route 53 (ví dụ: `cses2.id.vn`) từ danh sách thả xuống.
4. Cấu hình Subdomains để định tuyến nhánh `main` và thiết lập Redirect từ `www` về tên miền gốc.
5. Nhấn **Configure domain** và lưu lại. Amplify sẽ tự động xác thực DNS với Route 53 và cấp chứng chỉ SSL. Hệ thống IDP của bạn giờ đây đã sẵn sàng hoạt động an toàn qua HTTPS!