---
title : "Tạo các bảng DynamoDB"
date : 2026-07-01 
weight : 3 
chapter : false
pre : " <b> 5.3.3. </b> "
---

Chúng ta sẽ tạo 4 bảng sử dụng chế độ On-Demand (trả tiền theo dùng thực tế) để tối ưu hóa chi phí.

Truy cập giao diện **Amazon DynamoDB** và chọn **Tables** ở thanh menu bên trái.

#### Bảng 1: InvoicesData
Bảng này lưu trữ dữ liệu cuối cùng sau khi được AI bóc tách.
1. Bấm nút **Create table**.
2. **Table name**: Nhập **InvoicesData**.
3. **Partition key**: Nhập **documentId** (Kiểu dữ liệu: **String**).
4. **Table settings**: Chọn **Customize settings**.
5. **Read/write capacity settings**: Chọn **On-demand** (Quan trọng để tối ưu chi phí).

![InvoicesData](/images/5-Workshop/5.3-Storage-Database/dynamo-invoicesdata-1.png)
![InvoicesData](/images/5-Workshop/5.3-Storage-Database/dynamo-invoicesdata-2.png)
6. Bấm **Create table**.

#### Bảng 2: InvoicePayments
Bảng này theo dõi trạng thái thanh toán của từng hóa đơn.
1. Bấm **Create table** lần nữa.
2. **Table name**: Nhập **InvoicePayments**.
3. **Partition key**: Nhập **invoiceId** (Kiểu dữ liệu: **String**).
4. **Table settings**: Chọn **Customize settings** -> **On-demand**.

![InvoicePayments](/images/5-Workshop/5.3-Storage-Database/dynamo-invoicespayments-1.png)
![InvoicePayments](/images/5-Workshop/5.3-Storage-Database/dynamo-invoicespayments-2.png)
5. Bấm **Create table**.

#### Bảng 3: UserBudgets
Bảng này lưu trữ cấu hình hạn mức chi tiêu (ngân sách) do người dùng tự thiết lập.
1. Bấm **Create table** lần nữa.
2. **Table name**: Nhập **UserBudgets**.
3. **Partition key**: Nhập **userEmail** (Kiểu dữ liệu: **String**).
4. **Table settings**: Chọn **Customize settings** -> **On-demand**.
5. Bấm **Create table**.

#### Bảng 4: UserCategories
Bảng này lưu các quy tắc danh mục chi tiêu tự định nghĩa của người dùng.
1. Bấm **Create table** lần nữa.
2. **Table name**: Nhập **UserCategories**.
3. **Partition key**: Nhập **userEmail** (Kiểu dữ liệu: **String**).
4. **Table settings**: Chọn **Customize settings** -> **On-demand**.

![UserCategories](/images/5-Workshop/5.3-Storage-Database/dynamo-usercategories-1.png)
![UserCategories](/images/5-Workshop/5.3-Storage-Database/dynamo-usercategories-2.png)
5. Bấm **Create table**.

---

#### Xác nhận kết quả
Hãy đợi một lúc cho đến khi trạng thái (Status) của cả 4 bảng đều chuyển thành **Active** trước khi sang phần tiếp theo. Danh sách bảng DynamoDB của bạn sẽ hiển thị đầy đủ như hình dưới đây:

![All Tables Active](/images/5-Workshop/5.3-Storage-Database/dynamo-all-table.png)