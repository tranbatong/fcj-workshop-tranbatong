---
title : "Create User Pool & App Client"
date : 2026-07-01
weight : 1
chapter : false
pre : " <b> 5.6.1. </b> "
---

#### Initialize User Pool
1. Navigate to the **Amazon Cognito** service on the AWS Console and select **Create user pool**.
2. **Options for sign-in identifiers**: Check **Email**.
3. In the sign-up experience step, locate the **Self-registration** section and **Uncheck** *Enable self-registration* (This secures the system by preventing strangers from freely registering accounts).
4. **Required attributes for sign-up**: Open the dropdown menu and select both **email** and **name**.

#### Initialize App Client
1. Proceed to the Integrate your app step.
2. **Application type**: Select **Single-page application (SPA)** (Since we are using ReactJS).
3. **Name your application**: Enter `idp-react-app`.
4. Scroll to the bottom and click **Create user pool**.

![Create UserPool](/images/5-Workshop/5.6-identity-Cognito/user-pool.png)

After creation, copy the `User pool ID` and `Client ID` to paste into the `cognitoConfig.js` configuration file in your React source code.

#### Create a Test User
Since open registration is disabled, you must manually provision accounts for your staff:
1. Access your newly created User Pool, go to the **Users** tab (under User management), and click **Create user**.
2. Enter a username and the user's email address.
3. Enter a temporary password.
4. Check the **Mark email as verified** box to confirm the email is valid.

![Create User](/images/5-Workshop/5.6-identity-Cognito/create-user.png)

5. Click **Create user**. (Upon their first login on the Frontend, the user will be prompted to change this temporary password and provide their full name).
