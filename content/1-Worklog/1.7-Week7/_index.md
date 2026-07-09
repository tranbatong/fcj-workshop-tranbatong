---
title: "Worklog Week 7"
date: 2026-06-01
weight: 7
chapter: false
pre: " <b> 1.7. </b> "
---

### Objectives for Week 7:

- Deep dive into Windows enterprise storage features on the Cloud via Amazon FSx.
- Research the security platform based on AWS's "Security is Job Zero" philosophy.
- Master the Shared Responsibility Model, advanced identity management, organization management, and centralized data encryption.

### Tasks to Implement This Week:

| Day | Tasks                                                                                                                                                                                                                                                                                                                                | Start Date | End Date   | Source Materials     |
| --- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ---------- | ---------- | -------------------- |
| Mon | Initialize a Multi-AZ NTFS-standard file system with SSD and HDD configurations on Amazon FSx to ensure disaster recovery. Configure SMB-standard shared folders connected directly to Microsoft Active Directory for centralized user management.                                                                                   | 01/06/2026 | 01/06/2026 | AWS FCAJ 2026 Course |
| Tue | Set up storage quotas for users and centrally manage connection sessions and open files. Practice flexibly scaling storage capacity and throughput capacity when load increases without disrupting services.                                                                                                                         | 02/06/2026 | 02/06/2026 | AWS FCAJ 2026 Course |
| Wed | Research the Shared Responsibility Model, where AWS ensures the security of hardware, global physical infrastructure, and foundational software layers.                                                                                                                                                                              | 03/06/2026 | 03/06/2026 | AWS FCAJ 2026 Course |
| Thu | Learn Root Account Best Practices such as locking the root account and splitting password/hardware MFA information. Configure IAM Policy using JSON, prioritizing explicit Deny rules, and use IAM Role (AssumeRole) to grant temporary permissions. Avoid directly embedding fixed access keys into application source code on EC2. | 04/06/2026 | 04/06/2026 | AWS FCAJ 2026 Course |
| Fri | Centrally manage accounts via AWS Organizations with consolidated billing and Service Control Policies (SCP). Set up a Single Sign-On (SSO) mechanism via AWS Identity Center. Research the Amazon Cognito authentication solution and the AWS KMS centralized key management service.                                               | 05/06/2026 | 05/06/2026 | AWS FCAJ 2026 Course |
| Sat | Execute the resource cleanup process (Cost Optimization) using the Delete file system command on FSx without saving a final backup. Delete recovery points in AWS Backup and delete the Lab 25 Stack on CloudFormation to reclaim testing EC2 servers.                                                                               | 06/06/2026 | 06/06/2026 | AWS FCAJ 2026 Course |

### Achievements for Week 7:

| Day | Tasks                                  | Achievements                                                                                                                                                                             |
| --- | -------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Mon | Initialize Windows storage system      | Simultaneously deployed the Amazon FSx file system across multiple availability zones (Multi-AZ) and successfully set up SMB-standard shared folders connected to Active Directory.      |
| Tue | Optimize FSx system                    | Mastered the skills of administering, monitoring performance, and optimizing the capacity of large-scale enterprise Windows storage systems on Amazon FSx.                               |
| Wed | Research security architecture         | Clearly understood AWS's scope of responsibility (Security of the Cloud) regarding hardware safety and global infrastructure.                                                            |
| Thu | Access rights management (IAM)         | Deeply understood and practiced designing "Zero Trust" systems and multi-layered access control. Mastered how to avoid using direct access keys and grant temporary permissions via STS. |
| Fri | Hierarchical management and encryption | Understood how to apply Service Control Policies (SCP) to set maximum permission boundaries in Organizations and apply KMS encryption mechanisms to protect data at rest.                |
| Sat | Optimize costs                         | Successfully cleaned up FSx file systems, AWS Backup recovery points, and CloudFormation stacks, automatically reclaiming all dependent resources to save costs.                         |

---

### Plans for Next Week:

- Continue executing the Module's labs.
