---
title : "Prepare the environment"
date : 2026-07-01
weight : 1
chapter : false
pre : " <b> 5.4.1 </b> "
---

We will create a Standard SQS Queue to decouple the document upload process from the AI extraction process.

#### Step 1: Create the SQS Queue
1. Navigate to the **Amazon SQS** console and click **Create queue**.
2. **Type**: Select **Standard**.
3. **Name**: Enter `idp-document-queue`.
4. Under **Configuration**, change the **Visibility timeout** to **2 Minutes**. Keep other configurations as default.

![SQS Configuration](/images/5-Workshop/5.4-Messaging-IAM/sqs-config-1.png)

5. Scroll down to the **Access policy** section and choose **Advanced**.
6. Replace the existing JSON with the following policy to allow your S3 bucket to send messages to this queue:

![SQS Configuration](/images/5-Workshop/5.4-Messaging-IAM/sqs-config-2.png)

#### Step 2: Configure S3 Event Notifications
Now, we must tell our Ingestion Bucket to send a message to the newly created SQS queue whenever a new document is uploaded.

1. Navigate to the **Amazon S3** console and click on **idp-ingest-bucket-1**.
2. Go to the **Properties** tab.
3. Scroll down to Event notifications and click **Create event notification**.
4. **Event name**: Enter **SendToSQS**.
5. **Event types**: Check the box for **All object create events**.

![SQS SendToSQS](/images/5-Workshop/5.4-Messaging-IAM/send-to-sqs-1.png)

1. Scroll down to the **Destination** section.
2. **Destination**: Select **SQS queue**.
3. **Specify SQS queue**: Choose **Choose from your SQS queues** and select **idp-document-queue** from the dropdown.

![SQS Destination](/images/5-Workshop/5.4-Messaging-IAM/send-to-sqs-2.png)
4. Click **Save changes**.