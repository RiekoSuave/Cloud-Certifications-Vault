## Core Exam Rule

For every question:

1. Find the requirement
2. Identify the bottleneck or failure
3. Eliminate impossible AWS behavior
4. Match the optimization word
5. Choose the simplest correct architecture

> [!tip] Memory Trick
> **Requirement → Pattern → Service**

---

# Availability

Need:

**Survive EC2 failure**

→ Auto Scaling

Need:

**Survive AZ failure**

→ Multi-AZ

Need:

**Survive Region failure**

→ Multi-Region

Need:

**Relational DB failover**

→ RDS Multi-AZ

Need:

**More relational reads**

→ Read Replica

### Killer Shortcut

> **FAILOVER**
> → MULTI-AZ
>
> **READS**
> → READ REPLICA

---

# Scaling

Need:

**Bigger machine**

→ Vertical Scaling

Need:

**More machines**

→ Horizontal Scaling

Need:

**Automatic EC2 capacity**

→ Auto Scaling

Need:

**Distribute requests**

→ Load Balancer

Need:

**Known traffic spike**

→ Scheduled Scaling

Need:

**Forecast recurring demand**

→ Predictive Scaling

Need:

**Keep metric near target**

→ Target Tracking

---

# Stateless Architecture

Need:

**Replaceable app servers**

→ Stateless compute

Need:

**Fast shared sessions**

→ ElastiCache

Need:

**Durable shared key-value state**

→ DynamoDB

Need:

**User uploads**

→ S3

Need:

**Shared mounted Linux files**

→ EFS

### Memory Trick

> **COMPUTE CAN DIE**
>
> **STATE MUST SURVIVE**

---

# Decoupling

Need:

**Buffer work**

→ SQS

Need:

**One event to many**

→ SNS

Need:

**Fan-out + durable buffering**

→ SNS + SQS

Need:

**Route events**

→ EventBridge

Need:

**Orchestrate workflow**

→ Step Functions

### Memory Trick

> **SQS = HOLD**
>
> **SNS = BROADCAST**
>
> **EVENTBRIDGE = ROUTE**
>
> **STEP FUNCTIONS = ORCHESTRATE**

---

# SQS

Need:

**Strict ordering**

→ FIFO

Need:

**Repeated duplicate delivery safety**

→ Idempotent Consumer

Need:

**Long processing time**

→ Increase Visibility Timeout

Need:

**Repeated failures**

→ DLQ

Need:

**Reduce empty receives**

→ Long Polling

Need:

**Delay message processing**

→ Delay Queue

---

# Caching

Need:

**Global content cache**

→ CloudFront

Need:

**Application/database cache**

→ ElastiCache

Need:

**DynamoDB cache**

→ DAX

Need:

**API response cache**

→ API Gateway Cache

Need:

**More relational read capacity**

→ Read Replica

### Killer Shortcut

> **SAME READ REPEATEDLY**
> → CACHE
>
> **MANY DIFFERENT READS**
> → READ REPLICA

---

# Storage

Need:

**Object storage**

→ S3

Need:

**EC2 block storage**

→ EBS

Need:

**Shared Linux filesystem**

→ EFS

Need:

**Windows managed file share**

→ FSx for Windows File Server

Need:

**Lustre / HPC filesystem**

→ FSx for Lustre

---

# S3

Need:

**Unknown access pattern**

→ Intelligent-Tiering

Need:

**Automatic archival over time**

→ Lifecycle Policy

Need:

**Long-term archive**

→ Glacier class

Need:

**Recover overwrite/delete**

→ Versioning

Need:

**Immutable object retention**

→ Object Lock

Need:

**Cross-Region copy**

→ Cross-Region Replication

---

# EBS

Need:

**Point-in-time volume backup**

→ Snapshot

Need:

**Regional DR copy**

→ Cross-Region Snapshot Copy

Need:

**General-purpose SSD**

→ gp3

---

# Databases

Need:

**Relational SQL**

→ RDS / Aurora

Need:

**AWS-optimized relational**

→ Aurora

Need:

**Massive NoSQL**

→ DynamoDB

Need:

**In-memory cache**

→ ElastiCache

Need:

**Data warehouse**

→ Redshift

---

# RDS

Need:

**High Availability**

→ Multi-AZ

Need:

**Read Scaling**

→ Read Replica

Need:

**Point-in-Time Recovery**

→ Automated Backups

### Memory Trick

> **MULTI-AZ = SURVIVE**
>
> **READ REPLICA = READ**

---

# Aurora

Need:

**Aurora Multi-Region**

→ Aurora Global Database

Need:

**Aurora variable capacity**

→ Aurora Serverless

Need:

**Read scaling**

→ Aurora Replicas

---

# DynamoDB

Need:

**Unpredictable traffic**

→ On-Demand

Need:

**Predictable traffic**

→ Provisioned Capacity

Need:

**Multi-Region writes**

→ Global Tables

Need:

**React to item changes**

→ Streams

Need:

**Very fast repeated reads**

→ DAX

---

# Analytics

Need:

**SQL against S3**

→ Athena

Need:

**ETL / Data Catalog**

→ Glue

Need:

**Big-data processing**

→ EMR

Need:

**Search / log analytics**

→ OpenSearch

Need:

**Streaming data**

→ Kinesis

Need:

**Analytics warehouse**

→ Redshift

---

# Public and Private Networking

Need:

**Public Internet connectivity**

→ Internet Gateway

Need:

**Private subnet outbound IPv4 Internet**

→ NAT Gateway

Need:

**Private S3/DynamoDB**

→ Gateway Endpoint

Need:

**Private supported AWS service**

→ Interface Endpoint

---

# VPC Connectivity

Need:

**Two VPCs**

→ VPC Peering

Need:

**Many VPCs + transitive routing**

→ Transit Gateway

Need:

**One private service**

→ PrivateLink

### Memory Trick

> **PEERING = TWO**
>
> **TGW = MANY**
>
> **PRIVATELINK = SERVICE**

---

# VPC Endpoint

Gateway Endpoint:

- S3
- DynamoDB
- Route table

Interface Endpoint:

- ENI
- Security Group
- PrivateLink

### Killer Shortcut

> **S3 / DYNAMODB**
> → GATEWAY
>
> **MOST OTHER SUPPORTED SERVICES**
> → INTERFACE

---

# Hybrid Networking

Need:

**Quick encrypted on-prem connectivity**

→ Site-to-Site VPN

Need:

**Dedicated predictable connectivity**

→ Direct Connect

Need:

**Remote employee**

→ Client VPN

Need:

**On-prem to many VPCs**

→ VPN / DX + Transit Gateway

Need:

**Hybrid DNS**

→ Route 53 Resolver

---

# Route 53 Resolver

On-Prem  
→ AWS DNS

→ Inbound Endpoint

AWS  
→ On-Prem DNS

→ Outbound Endpoint

Need:

**Specific domain forwarding**

→ Resolver Rule

---

# Security Groups vs NACL

Security Group:

- Stateful
- Resource-level
- Allow only

NACL:

- Stateless
- Subnet-level
- Allow + deny
- Ordered rules

### Killer Shortcut

> **EXPLICIT DENY**
> → NACL

---

# IAM

Need:

**AWS permissions**

→ IAM

Need:

**Workload AWS access without keys**

→ IAM Role

Need:

**Workforce access across accounts**

→ IAM Identity Center

Need:

**Organization guardrail**

→ SCP

Need:

**Temporary credentials**

→ STS

---

# Encryption and Secrets

Need:

**Managed encryption keys**

→ KMS

Need:

**Dedicated HSM**

→ CloudHSM

Need:

**Secrets + rotation**

→ Secrets Manager

Need:

**Managed TLS certificate**

→ ACM

---

# Security Services

Need:

**SQL Injection / XSS**

→ WAF

Need:

**DDoS**

→ Shield

Need:

**VPC traffic inspection**

→ Network Firewall

Need:

**Threat Detection**

→ GuardDuty

Need:

**CVE / Vulnerability**

→ Inspector

Need:

**PII in S3**

→ Macie

Need:

**Central findings**

→ Security Hub

Need:

**Configuration compliance**

→ Config

---

# Logging

Need:

**Who called AWS API?**

→ CloudTrail

Need:

**Metrics / Logs / Alarms**

→ CloudWatch

Need:

**Network ACCEPT / REJECT**

→ VPC Flow Logs

Need:

**DNS query history**

→ Route 53 Resolver Query Logging

### Memory Trick

> **TRAIL = WHO**
>
> **WATCH = HOW**
>
> **FLOW LOGS = NETWORK**

---

# Serverless

Need:

**Event-driven compute**

→ Lambda

Need:

**Managed API**

→ API Gateway

Need:

**Serverless NoSQL**

→ DynamoDB

Need:

**Authentication**

→ Cognito

Need:

**Workflow**

→ Step Functions

Need:

**Async processing**

→ SQS + Lambda

---

# Containers

Need:

**AWS-native container orchestration**

→ ECS

Need:

**Kubernetes**

→ EKS

Need:

**Containers without managing servers**

→ Fargate

---

# Cost Optimization

Need:

**Underutilized EC2**

→ Right-size

Need:

**Variable EC2 demand**

→ Auto Scaling

Need:

**Unpredictable compute**

→ On-Demand

Need:

**Steady compute**

→ Savings Plans / Reserved pricing

Need:

**Interruptible workload**

→ Spot

Need:

**Old S3 data**

→ Lifecycle Policy

Need:

**Unknown S3 access**

→ Intelligent-Tiering

Need:

**High NAT cost to S3**

→ Gateway Endpoint

---

# Disaster Recovery

Need:

**Acceptable data loss**

→ RPO

Need:

**Acceptable downtime**

→ RTO

### Memory Trick

> **RPO = DATA**
>
> **RTO = TIME**

---

# DR Strategies

Backups only  
→ Backup and Restore

Core running  
→ Pilot Light

Full stack running small  
→ Warm Standby

Full stack running full  
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

# Elastic Disaster Recovery

Need:

**Continuous server replication**

→ Elastic Disaster Recovery

Need:

**Block-level replication**

→ Elastic Disaster Recovery

Need:

**AWS as DR site for on-prem servers**

→ Elastic Disaster Recovery

---

# Route 53 Routing Recognition

Need:

**Primary / Secondary**

→ Failover

Need:

**Lowest latency**

→ Latency-Based

Need:

**Percentage split**

→ Weighted

Need:

**User location**

→ Geolocation

Need:

**Resource geography + bias**

→ Geoproximity

Need:

**Multiple healthy responses**

→ Multi-Value Answer

---

# Global Services Recognition

Need:

**Global cached content**

→ CloudFront

Need:

**Static anycast IPs + fast endpoint failover**

→ Global Accelerator

Need:

**Global DynamoDB writes**

→ Global Tables

Need:

**Global Aurora**

→ Aurora Global Database

---

# Operational Overhead

If the question says:

**Least operational overhead**

strongly consider:

- Managed services
- Serverless
- AWS-native HA
- Automatic scaling

Avoid unnecessary:

- Custom EC2 clusters
- Self-managed databases
- Manual failover

---

# Architecture Tie-Breaker

If two answers both work:

Ask which better matches:

**The optimization phrase**

Examples:

Most cost-effective  
→ Lower total cost

Least operational overhead  
→ More managed

Most resilient  
→ Better failure isolation

Lowest latency  
→ Shorter/faster path

Most secure  
→ Least privilege + defense in depth

---

# Fast Elimination Rules

> **READ SCALING**
> → NOT MULTI-AZ
>
> **EXPLICIT DENY**
> → NOT SECURITY GROUP
>
> **TRANSITIVE VPC ROUTING**
> → NOT PEERING
>
> **REMOTE USER**
> → NOT SITE-TO-SITE VPN
>
> **PRIVATE S3**
> → NAT MAY BE UNNECESSARY
>
> **SQL INJECTION**
> → WAF
>
> **CVE**
> → INSPECTOR
>
> **API AUDIT**
> → CLOUDTRAIL
>
> **CORE RUNNING**
> → PILOT LIGHT
>
> **FULL STACK SMALL**
> → WARM STANDBY

---

# Top Service Pairs to Memorize

| Pair | Difference |
|---|---|
| Multi-AZ vs Read Replica | HA vs Read Scaling |
| SQS vs SNS | Queue vs Broadcast |
| EventBridge vs Step Functions | Route vs Orchestrate |
| CloudFront vs Global Accelerator | Cache vs Network Acceleration |
| SG vs NACL | Stateful Resource vs Stateless Subnet |
| Peering vs TGW | Two VPCs vs Many VPCs |
| Peering vs PrivateLink | Network vs Service |
| VPN vs Direct Connect | Quick Encrypted vs Dedicated Predictable |
| CloudWatch vs CloudTrail | Monitoring vs API Audit |
| GuardDuty vs Inspector | Threat vs Vulnerability |
| KMS vs Secrets Manager | Key vs Secret |
| Pilot Light vs Warm Standby | Core vs Full Stack Small |
| RPO vs RTO | Data Loss vs Downtime |

---

# Top Exam Traps

## Trap 1

Multi-AZ for read scaling

❌

→ Read Replica

---

## Trap 2

Security Group deny

❌

→ NACL

---

## Trap 3

Peering transitive routing

❌

→ Transit Gateway

---

## Trap 4

Direct Connect encrypted by default

❌

Private does not automatically mean:

**Encrypted**

---

## Trap 5

CloudTrail for network traffic

❌

→ VPC Flow Logs

---

## Trap 6

GuardDuty for CVEs

❌

→ Inspector

---

## Trap 7

WAF for all network inspection

❌

→ Network Firewall where advanced VPC inspection is required

---

## Trap 8

Backup frequency = RTO

❌

Backup frequency primarily affects:

**RPO**

---

## Trap 9

Warm Standby = Pilot Light

❌

Pilot:

**Core only**

Warm:

**Full stack small**

---

## Trap 10

Most complex answer wins

❌

Choose:

**Simplest answer meeting every requirement**

---

# Final 60-Second Review

> **ALB**
> → DISTRIBUTE
>
> **AUTO SCALING**
> → ADJUST CAPACITY
>
> **MULTI-AZ**
> → SURVIVE AZ
>
> **READ REPLICA**
> → SCALE READS
>
> **SQS**
> → BUFFER
>
> **SNS**
> → FAN-OUT
>
> **EVENTBRIDGE**
> → ROUTE EVENTS
>
> **STEP FUNCTIONS**
> → WORKFLOW
>
> **CLOUDFRONT**
> → EDGE CACHE
>
> **ELASTICACHE**
> → APP/DB CACHE
>
> **S3**
> → OBJECT
>
> **EBS**
> → BLOCK
>
> **EFS**
> → SHARED FILE
>
> **RDS/AURORA**
> → RELATIONAL
>
> **DYNAMODB**
> → NOSQL
>
> **NAT**
> → PRIVATE TO INTERNET
>
> **VPC ENDPOINT**
> → PRIVATE AWS SERVICE
>
> **PEERING**
> → TWO VPCs
>
> **TGW**
> → MANY VPCs
>
> **PRIVATELINK**
> → ONE SERVICE
>
> **VPN**
> → QUICK HYBRID
>
> **DIRECT CONNECT**
> → DEDICATED HYBRID
>
> **IAM**
> → PERMISSIONS
>
> **KMS**
> → KEYS
>
> **SECRETS MANAGER**
> → SECRETS
>
> **WAF**
> → WEB ATTACKS
>
> **SHIELD**
> → DDoS
>
> **GUARDDUTY**
> → THREATS
>
> **INSPECTOR**
> → VULNERABILITIES
>
> **CLOUDTRAIL**
> → WHO DID IT
>
> **CLOUDWATCH**
> → HOW IT'S RUNNING
>
> **RPO**
> → DATA LOSS
>
> **RTO**
> → DOWNTIME

---

## Master Memory Trick

> [!tip] Final Review Master Memory Trick
> When the exam gives you a long scenario, ask:
>
> **WHAT IS THE PROBLEM?**
>
> Too much traffic?
>
> → SCALE
>
> Backend overloaded?
>
> → DECOUPLE
>
> Same data repeated?
>
> → CACHE
>
> Component can fail everything?
>
> → ADD REDUNDANCY
>
> Too much management?
>
> → MANAGED / SERVERLESS
>
> Too expensive?
>
> → RIGHT-SIZE / ELASTICITY
>
> Needs private access?
>
> → PRIVATE NETWORKING OPTION
>
> Security problem?
>
> → IDENTITY / NETWORK / DATA / DETECTION
>
> Disaster?
>
> → RPO + RTO

Then remember:

> **REQUIREMENT FIRST**
>
> **ELIMINATE IMPOSSIBLE ANSWERS**
>
> **MATCH THE OPTIMIZATION WORD**
>
> **CHOOSE THE SIMPLEST CORRECT DESIGN**

That is the core SAA exam strategy.

---

## Related Notes

- [[SAA Exam Strategy]]
- [[SAA Exam Traps]]
- [[SAA Scenario Recognition Cheat Sheet]]
- [[18-Architecture Cheat Sheet]]
- [[Disaster Recovery Overview]]