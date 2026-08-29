## Core Concept

High Availability means designing systems so they:

**Continue operating when individual components fail**

The goal is to reduce:

**Downtime caused by failures**

Common techniques include:

- Multi-AZ deployment
- Load balancing
- Auto Scaling
- Health checks
- Database failover
- Redundant networking
- Managed highly available services

> [!tip] Memory Trick
> **High Availability = Keep Running During Failure**

---

# High Availability vs Disaster Recovery

## High Availability

Goal:

**Stay running**

Think:

- Multi-AZ
- Load Balancers
- Auto Scaling
- Automatic failover

## Disaster Recovery

Goal:

**Recover after major disruption**

Think:

- Backup and Restore
- Pilot Light
- Warm Standby
- Multi-Site

### Killer Shortcut

> **Component/AZ failure**
> → High Availability
>
> **Major site/Region failure**
> → Disaster Recovery

---

# Eliminate Single Points of Failure

A:

**Single Point of Failure**

is any component whose failure can bring down:

**The whole system**

Examples:

- One EC2 instance
- One AZ
- One database server
- One NAT instance
- One application server

### Killer Exam Principle

> **Highly available architectures avoid relying on one instance, one AZ, or one manually managed component**

---

# Multi-AZ Design

For regional high availability:

Deploy critical resources across:

**Multiple Availability Zones**

Architecture:

Users  
↓  
Load Balancer  
↓  
EC2 — AZ A  
EC2 — AZ B

If AZ A fails:

Traffic continues through:

**AZ B**

### Killer Exam Clue

> **Application must survive an Availability Zone failure**
>
> → **Multi-AZ**

---

# Availability Zone Failure

An AZ can experience:

- Power failure
- Network disruption
- Infrastructure failure

A properly designed application should:

**Continue operating through another AZ**

### Memory Trick

**One AZ = Risk**

**Two or More AZs = Resilience**

---

# Load Balancing

[[Application Load Balancer]] can distribute traffic across:

**Healthy targets in multiple AZs**

Benefits:

- Avoid one-server dependence
- Route around unhealthy instances
- Spread traffic

### Killer Exam Clue

> **Need requests routed only to healthy application servers**
>
> → **Load Balancer Health Checks**

---

# Health Checks

A load balancer continuously checks:

**Target health**

If a target fails:

**Traffic stops being sent to it**

Architecture:

ALB  
↓  
EC2 A ✅  
EC2 B ❌  
↓  
Traffic goes to EC2 A

### Memory Trick

**Health Check Fails → Stop Routing**

---

# Auto Scaling

[[Auto Scaling]] helps maintain:

**The required number of healthy EC2 instances**

If an instance fails:

Auto Scaling  
↓  
Detect Unhealthy Instance  
↓  
Replace Instance

### Killer Exam Clue

> **Automatically replace failed EC2 instances**
>
> → **Auto Scaling**

---

# Load Balancer + Auto Scaling

These are commonly used:

**Together**

Architecture:

Internet  
↓  
Load Balancer  
↓  
Auto Scaling Group  
↓  
EC2 Across Multiple AZs

### Memory Trick

**Load Balancer = Send Traffic**

**Auto Scaling = Maintain Capacity**

---

# Auto Scaling Across AZs

An Auto Scaling Group can distribute instances across:

**Multiple Availability Zones**

This protects against:

**Single-AZ failure**

### Exam Principle

> **Do not place the entire Auto Scaling Group in one AZ when HA is required**

---

# Stateless Application Tier

Stateless compute improves:

**High Availability**

because any instance can:

**Handle any request**

Architecture:

ALB  
↓  
EC2 A  
EC2 B  
↓  
Shared State Store

If EC2 A fails:

EC2 B continues without losing:

**Unique local session state**

### Killer Exam Principle

> **Stateless application tiers are easier to fail over**

---

# Database High Availability

Compute HA is not enough if:

**The database is a single point of failure**

Database options may include:

- RDS Multi-AZ
- Aurora replicas
- DynamoDB managed multi-AZ design

### Killer Exam Clue

> **Application tier is Multi-AZ but database must also survive AZ failure**
>
> → Choose a highly available database architecture

---

# RDS Multi-AZ

[[RDS]] Multi-AZ provides:

**Standby database infrastructure in another Availability Zone**

Architecture:

Application  
↓  
Primary RDS — AZ A  
↓  
Synchronous Replication  
↓  
Standby RDS — AZ B

If primary fails:

**Automatic failover**

### Killer Exam Clue

> **Relational database needs automatic AZ failover**
>
> → **RDS Multi-AZ**

---

# RDS Multi-AZ Is for HA

RDS Multi-AZ primarily improves:

**Availability**

It is NOT primarily for:

**Read scaling**

### Killer Exam Trap

> **Need more read capacity**
>
> → Read Replica
>
> **Need failover**
>
> → Multi-AZ

---

# Read Replica vs Multi-AZ

| Requirement | Answer |
|---|---|
| High Availability | Multi-AZ |
| Automatic Failover | Multi-AZ |
| Read Scaling | Read Replica |
| Reporting Queries | Read Replica |

### Memory Trick

**Multi-AZ = Survive**

**Read Replica = Scale Reads**

---

# Aurora High Availability

[[Aurora]] stores data across:

**Multiple Availability Zones**

and supports:

**Multiple Aurora Replicas**

If the writer fails:

An Aurora Replica can be:

**Promoted**

### Killer Exam Clue

> **Need highly available relational database with fast replica failover**
>
> → **Aurora**

---

# DynamoDB High Availability

[[DynamoDB]] is designed as:

**A highly available managed regional service**

It automatically distributes data across:

**Multiple Availability Zones**

### Killer Exam Principle

> **Managed services often provide built-in HA without you managing individual servers**

---

# S3 High Availability

[[S3]] stores objects redundantly across:

**Multiple Availability Zones**

for standard regional storage architectures.

This makes S3 useful for:

- Static assets
- Backups
- Durable object storage

### Exam Principle

> **Do not build unnecessary custom object-storage HA when S3 already provides managed redundancy**

---

# EFS High Availability

[[EFS]] Regional storage can provide:

**Shared filesystem access across multiple AZs**

This is useful when:

**Multiple EC2 instances in different AZs need shared files**

---

# NAT Gateway High Availability

A NAT Gateway is:

**Highly available within one AZ**

For resilient multi-AZ private subnet Internet access:

Deploy:

**One NAT Gateway per AZ**

Architecture:

Private Subnet A  
↓  
NAT A

Private Subnet B  
↓  
NAT B

### Killer Exam Clue

> **Private subnets must retain Internet egress if one AZ fails**
>
> → **NAT Gateway per AZ**

---

# Why Not One NAT Gateway?

If all private subnets use:

**One NAT Gateway in AZ A**

then failure of:

**AZ A**

can disrupt outbound connectivity for:

**Other AZs**

It can also create:

**Cross-AZ traffic**

### Memory Trick

**Each AZ Uses Its Own Exit**

---

# Highly Available Network Design

A strong HA VPC often contains:

Public Subnet — AZ A  
Public Subnet — AZ B

Private App Subnet — AZ A  
Private App Subnet — AZ B

Private DB Subnet — AZ A  
Private DB Subnet — AZ B

### Killer Pattern

> **Critical tiers span multiple AZs**

---

# Internet Gateway

An [[Internet Gateway]] is:

**AWS-managed and highly available**

You do not deploy:

**One IGW per AZ**

### Exam Trap

> **Do not treat IGW like an EC2 appliance**

---

# Route 53 Health Checks

[[Route 53]] can monitor endpoints and:

**Redirect DNS traffic**

when endpoints become:

**Unhealthy**

This is useful for:

- Regional failover
- Application failover
- DR architectures

---

# Multi-Region High Availability

For requirements involving:

**Complete Region failure**

Multi-AZ is not enough.

You may need:

**Multi-Region architecture**

### Killer Exam Clue

> **Application must survive an entire Region outage**
>
> → **Multi-Region**

---

# Multi-AZ vs Multi-Region

| Failure | Architecture |
|---|---|
| Instance Failure | Auto Scaling |
| AZ Failure | Multi-AZ |
| Region Failure | Multi-Region |

### Memory Trick

> **INSTANCE**
> → REPLACE
>
> **AZ**
> → MULTI-AZ
>
> **REGION**
> → MULTI-REGION

---

# Active-Active

In:

**Active-Active**

multiple environments serve:

**Production traffic simultaneously**

Benefits:

- High availability
- Better resource utilization
- Fast failover

### Exam Principle

> **Active-active often provides excellent availability but adds complexity**

---

# Active-Passive

In:

**Active-Passive**

one environment serves traffic while:

**The other waits**

Examples include:

- RDS Multi-AZ
- Route 53 failover architectures
- Multi-Site active-passive

### Memory Trick

**Active = Serving**

**Passive = Ready**

---

# Graceful Degradation

Highly available applications do not always need:

**Every feature working perfectly**

during a failure.

Sometimes the right architecture allows:

**Non-critical features to fail while core service remains available**

### Exam Principle

> **Prioritize essential functionality**

---

# Retry Logic

Temporary failures can often be handled with:

**Retries**

However retries should use:

**Backoff**

to avoid creating:

**More load during an outage**

---

# Exponential Backoff

Exponential backoff increases:

**Delay between retries**

Example:

1 second  
↓  
2 seconds  
↓  
4 seconds  
↓  
8 seconds

### Killer Exam Principle

> **Retries should not create a retry storm**

---

# Jitter

Adding:

**Randomness**

to retry timing helps prevent many clients from retrying:

**At exactly the same moment**

This is called:

**Jitter**

### Memory Trick

**Backoff = Wait Longer**

**Jitter = Don't All Retry Together**

---

# Decoupling for HA

[[SQS]] can improve availability by allowing:

**Work to wait**

if consumers become:

**Temporarily unavailable**

Producer  
↓  
SQS  
↓  
Consumer Down

Messages remain:

**Stored**

until processing resumes.

### Killer Exam Clue

> **Downstream failure should not cause upstream requests to fail**
>
> → **Decouple**

---

# Caching for HA

Caching can reduce reliance on:

**Backend services**

If a database experiences:

**Temporary load issues**

cached data may allow:

**Some requests to continue**

However:

**Cache is not a substitute for database HA**

---

# Managed Services

Managed AWS services can reduce HA complexity because AWS handles:

- Replication
- Failover
- Infrastructure replacement
- Scaling

### Killer Exam Clue

> **Need high availability with minimal operational effort**
>
> → Prefer **managed services**

---

# Application Load Balancer Health

Do not rely only on:

**EC2 process status**

The load balancer should check whether:

**The application endpoint actually works**

Example:

`/health`

### Exam Principle

> **A running server can still host a broken application**

---

# Database Connection Resilience

Applications should handle:

**Database failover**

without assuming:

**A specific database host never changes**

Use:

**Managed DNS endpoints**

rather than hardcoding:

**Instance IP addresses**

---

# DNS TTL and Failover

DNS-based failover depends partly on:

**TTL**

A shorter TTL can allow clients to:

**Refresh DNS answers sooner**

but increases:

**DNS query frequency**

### Exam Principle

> **DNS failover is not always instantaneous**

---

# Data Durability vs Availability

These terms are different.

## Durability

Think:

**Will the data survive?**

## Availability

Think:

**Can I access the service now?**

### Example

S3 may provide extremely high:

**Durability**

while application availability still depends on:

**The full architecture**

### Memory Trick

**Durability = Data Survives**

**Availability = Service Responds**

---

# Fault Tolerance vs High Availability

## High Availability

Attempts to:

**Minimize downtime**

Some brief failover interruption may occur.

## Fault Tolerance

Attempts to continue operating:

**Without interruption**

despite component failure.

### Exam Principle

> **Fault tolerance generally requires more redundancy and cost**

---

# Architecture Thinking

## Scenario 1 — Single EC2

Application runs on:

**One EC2 instance**

and downtime is unacceptable.

Better:

ALB  
+  
Auto Scaling  
+  
Multiple AZs

---

## Scenario 2 — AZ Failure

Application must continue if:

**AZ A goes down**

Deploy:

**Compute across AZ A and AZ B**

---

## Scenario 3 — Database Failure

RDS database must fail over automatically if:

**Primary DB instance fails**

Choose:

**RDS Multi-AZ**

---

## Scenario 4 — Read Scaling

Database is healthy but read traffic is:

**Too high**

Choose:

**Read Replica**

not Multi-AZ as the main scaling answer.

---

## Scenario 5 — Private Subnet Egress

Application spans:

Two AZs

but both private subnets use:

**One NAT Gateway**

Need stronger HA.

Use:

**NAT Gateway per AZ**

---

## Scenario 6 — Worker Failure

Consumers temporarily stop processing.

Producers must continue accepting work.

Use:

**SQS**

---

## Scenario 7 — Region Failure

Business requires continued service even if:

**Entire Region becomes unavailable**

Use:

**Multi-Region architecture**

---

# Scenario Recognition

Immediately think:

**Multi-AZ**

when you see:

- AZ failure
- Regional HA
- Redundant application tiers
- Multiple subnets

---

## Think Auto Scaling When You See

- Replace unhealthy EC2
- Maintain instance count
- Automatic capacity

---

## Think Load Balancer When You See

- Healthy target routing
- Multiple app servers
- Traffic distribution

---

## Think RDS Multi-AZ When You See

- Database failover
- Relational database HA
- Standby database

---

## Think Multi-Region When You See

- Region outage
- Global resilience
- Regional disaster

---

# Exam Traps

## Trap 1 — One Large EC2 Instance Is Highly Available

❌

It remains:

**One failure point**

---

## Trap 2 — Multi-AZ and Read Replica Are the Same

❌

Multi-AZ:

**Availability**

Read Replica:

**Read scalability**

---

## Trap 3 — One NAT Gateway Provides Full Multi-AZ Resilience

❌

For stronger AZ independence:

**One NAT Gateway per AZ**

---

## Trap 4 — Multi-AZ Protects Against Complete Region Failure

❌

Think:

**Multi-Region**

---

## Trap 5 — High Availability Means Zero Downtime

❌

High Availability aims to:

**Minimize downtime**

not necessarily eliminate every interruption.

---

## Trap 6 — Durable Data Automatically Means Highly Available Application

❌

Application availability depends on:

**All architecture layers**

---

# Quick Cheat Sheet

| Exam Clue | Answer |
|---|---|
| Instance Failure | Auto Scaling |
| Healthy Traffic Distribution | Load Balancer |
| AZ Failure | Multi-AZ |
| Database Failover | RDS Multi-AZ |
| Database Read Scaling | Read Replica |
| Region Failure | Multi-Region |
| Private Egress HA | NAT Gateway per AZ |
| Async Resilience | SQS |
| Global DNS Failover | Route 53 |
| Replaceable App Tier | Stateless Compute |
| Lower Ops HA | Managed Services |

---

# HA Decision Map

Need:

**Replace failed EC2**

→ Auto Scaling

Need:

**Stop routing to failed EC2**

→ Load Balancer

Need:

**Survive AZ failure**

→ Multi-AZ

Need:

**Relational DB automatic failover**

→ RDS Multi-AZ

Need:

**More DB reads**

→ Read Replica

Need:

**Survive Region failure**

→ Multi-Region

Need:

**Private subnet egress across AZ failure**

→ NAT Gateway per AZ

Need:

**Downstream failures buffered**

→ SQS

---

# Failure Domain Map

> **INSTANCE FAILS**
> → REPLACE
>
> **APPLICATION TARGET FAILS**
> → STOP ROUTING
>
> **AZ FAILS**
> → MULTI-AZ
>
> **DATABASE FAILS**
> → FAILOVER
>
> **REGION FAILS**
> → MULTI-REGION

---

# Final Exam Rapid-Fire

> **HIGH AVAILABILITY**
> → REDUNDANCY
>
> **INSTANCE FAILURE**
> → AUTO SCALING
>
> **UNHEALTHY TARGET**
> → LOAD BALANCER
>
> **AZ FAILURE**
> → MULTI-AZ
>
> **RDS FAILOVER**
> → MULTI-AZ
>
> **RDS READ SCALE**
> → READ REPLICA
>
> **REGION FAILURE**
> → MULTI-REGION
>
> **PRIVATE EGRESS HA**
> → NAT PER AZ
>
> **TEMPORARY BACKEND FAILURE**
> → SQS
>
> **STATELESS**
> → EASY REPLACEMENT
>
> **DNS FAILOVER**
> → ROUTE 53

---

## Master Memory Trick

> [!tip] High Availability Master Memory Trick
> Imagine your application is:
>
> **A hospital**
>
> One doctor?
>
> **Single point of failure**
>
> Multiple doctors?
>
> Better.
>
> One operating room?
>
> **Single point of failure**
>
> Multiple operating rooms in different buildings?
>
> Better.
>
> One database?
>
> Give it:
>
> **A standby**
>
> One server fails?
>
> **Replace it**
>
> One AZ fails?
>
> **Use another AZ**
>
> One Region fails?
>
> **Use another Region**

So remember:

> **AUTO SCALING**
> → REPLACE
>
> **LOAD BALANCER**
> → ROUTE AROUND FAILURE
>
> **MULTI-AZ**
> → SURVIVE AZ
>
> **RDS MULTI-AZ**
> → DATABASE FAILOVER
>
> **MULTI-REGION**
> → SURVIVE REGION
>
> **STATELESS**
> → REPLACEABLE COMPUTE

And the killer SAA question:

> **"What happens when this component fails?"**
>
> If the answer is:
>
> **"The application goes down"**
>
> then you probably found:
>
> **A single point of failure**

---

## Related Notes

- [[Architecture Principles]]
- [[Stateless vs Stateful Architecture]]
- [[Decoupled Architecture]]
- [[Application Load Balancer]]
- [[Auto Scaling]]
- [[RDS]]
- [[Aurora]]
- [[DynamoDB]]
- [[SQS]]
- [[Route 53]]
- [[Disaster Recovery Overview]]