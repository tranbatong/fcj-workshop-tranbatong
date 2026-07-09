---
title : "Configure Cognito Authorizer"
date : 2026-07-01
weight : 2
chapter : false
pre : " <b> 5.7.2. </b> "
---

#### Step 1: Create the Cognito Authorizer
To ensure that only authenticated users can invoke our API endpoints, we will integrate API Gateway with our Cognito User Pool.

1. Navigate to the **API Gateway** console and select your REST API: `idp-rest-api`.
2. In the left-hand navigation menu, click on **Authorizers**.
3. Click the **Create authorizer** button on the top right.
4. Configure the following parameters:
   * **Authorizer name**: Enter `CognitoUserPoolAuthorizer`.
   * **Authorizer type**: Select **Cognito**.
   * **Cognito user pool**: Ensure the region is `us-east-1` and select your User Pool (`idp-user-pool`).
   * **Token source**: Type `Authorization` (This specifies the header that the React Frontend will use to transmit the JWT Token).
   * **Token validation**: Leave this field blank.
![Cognito API](/images/5-Workshop/5.7-API-Gateway-WAF/cognito-api-1.png)
5. Click **Create authorizer**.

#### Step 2: Attach the Authorizer to the GET Method
We must explicitly apply this security mechanism to our resource endpoints to restrict public access.

1. Return to the **Resources** section via the left menu.
2. Expand the **/get-upload-url** path and click on the **GET** method underneath it.
3. Switch over to the **Method request** tab.
4. Under the *Method request settings* section, click **Edit**.
5. In the **Authorization** dropdown field (which defaults to *NONE*), select your newly created **CognitoUserPoolAuthorizer**.
![Cognito API](/images/5-Workshop/5.7-API-Gateway-WAF/cognito-api-2.png)
6. Click **Save** to apply the configuration.

#### Step 3: Repeat for the Remaining Resources
Repeat the exact process described in *Step 2* to map the `CognitoUserPoolAuthorizer` to the **GET** methods of the remaining endpoints:
* **GET** method for `/invoices`
* **GET** method for `/stats`
* **GET** method for `/categories`
* **GET** method for `/payments`

*(Note: Leave the Authorization setting for all OPTIONS methods as NONE so that browsers can perform pre-flight CORS verification seamlessly).*