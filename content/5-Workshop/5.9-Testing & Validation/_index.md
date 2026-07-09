---
title : "Testing & Validation"
date : 2026-07-01
weight : 9
chapter : false
pre : " <b> 5.9. </b> "
---

#### System Testing & Validation
After completing the deployment, we must perform test cases to ensure the end-to-end data processing flow—from the Frontend, through the API Gateway, to the underlying AWS services—is functioning correctly.

| Test Case | Description | Expected Result |
| :--- | :--- | :--- |
| **TC01** | System Login | Successfully redirected to Dashboard |
| **TC02** | Invoice Upload | File appears in S3 & Lambda worker processes without errors |
| **TC03** | Search/Filtering | Invoice list updates correctly based on keywords |
| **TC04** | Budget Alerts | UI displays warnings when spending exceeds limits |