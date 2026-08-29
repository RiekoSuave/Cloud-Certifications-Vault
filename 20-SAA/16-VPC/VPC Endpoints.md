## What Problem Does It Solve?

[[VPC Endpoints]] provide:

**Private connectivity from a VPC to supported AWS services**

without requiring:

- Internet Gateway
- NAT Gateway
- Public IP addresses
- Public Internet routing

Architecture:

Private Subnet  
↓  
VPC Endpoint  
↓  
AWS Service

> [!tip] Memory Trick
> **VPC Endpoint = Private Door to AWS Services**

---

## Core Concept

Without a VPC endpoint, a private EC2 instance may reach an AWS service through:

Private EC2  
↓  
NAT Gateway  
↓  
Internet Gateway  
↓  
AWS Service Public Endpoint

With a VPC endpoint:

Private EC2  
↓  
VPC Endpoint  
↓  
AWS Service

Traffic stays on:

**AWS networking**

### Killer Exam Clue

> **Private instances need access to an AWS service without Internet or NAT**
>
> → **VPC Endpoint**

---

# Why Use VPC Endpoints?

Benefits include:

- Private service access
- Reduced Internet exposure
- Less dependence on NAT Gateway
- Potential NAT cost reduction
- Simplified private architectures

### Memory Trick

**No NAT Needed for Supported Private Service Access**

---

# Two Major Endpoint Types

For SAA, the most important endpoint types are:

1. **Gateway Endpoints**
2. **Interface Endpoints**

### Killer Memory Trick

**Gateway = S3 + DynamoDB**

**Interface = PrivateLink + ENI**

---

# Gateway Endpoints

A:

**Gateway Endpoint**

provides private access to:

- [[S3]]
- [[DynamoDB]]

It works through:

**VPC route tables**

Architecture:

Private Subnet  
↓  
Route Table  
↓  
Gateway Endpoint  
↓  
S3 / DynamoDB

### Killer Exam Clue

> **Private subnet needs S3 access without NAT Gateway**
>
> → **S3 Gateway Endpoint**

---

# Gateway Endpoint Route Table

When configuring a Gateway Endpoint, selected:

**Route Tables**

receive routes directing supported service traffic to:

**The endpoint**

### Memory Trick

**Gateway Endpoint = Route Table Entry**

---

# Gateway Endpoint Cost

Gateway Endpoints generally do not have the same:

**Hourly endpoint charges**

associated with Interface Endpoints.

This can make them attractive for:

**S3 and DynamoDB private access**

### Killer Exam Cost Clue

> **Reduce NAT Gateway cost for heavy S3 traffic**
>
> → **S3 Gateway Endpoint**

---

# Gateway Endpoint Security

Gateway Endpoints can use:

**Endpoint Policies**

to control:

**What resources/services can be accessed through the endpoint**

Example:

Private EC2  
↓  
S3 Gateway Endpoint  
↓  
Only Approved Bucket

### Killer Exam Clue

> **Restrict S3 access through a VPC endpoint to specific buckets**
>
> → **Endpoint Policy**

---

# Interface Endpoints

An:

**Interface Endpoint**

creates:

**Elastic Network Interfaces — ENIs**

inside selected subnets.

It uses:

**AWS PrivateLink**

Architecture:

Private Resource  
↓  
Interface Endpoint ENI  
↓  
PrivateLink  
↓  
AWS Service

### Killer Exam Clue

> **Private subnet needs access to Secrets Manager without NAT**
>
> → **Interface VPC Endpoint**

---

# Interface Endpoint Examples

Common use cases include private access to services such as:

- [[Secrets Manager]]
- KMS
- Systems Manager
- SNS
- SQS
- CloudWatch
- API Gateway private APIs
- Other supported AWS services

### Memory Trick

**Most Supported AWS Services**
→ Interface Endpoint

---

# Interface Endpoint ENIs

Interface Endpoints place:

**Private IP addresses**

inside your VPC through:

**ENIs**

Applications connect to those:

**Private addresses**

instead of the service's public endpoint path.

---

# Security Groups

Interface Endpoints use:

[[Security Groups]]

to control:

**Which resources can connect to the endpoint**

Example:

EC2  
↓  
Interface Endpoint SG  
↓  
Secrets Manager

### Killer Exam Clue

> **Need to restrict access to an interface VPC endpoint**
>
> → **Security Group**

---

# Private DNS

Interface Endpoints commonly support:

**Private DNS**

When enabled, the normal AWS service hostname can resolve to:

**The private endpoint IP addresses**

inside the VPC.

Example:

Application requests:

`secretsmanager.<region>.amazonaws.com`

DNS resolves internally to:

**Interface Endpoint**

### Memory Trick

**Same Service Name → Private Route**

---

# Private DNS Benefit

Without private DNS:

Applications may need to use:

**Endpoint-specific DNS names**

With private DNS enabled:

Applications can often continue using:

**The standard service hostname**

This minimizes:

**Application changes**

---

# Interface Endpoint Cost

Interface Endpoints typically have:

- Hourly charges
- Data processing charges

### SAA Principle

> **Interface Endpoints improve private connectivity, but are not always cheaper than every alternative**

---

# Gateway vs Interface Endpoints

| Feature | Gateway Endpoint | Interface Endpoint |
|---|---|---|
| Primary Services | S3, DynamoDB | Many AWS Services |
| Uses ENI | ❌ | ✅ |
| Uses Route Table | ✅ | ❌ Primary |
| Security Groups | ❌ | ✅ |
| PrivateLink | ❌ | ✅ |
| Hourly Endpoint Charge | Generally No | Typically Yes |
| Private DNS | ❌ Primary | ✅ Common |

### Killer Shortcut

**S3 / DynamoDB**
→ Gateway Endpoint

**Secrets Manager / Systems Manager / many others**
→ Interface Endpoint

---

# Endpoint Policies

A:

**VPC Endpoint Policy**

controls:

**What actions/resources may be accessed through an endpoint**

Example:

Allow:

Only `GetObject`

on:

`arn:aws:s3:::company-private-data/*`

### Important Distinction

Endpoint policies do NOT replace:

- IAM policies
- Resource policies
- Security Groups

They provide:

**An additional layer of access control**

### Memory Trick

**Endpoint Policy = What Can Pass Through This Private Door**

---

# Endpoint Policy + IAM

For a request to succeed, multiple authorization layers may need to allow it.

Example:

EC2 Role  
↓  
IAM Policy  
↓  
VPC Endpoint Policy  
↓  
S3 Bucket Policy  
↓  
S3 Object

### SAA Principle

> **Effective access is the combination of applicable policies**

---

# S3 Bucket Policy + VPC Endpoint

An S3 bucket policy can restrict access so requests must come through:

**A specific VPC endpoint**

### Killer Exam Clue

> **S3 bucket must only be accessible through a designated VPC endpoint**
>
> → **S3 Bucket Policy using VPC Endpoint condition**

---

# Private S3 Architecture

Architecture:

Private EC2  
↓  
S3 Gateway Endpoint  
↓  
S3

No:

- Public IP
- NAT Gateway
- Internet Gateway path

### Killer Exam Pattern

> **Private instances upload large amounts of data to S3**
>
> → Use **S3 Gateway Endpoint**

---

# Private DynamoDB Architecture

Private Application  
↓  
DynamoDB Gateway Endpoint  
↓  
[[DynamoDB]]

This avoids:

**NAT Gateway**

for DynamoDB traffic.

---

# Private Secrets Manager Architecture

Private EC2 / Lambda  
↓  
Secrets Manager Interface Endpoint  
↓  
[[Secrets Manager]]

Use when:

**Credentials must be retrieved without public Internet access**

---

# Private Systems Manager Architecture

Private EC2 instances can use:

**Interface Endpoints**

for supported Systems Manager services.

This helps enable:

**Systems Manager connectivity without Internet/NAT**

### Killer Exam Clue

> **Private EC2 instances need Session Manager but no NAT Gateway**
>
> → **Systems Manager Interface Endpoints**

---

# VPC Endpoint vs NAT Gateway

## NAT Gateway

Provides:

**General outbound IPv4 Internet access**

## VPC Endpoint

Provides:

**Private access to specific supported services**

### Killer Shortcut

Need to reach:

Any Internet website  
→ NAT Gateway

Need only:

S3  
→ Gateway Endpoint

Need only:

Secrets Manager  
→ Interface Endpoint

### Memory Trick

**NAT = Internet**

**Endpoint = Specific Private Service**

---

# Cost Optimization with Endpoints

Suppose private EC2 instances transfer:

**Large amounts of data to S3**

through a NAT Gateway.

Architecture:

EC2  
↓  
NAT Gateway  
↓  
S3

This can incur:

**NAT data processing charges**

Better:

EC2  
↓  
S3 Gateway Endpoint  
↓  
S3

### Killer Exam Clue

> **Reduce NAT Gateway costs caused by S3 traffic**
>
> → **S3 Gateway Endpoint**

---

# VPC Endpoint vs Internet Gateway

## Internet Gateway

Provides:

**Public Internet connectivity**

## VPC Endpoint

Provides:

**Private service connectivity**

No public IP is needed for:

**Endpoint access**

---

# VPC Endpoint vs VPC Peering

## [[VPC Peering]]

Connects:

**Two VPC networks**

## VPC Endpoint

Connects:

**A VPC to a specific service**

### Killer Shortcut

**VPC-to-VPC**
→ Peering

**VPC-to-service**
→ Endpoint

---

# VPC Endpoint vs PrivateLink

This relationship matters.

## Interface Endpoint

Is built using:

**AWS PrivateLink**

## PrivateLink

Is the broader technology for:

**Private service connectivity**

### Memory Trick

**Interface Endpoint = Consumer Side of PrivateLink**

---

# Endpoint Services

Organizations can expose their own services privately using:

**PrivateLink Endpoint Services**

Architecture:

Provider VPC  
↓  
Network Load Balancer  
↓  
Endpoint Service  
↓  
PrivateLink  
↓  
Consumer Interface Endpoint

### Killer Exam Clue

> **Privately expose an application to customer VPCs without peering**
>
> → **PrivateLink Endpoint Service**

---

# VPC Endpoint vs Transit Gateway

## [[05-Networking/Transit Gateway]]

Provides:

**Network connectivity among VPCs and hybrid networks**

## VPC Endpoint

Provides:

**Private access to services**

They solve:

**Different problems**

---

# Regional Nature

VPC Endpoints are generally:

**Regional resources**

Applications should create endpoints in:

**Regions where private service access is required**

---

# High Availability for Interface Endpoints

For resilient access:

Create endpoint ENIs in:

**Multiple Availability Zones**

where appropriate.

### SAA Principle

> **Multi-AZ applications should consider Multi-AZ endpoint placement**

---

# DNS Troubleshooting

If an application can reach an endpoint-specific hostname but not:

**The normal AWS service hostname**

check:

- Private DNS setting
- VPC DNS settings
- DNS resolution

### Killer Exam Clue

> **Interface Endpoint exists but standard service hostname still resolves publicly**
>
> → Check **Private DNS**

---

# Route Troubleshooting

For Gateway Endpoints, if private resources cannot reach:

S3 / DynamoDB

check:

**The subnet's associated route table**

### Memory Trick

**Gateway Issue → Check Routes**

**Interface Issue → Check SG + DNS**

---

# Architecture Thinking

## Scenario 1 — Private S3 Access

EC2 in private subnet needs:

**S3 access**

without NAT.

Choose:

**S3 Gateway Endpoint**

---

## Scenario 2 — Private DynamoDB Access

Application needs:

**DynamoDB**

without Internet.

Choose:

**DynamoDB Gateway Endpoint**

---

## Scenario 3 — Private Secrets Manager

Private EC2 needs:

**Secrets Manager**

without NAT.

Choose:

**Interface Endpoint**

---

## Scenario 4 — General Internet Updates

Private EC2 needs:

- yum updates
- External websites
- Third-party APIs

VPC Endpoint alone is not enough.

Choose:

**NAT Gateway**

---

## Scenario 5 — Reduce NAT Cost

Private workload sends:

Terabytes to S3.

Choose:

**S3 Gateway Endpoint**

---

## Scenario 6 — Restrict S3 Access

Private EC2 should access only:

`company-data`

through the endpoint.

Use:

**Endpoint Policy**

and appropriate:

**IAM / S3 policies**

---

## Scenario 7 — Standard DNS Name

Application should continue using:

The normal Secrets Manager hostname.

Choose:

**Interface Endpoint + Private DNS**

---

## Scenario 8 — Private SaaS Service

Provider needs to expose:

One private application

to many consumer VPCs.

Choose:

**PrivateLink**

---

# Scenario Recognition

Immediately think:

**VPC Endpoint**

when you see:

- Private AWS service access
- No NAT
- No Internet
- Private S3
- Private DynamoDB
- Interface Endpoint
- Gateway Endpoint
- PrivateLink
- Endpoint Policy

---

## Think Gateway Endpoint When You See

- S3
- DynamoDB
- Route tables
- Reduce NAT cost

---

## Think Interface Endpoint When You See

- ENI
- PrivateLink
- Security Group
- Private DNS
- Most supported AWS services

---

## Think NAT Gateway When You See

- General outbound Internet
- External APIs
- Software updates from Internet

---

# Exam Traps

## Trap 1 — Every VPC Endpoint Uses an ENI

❌

Interface Endpoints:

**Yes**

Gateway Endpoints:

**No**

---

## Trap 2 — S3 Requires Interface Endpoint for Basic Private Access

❌

The classic SAA answer is:

**S3 Gateway Endpoint**

---

## Trap 3 — Gateway Endpoints Use Security Groups

❌

They primarily use:

**Route tables + endpoint policies**

---

## Trap 4 — Interface Endpoints Use Route Table Entries Like Gateway Endpoints

❌

They create:

**ENIs**

inside subnets.

---

## Trap 5 — Endpoint Policy Replaces IAM

❌

It is:

**An additional authorization layer**

---

## Trap 6 — VPC Endpoint Provides General Internet Access

❌

It provides:

**Private access to specific services**

---

## Trap 7 — Interface Endpoint Exists, So DNS Always Works Automatically

❌

Check:

**Private DNS configuration**

---

# Quick Cheat Sheet

| Exam Clue | Answer |
|---|---|
| Private AWS Service Access | VPC Endpoint |
| Private S3 | Gateway Endpoint |
| Private DynamoDB | Gateway Endpoint |
| Route Table Endpoint | Gateway Endpoint |
| ENI-Based Endpoint | Interface Endpoint |
| PrivateLink | Interface Endpoint |
| Endpoint Security Group | Interface Endpoint |
| Standard Service DNS Privately | Private DNS |
| Restrict Endpoint Access | Endpoint Policy |
| General Internet Access | NAT Gateway |
| Reduce NAT Cost for S3 | Gateway Endpoint |

---

# Endpoint Decision Map

Need:

**S3 privately**

→ Gateway Endpoint

Need:

**DynamoDB privately**

→ Gateway Endpoint

Need:

**Secrets Manager privately**

→ Interface Endpoint

Need:

**Systems Manager privately**

→ Interface Endpoint

Need:

**General Internet**

→ NAT Gateway

Need:

**Expose private service**

→ PrivateLink

---

# Final Exam Rapid-Fire

> **PRIVATE AWS SERVICE ACCESS**
> → VPC ENDPOINT
>
> **S3**
> → GATEWAY ENDPOINT
>
> **DYNAMODB**
> → GATEWAY ENDPOINT
>
> **ROUTE TABLE**
> → GATEWAY ENDPOINT
>
> **ENI**
> → INTERFACE ENDPOINT
>
> **PRIVATELINK**
> → INTERFACE ENDPOINT
>
> **SECURITY GROUP**
> → INTERFACE ENDPOINT
>
> **PRIVATE DNS**
> → INTERFACE ENDPOINT
>
> **GENERAL INTERNET**
> → NAT GATEWAY
>
> **REDUCE S3 NAT COST**
> → GATEWAY ENDPOINT
>
> **PRIVATE SERVICE EXPOSURE**
> → PRIVATELINK

---

## Master Memory Trick

> [!tip] VPC Endpoints Master Memory Trick
> Imagine your private subnet is:
>
> **A locked office building**
>
> Normally, to reach an AWS service, employees leave the building through:
>
> **NAT**
>
> travel outside,
>
> and reach the service.
>
> A VPC Endpoint instead builds:
>
> **A PRIVATE HALLWAY**
>
> directly to the AWS service.
>
> For:
>
> **S3 + DYNAMODB**
>
> use:
>
> **GATEWAY ENDPOINT**
>
> For many other AWS services:
>
> use:
>
> **INTERFACE ENDPOINT**
>
> which places:
>
> **A PRIVATE ENI**
>
> inside your VPC.

So remember:

> **ENDPOINT**
> → PRIVATE AWS ACCESS
>
> **GATEWAY**
> → S3 + DYNAMODB
>
> **INTERFACE**
> → ENI + PRIVATELINK
>
> **PRIVATE DNS**
> → NORMAL HOSTNAME, PRIVATE PATH
>
> **ENDPOINT POLICY**
> → CONTROL THE PRIVATE DOOR
>
> **NAT**
> → GENERAL INTERNET

And the killer SAA question:

> **"Does a private workload need to reach a supported AWS service without using a NAT Gateway, Internet Gateway, or public IP?"**
>
> YES
>
> → **VPC Endpoint**

---

## Related Notes

- [[VPC]]
- [[VPC Peering]]
- [[05-Networking/PrivateLink]]
- [[Security Groups]]
- [[S3]]
- [[DynamoDB]]
- [[Secrets Manager]]
- [[Systems Manager]]
- [[NAT Gateway]]