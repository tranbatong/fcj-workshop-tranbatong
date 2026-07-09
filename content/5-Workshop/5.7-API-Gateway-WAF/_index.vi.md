---
title : "API Gateway & WAF Security"
date : 2026-07-01
weight : 7
chapter : false
pre : " <b> 5.7. </b> "
---

#### Cấu hình API Gateway & Bảo mật WAF

Các hàm AWS Lambda mặc định là riêng tư. Để Frontend có thể tương tác được, chúng ta cần tạo một REST API công khai. **Amazon API Gateway** sẽ đóng vai trò làm "cánh cửa" định tuyến HTTP. Đồng thời, chúng ta sẽ cấu hình kiểm tra quyền truy cập bằng **Cognito Authorizer** và thiết lập **AWS WAF** để bảo vệ hệ thống.

#### Nội dung
- [Tạo REST API & Resources](1-create-api/)
- [Cấu hình Cognito Authorizer](2-cognito-authorizer/)
- [Cấu hình CORS & Deploy](3-deploy-api/)
- [Bảo mật với AWS WAF](4-waf-security/)