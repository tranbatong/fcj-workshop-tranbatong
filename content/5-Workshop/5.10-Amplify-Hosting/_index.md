---
title : "CI/CD with AWS Amplify"
date : 2026-07-01
weight : 10
chapter : false
pre : " <b> 5.10. </b> "
---

#### Integrating CI/CD and Deploying Frontend with AWS Amplify

We utilize AWS Amplify to automate the Continuous Integration and Continuous Deployment (CI/CD) pipeline for our React SPA, along with automated SSL (HTTPS) certificate provisioning.

**Source Code Integration & Build Setup**
1. Navigate to the **AWS Amplify** service, scroll down to "Start building with Amplify", and click the **Create new app** button.
2. Select **GitHub** as the source code provider and click **Next** (Authorize your GitHub account if prompted).
3. Select the Repository containing your project source code (`serverless-idp-project`) and specify the deployment branch (e.g., the `main` branch).
4. Check the **My app is a monorepo** box and enter the root directory path of the Frontend (e.g., `idp-frontend`). Click **Next**.
![Amplify](/images/5-Workshop/5.10-Amplify-Hosting/amplify-1.png)
5. In the **App settings** step, ensure the configuration matches your React project settings:
   * **Frontend build command:** `npm run build`
   * **Build output directory:** `dist`
![Amplify](/images/5-Workshop/5.10-Amplify-Hosting/amplify-2.png)
6. Click **Next**
![Amplify](/images/5-Workshop/5.10-Amplify-Hosting/amplify-3.png)
7. Then click **Save and deploy**. Amplify will automatically pull the source code, execute the build command, and publish the web interface.

**Custom Domain Configuration**
1. Once the initial deployment is successful, navigate to the **Hosting** section on the left menu and select **Custom domains**.
![Amplify](/images/5-Workshop/5.10-Amplify-Hosting/amplify-4.png)
2. Click the **Add domain** button in the top right corner.
![Amplify](/images/5-Workshop/5.10-Amplify-Hosting/amplify-5.png)
3. Select the custom domain previously configured in Route 53 (e.g., `cses2.id.vn`) from the dropdown menu.
4. Configure Subdomains to route your `main` branch and set up a redirect from `www` to the root domain.
5. Click **Configure domain** and save. Amplify will automatically verify the DNS with Route 53 and issue an SSL certificate. Your IDP system is now securely accessible via HTTPS!