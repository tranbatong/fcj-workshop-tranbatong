---
title : "Chuẩn bị tài nguyên"
date : 2026-07-01
weight : 1
chapter : false
pre : " <b> 5.4.1 </b> "
---

Chúng ta sẽ tạo một Hàng đợi SQS Tiêu chuẩn (Standard) để tách biệt quá trình tải tài liệu lên khỏi quá trình bóc tách bằng AI.

#### Bước 1: Khởi tạo Hàng đợi SQS
1. Truy cập vào giao diện **Amazon SQS** và bấm **Create queue**.
2. **Type**: Chọn **Standard**.
3. **Name**: Nhập `idp-document-queue`.
4. Tại mục **Configuration**, sửa giá trị **Visibility timeout** thành **2 Minutes**. Các tuỳ chọn còn lại giữ nguyên không thay đổi.

![SQS Configuration](/images/5-Workshop/5.4-Messaging-IAM/sqs-config-1.png)

5. Cuộn xuống phần **Access policy** và chọn **Advanced**.
6. Thay thế đoạn mã JSON hiện tại bằng chính sách (policy) dưới đây để cho phép bucket S3 của bạn gửi tin nhắn vào hàng đợi này:

![SQS Configuration](/images/5-Workshop/5.4-Messaging-IAM/sqs-config-2.png)

#### Bước 2: Cấu hình S3 Event Notifications
Bây giờ, chúng ta cần thiết lập để Bucket tiếp nhận dữ liệu tự động gửi thông báo sang hàng đợi SQS vừa tạo mỗi khi có tài liệu mới được tải lên.

1. Quay lại dịch vụ **Amazon S3** và bấm vào bucket **idp-ingest-bucket-1**.
2. Chuyển sang tab **Properties**.
3. Cuộn xuống mục **Event notifications** và bấm nút **Create event notification**.
4. **Event name**: Nhập **SendToSQS**.
5. **Event types**: Tích chọn ô **All object create events**.

![SQS SendToSQS](/images/5-Workshop/5.4-Messaging-IAM/send-to-sqs-1.png)

1. Cuộn xuống phần **Destination** ở cuối trang.
2. **Destination**: Chọn **SQS queue**.
3. **Specify SQS queue**: Chọn **Choose from your SQS queues** và chọn **idp-document-queue** từ danh sách thả xuống.

![SQS Destination](/images/5-Workshop/5.4-Messaging-IAM/send-to-sqs-2.png)

4. Bấm nút **Save changes** để lưu lại.



