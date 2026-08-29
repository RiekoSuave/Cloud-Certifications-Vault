## Core Concept

The SAA exam becomes much easier when you recognize:

**Scenario patterns**

instead of trying to recall:

**Every detail of every service**

> [!tip] Memory Trick
> **Clue → Pattern → Service**

---

# Availability Recognition

If you see:

**Survive one EC2 failure**

→ Auto Scaling

If you see:

**Survive one Availability Zone failure**

→ Multi-AZ

If you see:

**Survive complete Region failure**

→ Multi-Region

If you see:

**Relational database automatic failover**

→ RDS Multi-AZ

If you see:

**More relational database reads**

→ Read Replica

### Killer Shortcut

> **FAILURE**
> → AVAILABILITY
>
> **READ LOAD**
> → SCALING

---

# Compute Recognition

If you see:

**Unpredictable EC2 traffic**

→ Auto Scaling

If you see:

**Distribute web traffic**

→ Load Balancer

If you see:

**Short-lived event-driven code**

→ Lambda

If you see:

**Long-running custom process**

→ EC2 / ECS / EKS depending on requirements

If you see:

**Fault-tolerant interruptible workload**

→ Spot Instances

If you see:

**Steady long-term compute**

→ Savings Plans / Reserved pricing

---

# Scaling Recognition

If you see:

**Bigger server**

→ Vertical Scaling

If you see:

**More servers**

→ Horizontal Scaling

If you see:

**Keep CPU near target**

→ Target Tracking

If you see:

**Different scaling amounts at different thresholds**

→ Step Scaling

If you see:

**Known daily spike**

→ Scheduled Scaling

If you see:

**Forecast recurring demand**

→ Predictive Scaling

---

# Stateless Recognition

If you see:

**Auto Scaling instances losing user sessions**

→ Externalize session state

If you see:

**Fast shared sessions**

→ ElastiCache

If you see:

**Durable serverless state**

→ DynamoDB

If you see:

**User-uploaded files disappearing with EC2 termination**

→ S3

If you see:

**Shared mounted Linux files**

→ EFS

### Memory Trick

> **SESSION**
> → ELASTICACHE / DYNAMODB
>
> **OBJECT**
> → S3
>
> **SHARED FILESYSTEM**
> → EFS

---

# Decoupling Recognition

If you see:

**Backend cannot keep up**

→ SQS

If you see:

**Traffic spike must not be lost**

→ SQS

If you see:

**Long-running work should not block request**

→ SQS / Async Processing

If you see:

**One event to many consumers**

→ SNS

If you see:

**One event to many durable independent consumers**

→ SNS + SQS

If you see:

**Route events based on event content**

→ EventBridge

If you see:

**Multiple ordered workflow steps**

→ Step Functions

---

# SQS Recognition

If you see:

**Strict order**

→ FIFO Queue

If you see:

**Message processed more than once**

→ Idempotent Consumer

If you see:

**Message becomes visible before processing finishes**

→ Increase Visibility Timeout

If you see:

**Repeatedly failing message**

→ DLQ

If you see:

**Too many empty receive requests**

→ Long Polling

If you see:

**Delay processing after send**

→ Delay Queue

---

# Caching Recognition

If you see:

**Global static content**

→ CloudFront

If you see:

**Repeated database reads**

→ ElastiCache

If you see:

**Repeated DynamoDB reads**

→ DAX

If you see:

**Repeated API responses**

→ API Gateway Cache

If you see:

**Need more database read capacity but data is not highly repetitive**

→ Read Replica

### Killer Shortcut

> **REPEATED SAME DATA**
> → CACHE
>
> **MORE DIFFERENT READS**
> → READ REPLICA

---

# Storage Recognition

If you see:

**Object storage**

→ S3

If you see:

**Block storage for EC2**

→ EBS

If you see:

**Shared Linux filesystem**

→ EFS

If you see:

**Windows file shares**

→ FSx for Windows File Server

If you see:

**High-performance Lustre-style workload**

→ FSx for Lustre

---

# S3 Recognition

If you see:

**Unknown access pattern**

→ Intelligent-Tiering

If you see:

**Automatically move older objects to cheaper storage**

→ Lifecycle Policy

If you see:

**Long-term archive**

→ Glacier class

If you see:

**Recover overwritten object**

→ Versioning

If you see:

**Prevent deletion/overwrite during retention**

→ Object Lock

If you see:

**Copy objects to another Region**

→ Cross-Region Replication

---

# EBS Recognition

If you see:

**Point-in-time EC2 volume backup**

→ EBS Snapshot

If you see:

**Need snapshot available in another Region**

→ Cross-Region Snapshot Copy

If you see:

**General-purpose SSD with configurable performance**

→ gp3

---

# Relational Database Recognition

If you see:

**Managed MySQL/PostgreSQL/SQL Server/Oracle**

→ RDS

If you see:

**AWS-optimized relational database**

→ Aurora

If you see:

**Automatic failover**

→ Multi-AZ

If you see:

**Read scaling**

→ Read Replica

If you see:

**Cross-Region Aurora DR**

→ Aurora Global Database

If you see:

**Highly variable Aurora workload**

→ Aurora Serverless

---

# DynamoDB Recognition

If you see:

**Key-value / document**

→ DynamoDB

If you see:

**Massive scale with minimal operations**

→ DynamoDB

If you see:

**Unpredictable traffic**

→ On-Demand

If you see:

**Predictable steady traffic**

→ Provisioned Capacity

If you see:

**Multi-Region writes**

→ Global Tables

If you see:

**React to item changes**

→ DynamoDB Streams

If you see:

**Extremely fast repeated reads**

→ DAX

---

# Analytics Recognition

If you see:

**Query S3 with SQL**

→ Athena

If you see:

**Data warehouse**

→ Redshift

If you see:

**ETL / Data Catalog**

→ Glue

If you see:

**Big-data processing**

→ EMR

If you see:

**Search / log analytics**

→ OpenSearch

If you see:

**Real-time streaming ingestion**

→ Kinesis

---

# Networking Recognition

If you see:

**Public Internet access for public subnet**

→ Internet Gateway

If you see:

**Private subnet outbound IPv4 Internet**

→ NAT Gateway

If you see:

**Two VPCs**

→ VPC Peering

If you see:

**Many VPCs + transitive routing**

→ Transit Gateway

If you see:

**One private service exposed to consumers**

→ PrivateLink

If you see:

**Private AWS service access**

→ VPC Endpoint

---

# VPC Endpoint Recognition

If you see:

**Private S3**

→ Gateway Endpoint

If you see:

**Private DynamoDB**

→ Gateway Endpoint

If you see:

**Private Secrets Manager**

→ Interface Endpoint

If you see:

**ENI-based endpoint**

→ Interface Endpoint

If you see:

**Route-table endpoint**

→ Gateway Endpoint

### Memory Trick

> **S3 + DYNAMODB**
> → GATEWAY
>
> **MOST OTHER SUPPORTED SERVICES**
> → INTERFACE

---

# VPC Peering Recognition

If you see:

**Two non-overlapping VPCs**

→ VPC Peering

If you see:

**Transitive routing**

→ NOT Peering

If you see:

**Overlapping CIDRs**

→ Standard Peering is not appropriate

If you see:

**Many VPCs**

→ Transit Gateway

---

# PrivateLink Recognition

If you see:

**Specific private service**

→ PrivateLink

If you see:

**Many consumer VPCs**

→ PrivateLink

If you see:

**Avoid full VPC network connectivity**

→ PrivateLink

If you see:

**Overlapping consumer/provider CIDRs**

→ PrivateLink can be a strong fit

---

# Hybrid Connectivity Recognition

If you see:

**Quick encrypted on-premises connection**

→ Site-to-Site VPN

If you see:

**Dedicated predictable on-premises connection**

→ Direct Connect

If you see:

**Direct Connect backup**

→ Site-to-Site VPN

If you see:

**Remote employee**

→ Client VPN

If you see:

**On-premises network to many VPCs**

→ VPN / Direct Connect + Transit Gateway

---

# Direct Connect Recognition

If you see:

**Private VPC resources**

→ Private VIF

If you see:

**AWS public endpoints**

→ Public VIF

If you see:

**Transit Gateway**

→ Transit VIF

If you see:

**Many VPCs**

→ Direct Connect Gateway + Transit Gateway

If you see:

**Encryption required over DX**

→ VPN over Direct Connect or supported encrypted option

---

# Hybrid DNS Recognition

If you see:

**On-prem resolves AWS private DNS**

→ Inbound Resolver Endpoint

If you see:

**AWS resolves on-prem DNS**

→ Outbound Resolver Endpoint

If you see:

**Specific corporate domain forwarded**

→ Resolver Rule

### Memory Trick

> **ON-PREM → AWS**
> → INBOUND
>
> **AWS → ON-PREM**
> → OUTBOUND

---

# Security Group Recognition

If you see:

**Resource-level firewall**

→ Security Group

If you see:

**Stateful**

→ Security Group

If you see:

**Reference another SG**

→ Security Group

If you see:

**Explicit deny**

→ NOT Security Group

---

# NACL Recognition

If you see:

**Subnet-level**

→ NACL

If you see:

**Stateless**

→ NACL

If you see:

**Explicit allow and deny**

→ NACL

If you see:

**First matching numbered rule**

→ NACL

---

# IAM Recognition

If you see:

**Who can call AWS APIs**

→ IAM

If you see:

**EC2/Lambda needs AWS access without keys**

→ IAM Role

If you see:

**Workforce access across accounts**

→ IAM Identity Center

If you see:

**Organization-wide permissions guardrail**

→ SCP

If you see:

**Temporary credentials**

→ STS

---

# Encryption Recognition

If you see:

**Managed encryption keys**

→ KMS

If you see:

**Dedicated HSM**

→ CloudHSM

If you see:

**Database password/API key**

→ Secrets Manager

If you see:

**Secret rotation**

→ Secrets Manager

If you see:

**Managed TLS certificate**

→ ACM

---

# Web Security Recognition

If you see:

**SQL injection**

→ WAF

If you see:

**XSS**

→ WAF

If you see:

**Rate-based blocking**

→ WAF

If you see:

**DDoS**

→ Shield

If you see:

**Advanced VPC traffic inspection**

→ Network Firewall

---

# Detection Recognition

If you see:

**Suspicious behavior / malicious IP**

→ GuardDuty

If you see:

**CVE / vulnerable software**

→ Inspector

If you see:

**Sensitive data in S3**

→ Macie

If you see:

**Central security findings**

→ Security Hub

If you see:

**Resource compliance**

→ Config

---

# Logging Recognition

If you see:

**Who changed this AWS resource?**

→ CloudTrail

If you see:

**Metrics / alarms / logs**

→ CloudWatch

If you see:

**Source/destination IP + ACCEPT/REJECT**

→ VPC Flow Logs

If you see:

**DNS query history**

→ Route 53 Resolver Query Logging

---

# Serverless Recognition

If you see:

**Run code on event**

→ Lambda

If you see:

**Managed API**

→ API Gateway

If you see:

**User sign-up/sign-in**

→ Cognito

If you see:

**Workflow orchestration**

→ Step Functions

If you see:

**Minimal operations + unpredictable API**

→ API Gateway + Lambda + DynamoDB

---

# Container Recognition

If you see:

**Managed container orchestration without Kubernetes requirement**

→ ECS

If you see:

**Kubernetes requirement**

→ EKS

If you see:

**Run containers without managing EC2 hosts**

→ Fargate

### Memory Trick

> **ECS**
> → AWS CONTAINERS
>
> **EKS**
> → KUBERNETES
>
> **FARGATE**
> → NO SERVERS TO MANAGE

---

# Disaster Recovery Recognition

If you see:

**How much data can be lost**

→ RPO

If you see:

**How long can app be down**

→ RTO

If you see:

**Backups only**

→ Backup and Restore

If you see:

**Core running**

→ Pilot Light

If you see:

**Whole stack running small**

→ Warm Standby

If you see:

**Whole stack production-capable**

→ Multi-Site

### Master Memory Trick

> **BACKUP**
> → BUILD
>
> **PILOT**
> → START
>
> **WARM**
> → SCALE
>
> **MULTI-SITE**
> → ROUTE

---

# Elastic Disaster Recovery Recognition

If you see:

**Continuous server replication**

→ Elastic Disaster Recovery

If you see:

**Block-level replication**

→ Elastic Disaster Recovery

If you see:

**On-premises servers replicated into AWS**

→ Elastic Disaster Recovery

If you see:

**Low-cost staging + launch recovery servers later**

→ Elastic Disaster Recovery

---

# Cost Recognition

If you see:

**Underutilized EC2**

→ Right-size

If you see:

**Variable EC2 traffic**

→ Auto Scaling

If you see:

**Steady long-term compute**

→ Savings Plans / Reserved pricing

If you see:

**Interruptible workload**

→ Spot

If you see:

**S3 data ages over time**

→ Lifecycle Policy

If you see:

**Unknown S3 access**

→ Intelligent-Tiering

If you see:

**High NAT cost for S3**

→ Gateway Endpoint

---

# Operational Overhead Recognition

If you see:

**Least operational overhead**

favor:

- Serverless
- Managed databases
- Managed messaging
- Managed security services

over:

**Self-managed EC2 solutions**

when both satisfy:

**The requirements**

### Memory Trick

> **AWS Manages More**
> → You Manage Less

---

# Global Architecture Recognition

If you see:

**Global cached content**

→ CloudFront

If you see:

**Static anycast IPs + global traffic acceleration**

→ Global Accelerator

If you see:

**Lowest-latency DNS routing**

→ Route 53 Latency-Based Routing

If you see:

**Multi-Region Aurora**

→ Aurora Global Database

If you see:

**Multi-Region DynamoDB writes**

→ Global Tables

---

# Route 53 Recognition

If you see:

**Primary/secondary DNS failover**

→ Failover Routing

If you see:

**Send user to lowest-latency Region**

→ Latency-Based Routing

If you see:

**Distribute fixed percentages**

→ Weighted Routing

If you see:

**User location determines endpoint**

→ Geolocation Routing

If you see:

**Resource location and traffic bias**

→ Geoproximity Routing

If you see:

**Many records + health checks**

→ Multi-Value Answer

---

# Architecture Pattern — Highly Available Web App

Requirements:

- Variable traffic
- Survive AZ failure
- Relational database

Think:

Users  
↓  
ALB  
↓  
Auto Scaling Across Multiple AZs  
↓  
RDS Multi-AZ

---

# Architecture Pattern — Read-Heavy Web App

Users  
↓  
ALB  
↓  
Auto Scaling  
↓  
ElastiCache  
↓  
RDS Read Replicas  
↓  
Primary RDS

### Recognition

Repeated reads  
→ Cache

Remaining read load  
→ Read Replicas

---

# Architecture Pattern — Async Processing

Users  
↓  
Application  
↓  
SQS  
↓  
Auto Scaling Workers

### Recognition

Traffic burst  
→ Queue

Backlog grows  
→ Scale Workers

---

# Architecture Pattern — Fan-Out

Event  
↓  
SNS  
↓  
├── SQS Billing
├── SQS Shipping
└── SQS Analytics

### Recognition

One event  
→ Many independent processors

---

# Architecture Pattern — Serverless API

Users  
↓  
API Gateway  
↓  
Lambda  
↓  
DynamoDB

Optional:

Cognito  
→ Authentication

SQS  
→ Async work

---

# Architecture Pattern — Global Static Site

Users  
↓  
CloudFront  
↓  
S3

### Recognition

Static + Global + Low Latency

---

# Architecture Pattern — Private Three-Tier App

Internet  
↓  
Public ALB  
↓  
Private Application Subnets  
↓  
Private Database Subnets

Security:

ALB SG  
↓  
App SG  
↓  
DB SG

---

# Architecture Pattern — Hybrid Network

On-Premises  
↓  
VPN or Direct Connect  
↓  
Transit Gateway  
↓  
Multiple VPCs

Hybrid DNS:

Route 53 Resolver

---

# Architecture Pattern — Regional DR

Primary Region  
↓  
Replication  
↓  
Secondary Region

Then identify:

Backups  
→ Backup & Restore

Core  
→ Pilot Light

Small Full Stack  
→ Warm Standby

Full Stack  
→ Multi-Site

---

# Architecture Pattern — Private AWS Service Access

Private EC2  
↓  
VPC Endpoint  
↓  
AWS Service

S3 / DynamoDB  
→ Gateway

Most other supported services  
→ Interface

---

# Architecture Pattern — Centralized Network Inspection

Spoke VPCs  
↓  
Transit Gateway  
↓  
Inspection VPC  
↓  
Network Firewall

### Recognition

Many VPCs + Central Inspection

---

# Architecture Pattern — Cost-Optimized Batch

Jobs  
↓  
SQS  
↓  
Auto Scaling Workers  
↓  
Spot Instances

### Recognition

Fault-tolerant + Flexible + Large workload

---

# Killer Pair Recognition

| If You See | Think |
|---|---|
| HA vs Reads | Multi-AZ vs Read Replica |
| Queue vs Broadcast | SQS vs SNS |
| Event Routing vs Workflow | EventBridge vs Step Functions |
| Edge Cache vs Network Accelerator | CloudFront vs Global Accelerator |
| Resource vs Subnet Firewall | SG vs NACL |
| Two vs Many VPCs | Peering vs Transit Gateway |
| Network vs Service Access | Peering vs PrivateLink |
| Quick vs Dedicated Hybrid | VPN vs Direct Connect |
| API Audit vs Monitoring | CloudTrail vs CloudWatch |
| Threat vs Vulnerability | GuardDuty vs Inspector |
| Key vs Secret | KMS vs Secrets Manager |
| Core vs Small Full Stack | Pilot Light vs Warm Standby |
| Data Loss vs Downtime | RPO vs RTO |

---

# Final Recognition Table

| Exam Clue | Answer |
|---|---|
| AZ Failure | Multi-AZ |
| Region Failure | Multi-Region |
| Read Scaling | Read Replica |
| Repeated Reads | Cache |
| Web Scale | ALB + Auto Scaling |
| Buffer | SQS |
| Fan-Out | SNS |
| Fan-Out + Buffer | SNS + SQS |
| Event Routing | EventBridge |
| Workflow | Step Functions |
| Global Static | CloudFront |
| Static Global IPs | Global Accelerator |
| Object Storage | S3 |
| Block Storage | EBS |
| Shared Linux Files | EFS |
| Relational DB | RDS / Aurora |
| Serverless NoSQL | DynamoDB |
| Private S3 | Gateway Endpoint |
| Private AWS Service | Interface Endpoint |
| Two VPCs | VPC Peering |
| Many VPCs | Transit Gateway |
| One Private Service | PrivateLink |
| Quick Hybrid | Site-to-Site VPN |
| Dedicated Hybrid | Direct Connect |
| Remote User | Client VPN |
| Hybrid DNS | Route 53 Resolver |
| Explicit Deny | NACL |
| Workload Credentials | IAM Role |
| Encryption Key | KMS |
| Secret Rotation | Secrets Manager |
| SQL Injection | WAF |
| DDoS | Shield |
| Threat Detection | GuardDuty |
| Vulnerability | Inspector |
| PII in S3 | Macie |
| API History | CloudTrail |
| Network ACCEPT/REJECT | VPC Flow Logs |
| Data Loss | RPO |
| Downtime | RTO |
| Core Running | Pilot Light |
| Small Full Stack | Warm Standby |
| Full DR Stack | Multi-Site |

---

# Final Exam Rapid-Fire

> **FAILOVER**
> → MULTI-AZ
>
> **READ SCALE**
> → READ REPLICA
>
> **BUFFER**
> → SQS
>
> **BROADCAST**
> → SNS
>
> **ROUTE EVENTS**
> → EVENTBRIDGE
>
> **ORCHESTRATE**
> → STEP FUNCTIONS
>
> **GLOBAL CACHE**
> → CLOUDFRONT
>
> **DATABASE CACHE**
> → ELASTICACHE
>
> **DYNAMODB CACHE**
> → DAX
>
> **PRIVATE S3**
> → GATEWAY ENDPOINT
>
> **TWO VPCs**
> → PEERING
>
> **MANY VPCs**
> → TRANSIT GATEWAY
>
> **ONE SERVICE**
> → PRIVATELINK
>
> **QUICK HYBRID**
> → VPN
>
> **DEDICATED HYBRID**
> → DIRECT CONNECT
>
> **REMOTE USER**
> → CLIENT VPN
>
> **THREAT**
> → GUARDDUTY
>
> **CVE**
> → INSPECTOR
>
> **PII**
> → MACIE
>
> **API AUDIT**
> → CLOUDTRAIL
>
> **NETWORK FLOW**
> → VPC FLOW LOGS
>
> **RPO**
> → DATA LOSS
>
> **RTO**
> → DOWNTIME

---

## Master Memory Trick

> [!tip] Scenario Recognition Master Memory Trick
> On exam day, do not try to remember:
>
> **EVERY AWS FACT AT ONCE**
>
> Instead, train your brain to react to:
>
> **CLUE WORDS**
>
> **READS**
> → Read Replica / Cache
>
> **BURST**
> → SQS
>
> **GLOBAL**
> → CloudFront / Global Architecture
>
> **PRIVATE**
> → Endpoint / PrivateLink / Private Subnet
>
> **FAILURE**
> → HA / DR
>
> **MINIMAL OPERATIONS**
> → Managed / Serverless
>
> **LOWEST COST**
> → Meet requirement without overbuilding
>
> **DATA LOSS**
> → RPO
>
> **DOWNTIME**
> → RTO

Then ask:

> **What pattern does this scenario belong to?**

Once you recognize the pattern:

**Most answer choices become much easier to eliminate.**

---

## Related Notes

- [[SAA Exam Strategy]]
- [[SAA Exam Traps]]
- [[18-Architecture Cheat Sheet]]
- [[High Availability Architecture]]
- [[Scalable Architecture]]
- [[Decoupled Architecture]]
- [[Caching Architecture]]
- [[Secure Architecture]]
- [[Serverless Architecture]]
- [[Disaster Recovery Overview]]