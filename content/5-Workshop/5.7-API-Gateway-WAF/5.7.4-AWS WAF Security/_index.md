---
title : "AWS WAF Security"
date : 2026-07-01
weight : 4
chapter : false
pre : " <b> 5.7.4. </b> "
---

#### Initialize Web Application Firewall (WAF)
To protect the API Gateway from DDoS attacks or spam requests, we will configure a Rate-based rule using AWS WAF.

1. Navigate to the **AWS WAF** console. At the bottom of the notification banner, click the small text link: **"Switch to the previous console"**.
2. Click **Create web ACL**.
3. **Resource type**: Select **Regional resources**.
4. **Region**: Select `US East (N. Virginia) us-east-1`.
5. **Name**: Enter `idp-api-waf-shield`.
![Create WAF](/images/5-Workshop/5.7-API-Gateway-WAF/waf-1.png)
6. **Associated AWS resources**: Click the **Add AWS resources** button.
   * Select **Amazon API Gateway REST API**.
   * Check your API Gateway `idp-rest-api` (stage `dev`) and add it.

![Create WAF](/images/5-Workshop/5.7-API-Gateway-WAF/waf-2.png)   
7. Click **Next** to proceed to the rule creation step.

#### Configure Anti-Spam Rule (Rate-based rule)
We will create a rule to automatically block any IP address that sends too many requests in a short period.

1. In the Add rules step, click **Add rules** -> Select **Add my own rules and rule groups**.
2. **Rule type**: Select **Rate-based rule**.
3. **Name**: Enter `BlockSpamIP`.
![Create WAF](/images/5-Workshop/5.7-API-Gateway-WAF/waf-3.png)
4. **Rate limit**: Enter `100` (The system will block the IP if it detects more than 100 requests within a 5-minute window).
5. **Action**: Select **Block**.
![Create WAF](/images/5-Workshop/5.7-API-Gateway-WAF/waf-4.png) 
![Create WAF](/images/5-Workshop/5.7-API-Gateway-WAF/waf-5.png) 
6. Click **Add rule** to save this configuration.
7. For the subsequent steps (Step 3: Set rule priority, and Step 4: Configure metrics), leave the default settings and click **Next**.
8. In Step 5 (Review and create web ACL), verify your information and click **Create web ACL** to activate the firewall.