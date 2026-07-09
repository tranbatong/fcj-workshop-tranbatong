---
title : "Tạo IAM Role"
date : 2026-07-01 
weight : 2 
chapter : false
pre : " <b> 5.4.2. </b> "
---

Các hàm AWS Lambda yêu cầu một vai trò thực thi (execution role) để có thể tương tác với các dịch vụ AWS khác. Chúng ta sẽ tạo một role cung cấp các quyền thiết yếu.

#### Hướng dẫn từng bước:
1. Truy cập vào giao diện **IAM** (Identity and Access Management) và bấm **Create role**.
2. **Trusted entity type**: Chọn **AWS service**.
3. **Use case**: Chọn **Lambda**, sau đó bấm **Next**.

![IAM Trust Entity](/images/5-Workshop/5.4-Messaging-IAM/iam-trust-1.png)

4. Tại trang **Add permissions**, tìm kiếm và tích chọn 5 quyền (policies) sau đây:
   * `AWSLambdaSQSQueueExecutionRole`
   * `AmazonS3ReadOnlyAccess`
   * `AmazonDynamoDBFullAccess`
   * `AmazonTextractFullAccess`
   * `AmazonBedrockFullAccess`

![IAM Permissions](/images/5-Workshop/5.4-Messaging-IAM/iam-permissions-2.png)

5. Bấm **Next**.
6. **Role name**: Nhập `idp-lambda-ai-role`.
![IAM Permissions](/images/5-Workshop/5.4-Messaging-IAM/idp-lambda-ai-role.png)
7. Cuộn xuống cuối trang và bấm **Create role** để hoàn tất.