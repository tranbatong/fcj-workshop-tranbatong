---
title : "Custom Domain with Route 53"
date : 2026-07-01
weight : 9
chapter : false
pre : " <b> 5.9. </b> "
---

#### Configuring Custom Domain with Amazon Route 53

To enable access to the system via a custom domain instead of the default URLs, we will configure DNS (Domain Name System) resolution using Amazon Route 53.

1. Access the **Amazon Route 53** service on the AWS Console, navigate to **Hosted zones** on the left menu.
2. Click the **Create hosted zone** button.
3. In the configuration section:
   * **Domain name:** Enter your registered domain (e.g., `cses2.id.vn`).
   * **Type:** Select **Public hosted zone**.
![Custom Domain](/images/5-Workshop/5.9-Route53-Domain/custom-r53-1.png)
4. Click the **Create hosted zone** button.
5. Upon successful creation, Route 53 will generate and provide 4 Name Server addresses (`NS` records).
![Custom Domain](/images/5-Workshop/5.9-Route53-Domain/custom-r53-2.png)
6. Log in to your domain registrar's management dashboard (e.g., Namecheap, GoDaddy, etc.).
7. Locate the **DNS Settings** (or Name Servers) section, remove the existing records, and update them with the 4 NS addresses provided by AWS to delegate domain management to Route 53.
![Custom Domain](/images/5-Workshop/5.9-Route53-Domain/custom-r53-3.png)

