---
title : "Enable CORS & Deploy"
date : 2026-07-01
weight : 3
chapter : false
pre : " <b> 5.7.3. </b> "
---

#### Step 1: Enable CORS
Since our React frontend and API Gateway will be hosted on different domains, we must enable Cross-Origin Resource Sharing (CORS).

1. Select the root resource **/get-upload-url** in your API list.
2. Click the **Enable CORS** button.
3. Under **Gateway responses**, check **Default 4XX** and **Default 5XX**.
4. Under **Access-Control-Allow-Methods**, make sure **GET** and **OPTIONS** are checked.
![Enable CORS](/images/5-Workshop/5.7-API-Gateway-WAF/api-cors.png)
5. Click **Save**.
6. **Repeat steps 1-5 for ALL other resources** (**/categories**, **/invoices**, **/payments**, **/stats**).


#### Step 2: Deploy the API
Your API is not accessible until you deploy it to a stage.

1. Click the **Deploy API** button at the top right.
2. **Stage**: Select **\*New stage\***.
3. **Stage name**: Enter `dev`.
![Deploy API](/images/5-Workshop/5.7-API-Gateway-WAF/deploy-api.png)
4. Click **Deploy**.

#### Step 3: Save the Invoke URL
After deployment, you will be redirected to the Stage details page. 
* Locate the **Invoke URL** (e.g., `https://xb9xtht5w1.execute-api.us-east-1.amazonaws.com/dev`).

![Invoke URL](/images/5-Workshop/5.7-API-Gateway-WAF/api-invoke-url.png)

* **Copy and save this URL!** You will need to paste this URL into your React frontend configuration file in the next chapter.