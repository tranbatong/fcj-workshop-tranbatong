---
title : "API Gateway & WAF Security"
date : 2026-07-01
weight : 7
chapter : false
pre : " <b> 5.7. </b> "
---

#### API Gateway Configuration & WAF Security

AWS Lambda functions are private by default. To allow our frontend application to interact with them, we need to create a public REST API. **Amazon API Gateway** will act as the "front door" routing HTTP requests. Additionally, we will secure our endpoints using a **Cognito Authorizer** and deploy **AWS WAF** to block malicious traffic.

#### Content
- [Create REST API & Resources](1-create-api/)
- [Configure Cognito Authorizer](2-cognito-authorizer/)
- [Enable CORS & Deploy](3-deploy-api/)
- [AWS WAF Security](4-waf-security/)