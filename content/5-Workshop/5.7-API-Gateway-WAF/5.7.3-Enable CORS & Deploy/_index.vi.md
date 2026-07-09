---
title : "Cấu hình CORS & Deploy"
date : 2026-07-01
weight : 3
chapter : false
pre : " <b> 5.7.3. </b> "
---

#### Bước 1: Kích hoạt CORS
Vì giao diện React và API Gateway chạy trên 2 tên miền (domain) khác nhau, trình duyệt sẽ chặn các kết nối. Chúng ta phải bật CORS (Cross-Origin Resource Sharing) để cho phép giao tiếp.

1. Bấm chọn resource gốc **get-upload-url** trong danh sách API.
2. Bấm nút **Enable CORS**.
3. Tại mục **Gateway responses**, tích chọn **Default 4XX** và **Default 5XX**.
4. Tại mục **Access-Control-Allow-Methods**, đảm bảo **GET** và **OPTIONS** đã được chọn.
![Enable CORS](/images/5-Workshop/5.6-API-Gateway/api-cors.png)
5. Bấm **Save**.
6. **Lặp lại các bước từ 1-5 cho TẤT CẢ các resource còn lại** (**/categories**, **/invoices**, **/payments**, **/stats**).
#### Bước 2: Triển khai (Deploy) API
API của bạn sẽ chưa thể hoạt động nếu chưa được triển khai (Deploy) vào một môi trường (Stage) cụ thể.

1. Bấm nút **Deploy API** ở góc trên bên phải.
2. **Stage**: Chọn **\*New stage\***.
3. **Stage name**: Nhập `dev`.
![Deploy API](/images/5-Workshop/5.6-API-Gateway/deploy-api.png)
4. Bấm **Deploy**.

#### Bước 3: Lưu lại Invoke URL
Sau khi Deploy thành công, bạn sẽ được chuyển đến trang chi tiết của Stage.
* Tìm đến dòng **Invoke URL** (có dạng `https://xb9xtht5w1.execute-api.us-east-1.amazonaws.com/dev`).

![Invoke URL](/images/5-Workshop/5.6-API-Gateway/api-invoke-url.png)

* **Hãy copy và lưu lại đường link này!** Ở chương tiếp theo, bạn sẽ cần dán link này vào tệp cấu hình của React Frontend để hệ thống hoạt động.
