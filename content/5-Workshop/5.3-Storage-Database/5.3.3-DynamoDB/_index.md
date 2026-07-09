---
title : "Create DynamoDB Tables"
date : 2026-07-01 
weight : 3 
chapter : false
pre : " <b> 5.3.3. </b> "
---

We will create four tables using On-Demand capacity to ensure you only pay for the exact reads and writes your application performs.

Navigate to the **Amazon DynamoDB** console and select **Tables** from the left menu.

#### Table 1: InvoicesData
This table stores the final data extracted by the AI.
1. Click **Create table**.
2. **Table name**: **InvoicesData**.
3. **Partition key**: **documentId** (Type: **String**).
4. **Table settings**: Select **Customize settings**.
5. **Read/write capacity settings**: Select **On-demand** (Important for cost savings).

![InvoicesData](/images/5-Workshop/5.3-Storage-Database/dynamo-invoicesdata-1.png)
![InvoicesData](/images/5-Workshop/5.3-Storage-Database/dynamo-invoicesdata-2.png)
6. Click **Create table**.

#### Table 2: InvoicePayments
This table tracks the payment status of each invoice.
1. Click **Create table** again.
2. **Table name**: **InvoicePayments**.
3. **Partition key**: **invoiceId** (Type: **String**).
4. **Table settings**: Select **Customize settings** -> **On-demand**.

![InvoicePayments](/images/5-Workshop/5.3-Storage-Database/dynamo-invoicespayments-1.png)
![InvoicePayments](/images/5-Workshop/5.3-Storage-Database/dynamo-invoicespayments-2.png)
5. Click **Create table**.

#### Table 3: UserBudgets
This table stores the budget configurations set by users based on their email.
1. Click **Create table** again.
2. **Table name**: **UserBudgets**
3. **Partition key**: **userEmail** (Type: **String**)
4. **Table settings**: Select **Customize settings** -> **On-demand**.
5. Click **Create table**.

#### Table 4: UserCategories
This table stores custom categorization rules for users.
1. Click **Create table** again.
2. **Table name**: **UserCategories**.
3. **Partition key**: **userEmail** (Type: **String**).
4. **Table settings**: Select **Customize settings** -> **On-demand**.

![UserCategories](/images/5-Workshop/5.3-Storage-Database/dynamo-usercategories-1.png)
![UserCategories](/images/5-Workshop/5.3-Storage-Database/dynamo-usercategories-2.png)
5. Click **Create table**.

---

#### Verification
Wait a few moments until the status of all four tables becomes **Active** before moving to the next section. Your DynamoDB tables list should look exactly like this:

![All Tables Active](/images/5-Workshop/5.3-Storage-Database/dynamo-all-table.png)