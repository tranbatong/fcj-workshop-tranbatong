---
title: "Worklog Week 2"
date: 2026-04-24
weight: 2
chapter: false
pre: " <b> 1.2. </b> "
---

### Week 2 Objectives:

- Consolidate account security knowledge and advanced user management on the IAM system.
- Research the theory and actual configuration of the Amazon VPC virtual network architecture.
- Practice dividing subnets, configuring routing, and setting up Security Groups to protect resource infrastructure.

### Tasks to Deploy This Week:

| Day | Task                                                                                                                                                                                                                         | Start Date | Completion Date | Documentation Source                      |
| --- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------- | --------------- | ----------------------------------------- |
| Mon | - Deeply research identity management and user security on the system <br> - Learn how to set up Multi-Factor Authentication (MFA) for the account                                                                           | 24/04/2026 | 24/04/2026      | First Cloud AI Journey Course             |
| Tue | - Practice permission handling in IAM, group management, and isolating privileges between Root User and IAM Users <br> - Create sub-accounts to serve daily operational tasks                                                | 25/04/2026 | 25/04/2026      | First Cloud AI Journey Course             |
| Wed | - Learn the theoretical foundations of Module 02 regarding Amazon Virtual Private Cloud (VPC) <br> - Explore core concepts: what a VPC is, public subnets, and private subnets                                               | 27/04/2026 | 27/04/2026      | First Cloud AI Journey Course             |
| Thu | - Learn about network routing mechanisms via Route Tables and Internet Gateways <br> - Research NAT Gateway solutions that allow private subnet instances to connect one-way to the internet                                 | 28/04/2026 | 28/04/2026      | <https://cloudjourney.awsstudygroup.com/> |
| Fri | - Design the network topology diagram for the practical Lab assignment <br> - Prepare IPv4 CIDR blocks for the VPC and subnets planned for initialization                                                                    | 29/04/2026 | 29/04/2026      | First Cloud AI Journey Course             |
| Sat | - Conduct the hands-on Lab on the AWS Management Console <br> - Initialize the VPC, partition public/private subnets, attach the Internet Gateway, configure Route Tables, and establish firewall rules with Security Groups | 30/04/2026 | 30/04/2026      | <https://cloudjourney.awsstudygroup.com/> |

### Week 2 Achievements:

| Day | Task                                            | Achievement                                                                                                                                                                                                                                                                                                                                         |
| --- | ----------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Mon | Multi-Factor Authentication (MFA) configuration | Successfully configured Multi-Factor Authentication (MFA) for the account environment, strengthening the system security shield.                                                                                                                                                                                                                    |
| Tue | IAM permissions & account management            | Ensured Root User safety by disabling active access keys. Managed and allocated permissions for the sub-user account truc-user within the Admin-groups for daily operations in compliance with regulations.                                                                                                                                         |
| Wed | Amazon VPC theoretical foundations              | Clearly understood the logic isolation nature of a Virtual Private Cloud (VPC) to separate development environments (dev, test, production). Mastered partitioning the network space into public and private subnets.                                                                                                                               |
| Thu | Network routing mechanism research              | Comprehended the operational behavior of Default route tables and Custom route tables. Learned how to utilize an Internet Gateway to open outbound internet traffic and how a NAT Gateway securely connects private subnet resources one-way.                                                                                                       |
| Fri | Infrastructure resource allocation planning     | Explicitly determined technical parameters, the 10.0.0.0/16 CIDR block, and planned clear associations for network components prior to live deployment on the console.                                                                                                                                                                              |
| Sat | Live implementation of Lab 03 (VPC deployment)  | Successfully initialized the virtual network named truc-vpc (IPv4 CIDR 10.0.0.0/16). Detailed configuration completed for truc-public-subnet1 and truc-private-subnet1. Attached the truc-igw gateway, created the truc-route-Public1 route table, and established two security groups allowing secure management of SSH, Ping, and HTTP protocols. |

---

### Practical Evidence Images:

**Monday: Multi-Factor Authentication (MFA) configuration**
![MFA](image.png)

**Tuesday: IAM permissions & account management**
![IAM](image-3.png)

**Wednesday: Amazon VPC theoretical foundations**

**Thursday: Network routing mechanism research**

**Friday: Infrastructure resource allocation planning**

**Saturday: Live implementation of Lab 03 (VPC deployment)**
![Your VPCs](image-1.png)
![Subnets](image-2.png)
