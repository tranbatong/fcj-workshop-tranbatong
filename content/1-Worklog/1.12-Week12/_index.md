---
title: "Worklog Week 12"
date: 2026-07-06
weight: 12
chapter: false
pre: " <b> 1.12. </b> "
---

### Week 12 Objectives:

- Finalize the security layer for the IDP architecture using Amazon Cognito (User Authentication) and AWS WAF (Web Application Firewall).
- Fully integrate the Frontend for secure communication with API Gateway and S3.
- Complete the Worklog report, write a Blog post sharing the project journey, and prepare Event/Workshop materials.
- Submit the final project and request feedback/reviews from FCJ Admin mentors to learn and improve.

### Tasks to Deploy This Week:

| Day | Task                                                                                                                                                                                                                                                              | Start Date | Completion Date | Documentation Source                      |
| --- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------- | --------------- | ----------------------------------------- |
| Mon | Set up a User Pool in Amazon Cognito to manage user authentication. Configure JWT Token Validation integration between Cognito and Amazon API Gateway to protect the Dashboard APIs, ensuring only valid authenticated users can access the data.                 | 06/07/2026 | 06/07/2026      | Amazon Cognito Guide, API Gateway Auth    |
| Tue | Deploy AWS WAF at the Global layer to protect the system from common web exploits (e.g., SQL Injection, XSS) and enforce rate limiting on API requests. Finalize the Frontend connection to S3 for file uploads and API Gateway for retrieving statistics.        | 07/07/2026 | 07/07/2026      | AWS WAF Documentation                     |
| Wed | Conduct a comprehensive End-to-End review of the entire system using real-world scenarios. Clean up the codebase, optimize configurations, and finalize the ultimate Serverless Intelligent Document Processing (IDP) architecture diagram.                       | 08/07/2026 | 08/07/2026      | Overall Architecture Diagram              |
| Thu | Consolidate all content from Week 1 to Week 12 to complete the Worklog site. Ensure that configuration details, practical evidence images, and achievements from each week are fully, clearly, and logically documented.                                          | 09/07/2026 | 09/07/2026      | Weekly Worklog Contents                   |
| Fri | Write a Blog post sharing the journey of building the IDP project on AWS, detailing the challenges faced and lessons learned. Design the presentation slides for the Event/Workshop session to share knowledge with the community.                                | 10/07/2026 | 10/07/2026      | Blog Template, Workshop Slides            |
| Sat | Package the final deliverables (Worklog, Blog, Event Slides) for course submission. Share project details in the community group to request reviews and constructive feedback from FCJ Admin mentors, aiming to refine skills and fix any remaining shortcomings. | 11/07/2026 | 11/07/2026      | <https://cloudjourney.awsstudygroup.com/> |

### Week 12 Achievements:

| Day | Task                                                | Achievement                                                                                                                                                                                                      |
| --- | --------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Mon | Integrating Amazon Cognito and securing APIs        | The application now has a secure login screen. API Gateway automatically rejects requests without a valid JWT Token, significantly enhancing the security of the data system.                                    |
| Tue | Deploying AWS WAF and finalizing Frontend           | AWS WAF is active and successfully blocking malicious IPs and spam requests. The Frontend is fully operational, allowing invoice uploads to S3 and displaying charts and invoice lists fetched from API Gateway. |
| Wed | Comprehensive testing and system optimization       | The IDP architecture runs stably and smoothly. The final architecture diagram has been saved for the report. Minor vulnerabilities in IAM configurations have been completely patched.                           |
| Thu | Finalizing the Worklog site                         | The Hugo Worklog system is beautifully presented with complete content from Week 1 to Week 12. Practical evidence images and execution steps are documented professionally, ready for submission.                |
| Fri | Completing Blog and Event/Workshop materials        | Completed a high-quality Blog post summarizing the entire AWS Serverless project journey. The Workshop presentation file is visually designed and easy to understand for presenting to the panel.                |
| Sat | Submitting the project and gathering Admin feedback | The entire project was submitted on time. Received highly valuable feedback from FCJ Admin mentors, noting areas for improvement (such as advanced CI/CD and Monitoring) to guide future learning paths.         |
