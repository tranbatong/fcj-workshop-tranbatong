---
title: "Event Report: AI Innovations & Cloud Foundations"
date: 2026-06-29
weight: 2
chapter: false
pre: " <b> 4.2. </b> "
---

### Purpose of the Event

- Update trends in AI-integrated system design, especially Multi-Agent architecture and context management.
- Understand the technical nature and how to optimize parameters of Large Language Models (LLMs).
- Share solutions for cost optimization and network infrastructure security in Cloud environments.
- Summarize practical experiences from Hackathons and real-world product development processes.

### List of Speakers

- **Vy Lam** - Senior Business Systems Analyst, VPBank
- **Duc Dao** - Solution Architect, Cloud Kinetics
- **Team VIB** - Competing team at Lotus Hacks 2026
- **Nguyen Tuan Thinh** - DevOps Engineer
- **Tinh Truong** - Platform Engineer, GoTymeX
- **Pham Ng Hai Anh** - G-AsiaPacific Vietnam, AWS Community Builder

### Key Highlights

#### Enterprise-Grade Multi-Agent System

- Traditional startup credit scoring systems often lack historical financial data.
- The Multi-Agent solution operates as a virtual committee with specialized Agents (Financial Analyst, Risk Assessor, etc.).
- The results help reduce processing time and costs by 95%, enhancing cross-checking capabilities and security compared to a Single Agent.

#### Non-Determinism of LLMs

- Setting Temperature = 0 does not guarantee identical results due to microscopic rounding errors in GPU floating-point operations.
- It is recommended to use Temperature = 0.1 to avoid repetitive loops.
- It is advisable to combine multiple runs for majority voting and enforce structured outputs like JSON mode.

#### Learnings from Lotus Hacks

- The 36-hour journey of building UTMorpho (Sketch2App), a tool that converts UI sketches into frontend code.
- Major challenges included Claude API Token Limits, Scope Creep, and widespread bug generation by AI.
- The core lesson is to maintain team synchronization and prioritize delivering the core value first.

#### Building Infrastructure Foundations with CloudFront

- Cost concerns due to unpredictable traffic spikes or DDoS attacks can be mitigated via a global Edge network.
- Data Transfer Out (DTO) from AWS Origins is completely free.
- Provides Origin Cloaking via Origin Access Control (OAC) to completely hide origin servers from the public internet.

#### The Importance of Context in AI

- AI providing incorrect answers is often due to weak or noisy context.
- Stuffing irrelevant documents wastes tokens and reduces accuracy.
- The future trend is shifting from single prompts to contextual memory systems for effective personalization.

#### Amazon Q Application and Automated Auditing

- Amazon Q acts as a unified assistant, helping generate meeting minutes, send emails, schedule, and retrieve data from over 40 sources.
- Ensures security compliance and Role-Based Access Control (RBAC) when enterprises adopt AI.
- Integrates GenAI to perform automated infrastructure security audits on cloud systems.

### What Was Learned

#### Core Technical Mindset

- Accept the inherent probabilistic nature of AI models and proactively build error-handling mechanisms and output structure validation.
- Understand the difference between stuffing raw data and building an effective contextual memory system.

#### System Design

- Grasp the Multi-Agent model to solve complex business problems requiring transparency and cross-referencing.
- Understand how to deploy infrastructure protection at the Edge layer rather than focusing solely on internal application servers.

#### Deployment Strategy

- Avoid Scope Creep in the early stages of a project.
- Leverage available services like Lambda@Edge and CloudFront for flexible failover handling.

### Application to Work

- Enforce JSON return formats for AI processing flows integrated into backend APIs for easy data extraction and storage in MongoDB.
- Apply the Origin Access Control (OAC) mechanism combined with the current network architecture to completely hide Spring Boot and Node.js servers from the internet, enhancing system security.
- Experiment with breaking down complex processing logic into a Multi-Agent approach for diagnostic or analytical modules, rather than relying on a single processing thread.
- Utilize Amazon Q to automate document writing and initialize structures for test cases, integrating directly into the CI/CD pipeline on GitHub Actions to shorten development time.

### Experience at the Event

Attending the event helped broaden my perspective from merely writing application code to a systematic approach to system design and AI integration. Some notable experiences:

#### Deep Dive into the Technical Nature of AI

- The presentations went beyond the application level and delved into the hardware nature, explaining why LLMs are not completely deterministic, helping me establish more realistic parameter settings.

#### Accessing Modern Infrastructure Architecture

- Gained a clearer understanding of techniques for anonymizing origin servers and controlling data flow on the cloud, a crucial factor when deploying systems that require high availability and strict security.

#### Learning from Real-World Problems

- The practical experience from the Hackathon team is the clearest proof of feature limitation and risk management when using third-party APIs under time pressure.
- The banking industry's approach to Multi-Agent systems provides great inspiration for restructuring traditional data processing flows.

#### Key Takeaways

- No single technological solution is absolutely perfect; understanding AI's limitations (such as token limits, non-determinism) helps build more robust software.
- Infrastructure cost optimization needs to be calculated right from the Edge network design phase, rather than just at the application code level.

> Overall, the event provided me with in-depth knowledge of both AI and Cloud, while also offering practical guidelines for upgrading system architecture, improving scalability, and ensuring safety for real-world applications.
