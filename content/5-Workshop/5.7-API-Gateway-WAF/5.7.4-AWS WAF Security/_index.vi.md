---
title : "Bảo mật với AWS WAF"
date : 2026-07-01
weight : 4
chapter : false
pre : " <b> 5.7.4. </b> "
---

#### Khởi tạo Web Application Firewall (WAF)
Để bảo vệ API Gateway khỏi các cuộc tấn công DDoS hoặc spam request, chúng ta sẽ thiết lập quy tắc giới hạn tần suất (Rate-based rule) trên AWS WAF.

1. Truy cập giao diện **AWS WAF**. Ở cuối dải thông báo (banner), hãy bấm vào đường link chữ nhỏ: **"Switch to the previous console"** (Chuyển về giao diện trước đó).
2. Bấm nút **Create web ACL**.
3. **Resource type**: Chọn **Regional resources**.
4. **Region**: Chọn `US East (N. Virginia) us-east-1`.
5. **Name**: Nhập `idp-api-waf-shield`.
![Create WAF](/images/5-Workshop/5.7-API-Gateway-WAF/waf-1.png)
6. **Associated AWS resources**: Bấm nút **Add AWS resources**.
   * Chọn loại tài nguyên là **Amazon API Gateway REST API**.
   * Tích chọn API Gateway `idp-rest-api` với stage `dev`. Bấm Add.

![Create WAF](/images/5-Workshop/5.7-API-Gateway-WAF/waf-2.png) 
7. Bấm **Next** để chuyển sang bước tạo quy tắc.

#### Cấu hình Quy tắc chống Spam (Rate-based rule)
Chúng ta sẽ tạo một quy tắc tự động chặn IP nếu nó gửi quá nhiều yêu cầu trong một khoảng thời gian ngắn.

1. Tại bước Add rules, bấm vào nút **Add rules** -> Chọn **Add my own rules and rule groups**.
2. **Rule type**: Chọn **Rate-based rule**.
3. **Name**: Nhập `BlockSpamIP`.
![Create WAF](/images/5-Workshop/5.7-API-Gateway-WAF/waf-3.png)
4. **Rate limit**: Nhập `100` (Hệ thống sẽ tự động chặn IP nếu phát hiện hơn 100 yêu cầu được gửi đến trong vòng 5 phút).
5. **Action**: Chọn **Block**.
![Create WAF](/images/5-Workshop/5.7-API-Gateway-WAF/waf-4.png)
![Create WAF](/images/5-Workshop/5.7-API-Gateway-WAF/waf-5.png)
6. Bấm **Add rule** để lưu quy tắc này.
7. Ở các bước tiếp theo (Bước 3: Set rule priority và Bước 4: Configure metrics), hãy giữ nguyên cấu hình mặc định và bấm **Next**.
8. Tại Bước 5 (Review and create web ACL), kiểm tra lại toàn bộ thông tin và bấm **Create web ACL** để kích hoạt tường lửa.