## Core Concept

Many SAA questions are designed so:

**Several answers sound reasonable**

but one option contains:

**A subtle architectural flaw**

The exam often tests whether you can identify:

- Wrong service purpose
- Missing requirement
- Incorrect AWS behavior
- Unnecessary complexity
- Wrong failure domain
- Wrong cost tradeoff
- Wrong networking assumption

> [!tip] Memory Trick
> **SAA Traps = One Small Detail Makes the Answer Wrong**

---

# Trap 1 — RDS Multi-AZ vs Read Replica

This is one of the most common traps.

## Multi-AZ

Think:

**High Availability**

Use for:

- Automatic failover
- AZ failure
- Database resilience

## Read Replica

Think:

**Read Scaling**

Use for:

- Reporting
- Read-heavy workload
- Offloading SELECT queries

### Killer Shortcut

> **SURVIVE**
> → Multi-AZ
>
> **READ**
> → Read Replica

---

# Trap 2 — Read Replica Is Automatic Failover

❌

A standard Read Replica is primarily for:

**Read scaling**

It should not automatically be treated as:

**The same thing as Multi-AZ standby failover**

### Exam Rule

> **Read Replica = Scaling First**
>
> **Multi-AZ = Availability First**

---

# Trap 3 — Multi-AZ Protects Against Region Failure

❌

Multi-AZ protects within:

**One AWS Region**

If the requirement says:

**Complete Region failure**

think:

**Multi-Region**

---

# Trap 4 — One Large EC2 Instance Is Highly Available

❌

A huge instance is still:

**One instance**

If it fails:

**The workload fails**

Better architecture:

Load Balancer  
↓  
Auto Scaling  
↓  
Multiple AZs

---

# Trap 5 — Multiple EC2 Instances in One AZ = Multi-AZ

❌

More instances improve:

**Instance resilience**

but if they are all inside:

**One AZ**

they still share:

**The same AZ failure domain**

### Killer Exam Principle

> **Redundancy must cross the failure domain you are protecting against**

---

# Trap 6 — Auto Scaling = Load Balancing

❌

They solve different problems.

## Auto Scaling

**Adds / removes / replaces capacity**

## Load Balancer

**Distributes traffic**

### Memory Trick

> **ASG = CAPACITY**
>
> **ELB = TRAFFIC**

---

# Trap 7 — Load Balancer Automatically Creates EC2 Instances

❌

The load balancer:

**Routes traffic**

It does not:

**Scale the fleet**

Think:

**Auto Scaling**

---

# Trap 8 — Stateful App + Auto Scaling Is Automatically Fine

❌

If sessions live on:

**Local EC2 instances**

terminating instances can cause:

**Session loss**

Better:

**Externalize state**

---

# Trap 9 — Sticky Sessions = Stateless

❌

Sticky sessions keep users tied to:

**One backend**

That is still:

**Stateful coupling**

A more scalable design may store sessions in:

- ElastiCache
- DynamoDB

---

# Trap 10 — S3 Is a File System

❌

S3 is:

**Object storage**

If the requirement says:

**Mounted shared filesystem**

think:

**EFS or FSx**

---

# Trap 11 — EBS Is Shared Multi-Instance File Storage

Usually wrong for the classic exam pattern.

Think:

**EBS = Block storage attached to EC2**

Need:

**Shared Linux filesystem**

→ EFS

---

# Trap 12 — EFS Is Object Storage

❌

EFS provides:

**Managed shared file storage**

S3 provides:

**Object storage**

---

# Trap 13 — SQS Sends One Message to Every Consumer

❌

SQS is primarily:

**A queue**

Consumers compete for:

**Messages**

Need one event copied to many consumers?

→ **SNS**

---

# Trap 14 — SNS Is Durable Work Buffering

SNS is primarily:

**Publish/Subscribe fan-out**

If consumers may be temporarily unavailable and must process later:

Use:

**SNS + SQS**

### Memory Trick

> **SNS COPIES**
>
> **SQS HOLDS**

---

# Trap 15 — EventBridge = SQS

❌

## EventBridge

**Routes events**

## SQS

**Stores work until processed**

### Killer Shortcut

**ROUTE**
→ EventBridge

**WAIT**
→ SQS

---

# Trap 16 — Step Functions = EventBridge

❌

## Step Functions

**Orchestrates workflow steps**

## EventBridge

**Routes events**

### Memory Trick

> **EventBridge = WHERE**
>
> **Step Functions = WHAT NEXT**

---

# Trap 17 — SQS Receive Deletes Message

❌

When a consumer receives a message:

It becomes:

**Temporarily invisible**

The consumer must delete it after:

**Successful processing**

---

# Trap 18 — Visibility Timeout = Retention Period

❌

Visibility Timeout:

**How long a received message is hidden**

Retention Period:

**How long SQS keeps the message overall**

---

# Trap 19 — Standard SQS Guarantees Exactly-Once Delivery

❌

Standard queues provide:

**At-least-once delivery**

Therefore consumers should be:

**Idempotent**

---

# Trap 20 — Standard SQS Guarantees Strict Order

❌

Need strict ordering?

→ **FIFO**

---

# Trap 21 — FIFO Is Always Better

❌

FIFO provides:

**Stronger ordering guarantees**

but Standard queues may be better when:

**Strict ordering is unnecessary and very high throughput is desired**

### Exam Principle

> **Do not pay architectural complexity for a requirement that does not exist**

---

# Trap 22 — DLQ Processes Failed Messages

❌

A DLQ:

**Stores repeatedly failing messages**

You still need:

**A process to inspect or redrive them**

---

# Trap 23 — CloudFront = Global Accelerator

❌

## CloudFront

Think:

**Content delivery + caching**

## Global Accelerator

Think:

**Network acceleration + static anycast IPs**

### Killer Shortcut

**CACHE CONTENT**
→ CloudFront

**STATIC GLOBAL IP + FAST FAILOVER**
→ Global Accelerator

---

# Trap 24 — CloudFront Only Works With S3

❌

CloudFront can use origins such as:

- S3
- ALB
- EC2-backed applications
- Other HTTP origins

---

# Trap 25 — ElastiCache = Read Replica

❌

## ElastiCache

May avoid:

**Database queries entirely**

## Read Replica

Still processes:

**Database reads**

### Killer Shortcut

Repeated same data  
→ Cache

More varied reads  
→ Read Replica

---

# Trap 26 — DAX Is a General Database Cache

❌

DAX is designed for:

**DynamoDB**

Need cache for RDS/application data?

→ **ElastiCache**

---

# Trap 27 — Cache Is the Source of Truth

Usually wrong.

The cache normally stores:

**Temporary copies**

The durable database/object store remains:

**The authoritative source**

### Memory Trick

> **CACHE = COPY**
>
> **DATABASE = TRUTH**

---

# Trap 28 — Long TTL Is Always Better

❌

Long TTL improves:

**Cache efficiency**

but increases risk of:

**Stale data**

---

# Trap 29 — Security Group Can Deny Traffic

❌

Security Groups use:

**Allow rules**

Need explicit deny?

→ **NACL**

---

# Trap 30 — NACL Is Stateful

❌

NACL is:

**Stateless**

Return traffic must be:

**Explicitly permitted**

---

# Trap 31 — NACL Highest Rule Number Wins

❌

Rules are evaluated from:

**Lower number to higher number**

The:

**First matching rule wins**

### Memory Trick

**Lowest Match Wins**

---

# Trap 32 — Security Group Rule Order Matters

❌

Security Group rules are not processed like:

**Ordered firewall rules**

Permissions are evaluated as:

**A combined set**

---

# Trap 33 — Private Subnet Automatically Means No Internet

Not necessarily.

A private subnet can have outbound Internet access through:

**NAT Gateway**

### Memory Trick

**Private = No Direct IGW Route**

Not:

**No Internet Ever**

---

# Trap 34 — NAT Gateway Belongs in a Private Subnet

For public Internet egress:

❌

A public NAT Gateway belongs in:

**A public subnet**

with a route to:

**Internet Gateway**

Private subnets route to:

**The NAT Gateway**

---

# Trap 35 — NAT Gateway Accepts Unsolicited Inbound Internet Connections

❌

Its common purpose is:

**Outbound IPv4 Internet access for private resources**

---

# Trap 36 — One NAT Gateway Is Ideal Multi-AZ HA

Not necessarily.

For stronger AZ independence:

**Use a NAT Gateway per AZ**

where requirements justify it.

---

# Trap 37 — Internet Gateway Needs One Per AZ

❌

Internet Gateway is:

**VPC-level AWS-managed infrastructure**

You do not create:

**One per AZ**

---

# Trap 38 — VPC Peering Is Transitive

❌

A ↔ B  
B ↔ C

does NOT imply:

A ↔ C

Need transitive routing?

→ **Transit Gateway**

---

# Trap 39 — Peering Works With Overlapping CIDRs

❌

Standard VPC Peering requires:

**Non-overlapping CIDRs**

---

# Trap 40 — Peering Automatically Updates Route Tables

❌

You must configure:

**Routes**

on the relevant sides.

---

# Trap 41 — Transit Gateway = PrivateLink

❌

## Transit Gateway

Connects:

**Networks**

## PrivateLink

Exposes:

**Specific services**

### Memory Trick

> **TGW = NETWORK HUB**
>
> **PRIVATELINK = SERVICE DOOR**

---

# Trap 42 — PrivateLink Gives Full VPC Access

❌

PrivateLink is designed for:

**Specific service connectivity**

not broad routed network access.

---

# Trap 43 — Every VPC Endpoint Uses an ENI

❌

## Interface Endpoint

Uses:

**ENIs**

## Gateway Endpoint

Uses:

**Route tables**

---

# Trap 44 — S3 Private Access Always Needs NAT Gateway

❌

Think:

**S3 Gateway Endpoint**

when appropriate.

---

# Trap 45 — Gateway Endpoint = Interface Endpoint

❌

Gateway Endpoint:

- S3
- DynamoDB
- Route table

Interface Endpoint:

- ENI
- Security Group
- PrivateLink

---

# Trap 46 — VPC Endpoint Provides General Internet Access

❌

VPC Endpoints provide:

**Private access to specific supported services**

Need general Internet?

→ **NAT Gateway**

---

# Trap 47 — Site-to-Site VPN = Client VPN

❌

## Site-to-Site VPN

**Network-to-network**

## Client VPN

**User/device-to-network**

### Memory Trick

> **SITE = NETWORK**
>
> **CLIENT = USER**

---

# Trap 48 — VPN = Dedicated Circuit

❌

Site-to-Site VPN normally uses:

**The public Internet**

with:

**IPsec encryption**

Need dedicated connection?

→ **Direct Connect**

---

# Trap 49 — Direct Connect Is Encrypted by Default

❌

Direct Connect provides:

**Dedicated/private connectivity**

but private does not automatically mean:

**Encrypted**

---

# Trap 50 — Direct Connect Is the Fastest to Provision

❌

Physical provisioning can take:

**Longer**

Need connectivity quickly?

→ **Site-to-Site VPN**

---

# Trap 51 — Direct Connect Replaces VPN in Every Case

❌

VPN may still be useful for:

- Backup
- Rapid deployment
- IPsec encryption

---

# Trap 52 — Direct Connect Solves Hybrid DNS

❌

Direct Connect provides:

**Network connectivity**

Need hybrid DNS?

→ **Route 53 Resolver**

---

# Trap 53 — Route 53 Resolver Inbound Means AWS to On-Prem

❌

Inbound means:

**Queries come INTO AWS**

On-Prem  
→ AWS

---

# Trap 54 — Route 53 Resolver Outbound Means On-Prem to AWS

❌

Outbound means:

**Queries leave AWS**

AWS  
→ On-Prem

---

# Trap 55 — CloudTrail = CloudWatch

❌

## CloudTrail

**AWS API activity**

## CloudWatch

**Metrics, logs, alarms**

### Memory Trick

> **TRAIL = WHO DID IT**
>
> **WATCH = HOW IS IT RUNNING**

---

# Trap 56 — VPC Flow Logs = Packet Capture

❌

Flow Logs contain:

**Traffic metadata**

not:

**Full packet payloads**

---

# Trap 57 — VPC Flow Logs Block Traffic

❌

They:

**Record**

Security controls:

**Allow or block**

---

# Trap 58 — GuardDuty = Inspector

❌

## GuardDuty

**Threat detection**

## Inspector

**Vulnerability management**

### Killer Shortcut

Suspicious behavior  
→ GuardDuty

Known CVE  
→ Inspector

---

# Trap 59 — Inspector Installs Patches

❌

Inspector:

**Finds vulnerabilities**

Systems Manager Patch Manager:

**Applies patches**

---

# Trap 60 — Macie Scans EC2 for Vulnerabilities

❌

Macie focuses on:

**Sensitive data discovery in S3**

---

# Trap 61 — Security Hub Detects Every Threat Itself

❌

Security Hub primarily:

**Aggregates and organizes security findings**

from supported sources.

---

# Trap 62 — WAF = Shield

❌

## WAF

Think:

**Web request attacks**

Examples:

- SQL injection
- XSS

## Shield

Think:

**DDoS**

---

# Trap 63 — WAF Protects All Network Traffic

❌

WAF focuses on:

**HTTP(S) application-layer traffic**

Need advanced VPC inspection?

→ **Network Firewall**

---

# Trap 64 — KMS Stores Passwords

❌

KMS manages:

**Encryption keys**

Need application secrets?

→ **Secrets Manager**

---

# Trap 65 — Secrets Manager = Parameter Store

They overlap in some use cases but are not identical.

Need:

**Secret rotation**

→ Secrets Manager

Need:

**Configuration parameter**

→ Parameter Store may be appropriate

---

# Trap 66 — Hardcoded AWS Keys Are Fine if Instance Is Private

❌

Use:

**IAM Roles**

---

# Trap 67 — SCP Grants Permissions

❌

SCPs establish:

**Permission guardrails**

They do not directly grant:

**Access**

IAM still must allow the action.

---

# Trap 68 — Root User Should Be Used for Daily Administration

❌

Use:

**IAM identities / federation**

Root should be:

**Rarely used**

and protected with:

**MFA**

---

# Trap 69 — Serverless Means No Servers Exist

❌

Servers exist.

AWS:

**Manages them**

---

# Trap 70 — Lambda Is Good for Every Application

❌

Lambda may be a poor fit for:

- Long-running processes
- Certain specialized runtimes
- Workloads requiring deep OS control

---

# Trap 71 — Lambda Local Storage Is Permanent

❌

Treat Lambda compute as:

**Ephemeral/stateless**

Store important state in:

**Durable external services**

---

# Trap 72 — Lambda Automatically Has AWS Permissions

❌

Lambda needs:

**An execution role**

with appropriate permissions.

---

# Trap 73 — Serverless Is Always Cheapest

❌

Usage pattern matters.

Constant heavy workloads may sometimes favor:

**Other architectures**

---

# Trap 74 — DynamoDB Is Always Best Because It Scales

❌

If the workload requires:

- Relational joins
- SQL relationships
- Relational transactions

then:

**RDS / Aurora**

may be a better fit.

---

# Trap 75 — RDS Is Always Better Than DynamoDB

❌

If the workload needs:

- Key-value access
- Massive scale
- Serverless operation
- Predictable low latency

think:

**DynamoDB**

---

# Trap 76 — DynamoDB On-Demand Is Always Cheapest

❌

For:

**Predictable steady workloads**

Provisioned capacity may be:

**More cost-effective**

---

# Trap 77 — Spot Is Safe for Any Production Workload

❌

Spot can be:

**Interrupted**

Use for workloads that can:

**Tolerate interruption**

---

# Trap 78 — Reserved Pricing Is Best for Unpredictable Short-Term Workloads

❌

Commitment pricing fits:

**Steady predictable usage**

Need flexibility?

→ **On-Demand**

---

# Trap 79 — S3 Glacier Is Always Best for Backups

❌

Archive retrieval times must satisfy:

**RTO / access requirements**

---

# Trap 80 — S3 Intelligent-Tiering Is Always Required

❌

Use it when:

**Access patterns are unknown or changing**

If the access pattern is known:

A specific storage class may be:

**More appropriate**

---

# Trap 81 — Lifecycle Policy = Intelligent-Tiering

❌

## Lifecycle Policy

Moves objects according to:

**Rules and age**

## Intelligent-Tiering

Automatically changes access tiers based on:

**Observed access patterns**

---

# Trap 82 — Backup Frequency Determines RTO

❌

Backup frequency primarily affects:

**RPO**

Restore/recovery speed primarily affects:

**RTO**

### Memory Trick

> **RPO = DATA**
>
> **RTO = TIME**

---

# Trap 83 — Pilot Light = Warm Standby

❌

## Pilot Light

**Core only**

## Warm Standby

**Full stack running small**

---

# Trap 84 — Warm Standby = Multi-Site

❌

Warm Standby:

**Scale after disaster**

Multi-Site:

**Already production-capable**

---

# Trap 85 — Backup and Restore Is Fastest DR Strategy

❌

It generally has:

**The longest recovery time**

---

# Trap 86 — Multi-Site Is Always Best

❌

It can provide:

**Very fast recovery**

but has:

**High ongoing cost and complexity**

Choose it only when:

**RPO/RTO justify it**

---

# Trap 87 — Backup = Replication

❌

Backup preserves:

**Recovery points**

Replication copies:

**Changes**

They solve related but different problems.

---

# Trap 88 — Backup Exists, Therefore Recovery Is Guaranteed

❌

Backups must be:

**Tested and restorable**

---

# Trap 89 — Multi-Region Replaces Multi-AZ

❌

A robust Multi-Region architecture may still need:

**Multi-AZ within each Region**

---

# Trap 90 — Most Complex Architecture Wins

❌

This may be the biggest exam trap of all.

The best answer is often:

**The simplest architecture that satisfies every requirement**

### Killer Exam Principle

> **More services does not automatically mean better architecture**

---

# Trap 91 — Cheapest Answer Always Wins

❌

The cheapest answer must still satisfy:

- Availability
- Performance
- Security
- RPO/RTO
- Operational requirements

### Memory Trick

**Requirement First**

**Cost Second**

---

# Trap 92 — Most Secure-Looking Answer Always Wins

❌

Security must fit:

**The actual threat and requirement**

Example:

Need:

**SQL injection protection**

Network Firewall may sound powerful.

But the targeted answer is likely:

**WAF**

---

# Trap 93 — Managed Service Is Always Required

❌

Managed services are great for:

**Lower operational overhead**

But if the scenario requires:

**Deep customization or OS control**

EC2 or containers may be more appropriate.

---

# Trap 94 — Every Correct Answer Uses One Service

❌

Many architecture answers require:

**A combination**

Example:

Highly available scalable application:

ALB  
+  
Auto Scaling  
+  
Multiple AZs

---

# Trap 95 — Ignore the Words "Without Modifying the Application"

❌

This phrase can eliminate solutions requiring:

**Code changes**

Look for:

**Infrastructure-level solutions**

---

# Trap 96 — Ignore the Words "Without Downtime"

❌

This can eliminate:

- Manual rebuild approaches
- Slow migrations
- Some disruptive maintenance strategies

### Exam Principle

> **Every constraint matters**

---

# Trap 97 — Ignore "Least Operational Overhead"

❌

If two answers work:

Choose the one requiring:

**Less infrastructure administration**

when this phrase appears.

---

# Trap 98 — Ignore "Most Cost-Effective"

❌

If two answers work:

Choose the one that meets requirements with:

**Lower ongoing cost**

---

# Trap 99 — Ignore "Highly Available"

❌

Single-AZ answers become suspicious immediately.

---

# Trap 100 — Choose Based on Familiar Service Name

❌

This is the ultimate memory trap.

The fact that you recognize a service does not mean:

**It solves the requirement**

### Final Rule

> **Architecture problem first**
>
> **Service name second**

---

# Fast Trap Recognition Table

| If You See | Do NOT Confuse It With |
|---|---|
| RDS Multi-AZ | Read Replica |
| Read Replica | Automatic HA Standby |
| SQS | SNS |
| SNS | Durable Queue |
| EventBridge | SQS |
| Step Functions | EventBridge |
| CloudFront | Global Accelerator |
| ElastiCache | Read Replica |
| DAX | General DB Cache |
| Security Group | NACL |
| NACL | Stateful Firewall |
| VPC Peering | Transit Gateway |
| PrivateLink | VPC Peering |
| VPN | Direct Connect |
| Client VPN | Site-to-Site VPN |
| CloudWatch | CloudTrail |
| GuardDuty | Inspector |
| WAF | Shield |
| KMS | Secrets Manager |
| Pilot Light | Warm Standby |
| Warm Standby | Multi-Site |
| RPO | RTO |

---

# Rapid Elimination Rules

> **READ SCALING**
> → NOT MULTI-AZ
>
> **EXPLICIT DENY**
> → NOT SECURITY GROUP
>
> **TRANSITIVE VPC ROUTING**
> → NOT PEERING
>
> **PRIVATE S3**
> → NAT MAY BE UNNECESSARY
>
> **REMOTE USER**
> → NOT SITE-TO-SITE VPN
>
> **HYBRID NETWORK**
> → NOT CLIENT VPN
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
> **PACKET CONTENT**
> → NOT FLOW LOGS
>
> **CORE RUNNING**
> → PILOT LIGHT
>
> **FULL STACK SMALL**
> → WARM STANDBY

---

# Final Exam Rapid-Fire

> **MULTI-AZ**
> → AVAILABILITY
>
> **READ REPLICA**
> → READ SCALE
>
> **SQS**
> → HOLD
>
> **SNS**
> → FAN-OUT
>
> **EVENTBRIDGE**
> → ROUTE
>
> **STEP FUNCTIONS**
> → ORCHESTRATE
>
> **CLOUDFRONT**
> → CACHE
>
> **GLOBAL ACCELERATOR**
> → NETWORK ACCELERATION
>
> **SG**
> → STATEFUL RESOURCE
>
> **NACL**
> → STATELESS SUBNET
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
> → QUICK ENCRYPTED HYBRID
>
> **DIRECT CONNECT**
> → DEDICATED HYBRID
>
> **CLIENT VPN**
> → REMOTE USER
>
> **CLOUDTRAIL**
> → API ACTIVITY
>
> **CLOUDWATCH**
> → MONITORING
>
> **GUARDDUTY**
> → THREATS
>
> **INSPECTOR**
> → VULNERABILITIES
>
> **RPO**
> → DATA LOSS
>
> **RTO**
> → DOWNTIME

---

## Master Memory Trick

> [!tip] SAA Exam Traps Master Memory Trick
> On the exam, imagine every answer choice is:
>
> **Trying to sell you something**
>
> One answer sounds:
>
> **More powerful**
>
> Another sounds:
>
> **More secure**
>
> Another sounds:
>
> **More complicated**
>
> But only one actually:
>
> **SOLVES THE QUESTION**
>
> Your job is not to find:
>
> **The coolest AWS service**
>
> Your job is to find:
>
> **The answer with no fatal flaw**

So remember:

> **MULTI-AZ**
> → NOT READ SCALE
>
> **READ REPLICA**
> → NOT HA FIRST
>
> **SQS**
> → NOT BROADCAST
>
> **SNS**
> → NOT QUEUE
>
> **SG**
> → NOT DENY
>
> **NACL**
> → NOT STATEFUL
>
> **PEERING**
> → NOT TRANSITIVE
>
> **DX**
> → NOT ENCRYPTED BY DEFAULT
>
> **FLOW LOGS**
> → NOT PACKET CAPTURE
>
> **BACKUP**
> → NOT FASTEST DR

And the killer question to ask for every answer choice:

> **"What is wrong with this answer?"**

If you can find:

**One requirement it violates**

or:

**One incorrect AWS assumption**

eliminate it.

---

## Related Notes

- [[SAA Exam Strategy]]
- [[18-Architecture Cheat Sheet]]
- [[High Availability Architecture]]
- [[Scalable Architecture]]
- [[Cost-Optimized Architecture]]
- [[Secure Architecture]]
- [[Serverless Architecture]]
- [[Disaster Recovery Overview]]