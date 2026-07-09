---
title: "Worklog Week 5"
date: 2026-05-18
weight: 5
chapter: false
pre: " <b> 1.5. </b> "
---

### Objectives for Week 5:

- Handle advanced scenarios regarding cloud network scaling by building a central router, AWS Transit Gateway.
- Master the core characteristics of EC2 virtual servers, including Instance categorization, storage mechanisms, auto-scaling systems, and shared network files.
- Implement solutions for data security, automated backups, and Disaster Recovery using AWS Backup and Amazon SNS.

### Tasks to Implement This Week:

| Day | Tasks                                                                                                                                                                                                                            | Start Date | End Date   | Source Materials                          |
| --- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------- | ---------- | ----------------------------------------- |
| Mon | - Deep dive into Module 03 on EC2: CPU chip classifications (Intel, AMD, ARM/Graviton) and cost optimization methods <br> - Differentiate the storage mechanisms between EBS Volume and Instance Store (ephemeral storage)       | 18/05/2026 | 18/05/2026 | First Cloud AI Journey Course             |
| Tue | - Learn about EC2 User Data & Metadata features, Auto Scaling & Load Balancing mechanisms <br> - Research shared network storage solutions (Amazon EFS, FSx) and the system migration service AWS MGN                            | 19/05/2026 | 19/05/2026 | First Cloud AI Journey Course             |
| Wed | - Practice Lab 20 (AWS Transit Gateway): Use CloudFormation to quickly provision an infrastructure of 4 VPCs and 4 EC2 servers <br> - Initialize the central router Transit Gateway to solve the VPC Peering scaling issue       | 20/05/2026 | 20/05/2026 | First Cloud AI Journey Course             |
| Thu | - Create Transit Gateway Attachments to link 4 VPCs to the central network <br> - Configure the TGW route table (Associations, Propagations) and update the Route Table of each VPC to route traffic through the TGW             | 21/05/2026 | 21/05/2026 | First Cloud AI Journey Course             |
| Fri | - Practice Lab 13 (AWS Backup): Build a Backup Plan defining backup rules and initialize a KMS-encrypted Backup Vault <br> - Configure Amazon SNS to create a Topic for sending backup alerts to the admin email                 | 22/05/2026 | 22/05/2026 | First Cloud AI Journey Course             |
| Sat | - Test the network via Reachability Analyzer and perform cross-SSH testing between VPCs. Execute a Restore Test to recover an EC2 server <br> - Execute the cleanup process for all resources (Backup, SNS, TGW, CloudFormation) | 23/05/2026 | 23/05/2026 | <https://cloudjourney.awsstudygroup.com/> |

### Achievements for Week 5:

| Day | Tasks                                                   | Achievements                                                                                                                                                                                                                                   |
| --- | ------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Mon | Research EC2 virtual server architecture                | Deeply understood CPU selection strategies (especially the Graviton chip series which saves 40% in costs). Differentiated the 99.999% availability of EBS storage networks compared to the read/write speed of physical Instance Store drives. |
| Tue | Scaling mechanisms and network storage                  | Mastered how to automatically run scripts using User Data and fetch internal information via Metadata. Understood the NFSv4 standard file sharing mechanism (EFS) and data deduplication in SMB (FSx).                                         |
| Wed | Initialize centralized network infrastructure in Lab 20 | Successfully built the pre-configured CloudFormation Stack for 4 independent VPCs. Clearly understood the advantages of the Hub-and-Spoke model (Transit Gateway) over the Mesh connection of VPC Peering.                                     |
| Thu | Configure AWS Transit Gateway routing                   | Successfully linked virtual networks to the central gateway via TGW Attachments, performed automated route propagation, and ensured seamless routing from VPCs to the TGW.                                                                     |
| Fri | Deploy automated AWS Backup solution                    | Successfully set up a secure system backup plan into the Backup-LAB-VAULT, while successfully activating the automated incident alerting feature via Email using Amazon SNS.                                                                   |
| Sat | Test the system and optimize resources                  | Confirmed seamless Private network connections between VPC 1, VPC 2, VPC 3, and VPC 4. Successfully restored servers from a Recovery Point. Completely cleaned up all practice resources to avoid incurring costs.                             |

---

### Practical Proof Images of the Lab:

#### 1. Initialize Lab 20 Network Infrastructure via CloudFormation

The system reports the successful deployment of the Lab20-Stack, automatically creating 4 VPC networks and accompanying EC2 servers for the Transit Gateway lab.
![alt text](image.png)

#### 2. Initialize the Central Router AWS Transit Gateway

The interface shows the central connection gateway lab20-tgw has been successfully initialized and is in the Available state.
![alt text](image-1.png)

#### 3. Configure Network Links (Transit Gateway Attachments)

Successfully attached all 4 independent VPC networks to the Transit Gateway, forming a Hub-and-Spoke centralized network model.
![alt text](image-2.png)

#### 4. Configure TGW Route Table - Associations Tab

The Transit Gateway route table records the successfully Associated VPCs, ready for routing.
![alt text](image-6.png)

#### 5. Configure TGW Route Table - Propagations Tab

Successfully activated the automatic route Propagation feature, allowing the Transit Gateway to automatically recognize the IP ranges of the 4 connected VPC networks.
![alt text](image-7.png)

#### 6. Update Route Tables at the VPCs

Network routing at the VPCs has been fine-tuned, establishing a path for the 172.16.0.0/16 IP range pointing directly to the Transit Gateway instead of the Internet.
![alt text](image-8.png)

#### 7. SSH into the Bastion Host Server (VPC 1)

Successfully used MobaXterm to access the EC2 server located in VPC 1 (IP 100.48.207.178) as a jump host (Bastion Host) in preparation for network testing.
![alt text](image-3.png)

#### 8. Check Internet Connection from the Bastion Server

Successfully executed the ping amazon.com and ping google.com commands from the VPC 1 server to ensure the server has a stable external network connection before testing the internal network.
![alt text](image-7.png)

#### 9. Execute the ping 172.16.2.5 command (VPC 2). Although the ping failed (100% packet loss) due to the Security Group not allowing ICMP, network routing is clear

From the Bastion server in VPC 1, execute the ping command to 172.16.2.5 (VPC 2). The successful response data proves the central network has routed seamlessly.
![alt text](image-4.png)

#### 10. Cross-SSH to VPC 2 and Continue Testing to VPC 3

Used the key file (tgw-key.pem) to SSH directly from the jump host in VPC 1 to the Private IP of the server in VPC 2 (172.16.2.5). Immediately after, successfully executed a ping command to the IP range of VPC 3 (172.16.3.7).
![alt text](image-9.png)

#### 11. Complete Comprehensive Routing Check (VPC 4)

Continued the Transit Gateway central network testing flow by successfully pinging from the current server to the IP range of VPC 4 (172.16.4.6). The network system of all 4 VPCs is completely and securely interconnected.
![alt text](image-10.png)
