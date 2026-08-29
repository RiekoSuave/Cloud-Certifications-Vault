## What Problem Does It Solve?

[[PrivateLink]] provides:

**Private connectivity to services without exposing traffic to the public Internet**

It is especially useful when:

- A provider exposes one private service
- Consumers should not receive full VPC network access
- VPC peering would create too many connections
- CIDR overlap makes network-to-network connectivity difficult

Architecture:

Consumer VPC  
↓  
Interface Endpoint  
↓  
PrivateLink  
↓  
Endpoint Service  
↓  
Provider Application

> [!tip] Memory Trick
> **PrivateLink = Private Access to ONE Service**

---

## Core Concept

PrivateLink is designed for:

**Service-to-consumer connectivity**

rather than:

**Full VPC-to-VPC connectivity**

### Killer Exam Clue

> **Need to expose a private application to many VPCs without VPC peering**
>
> → **PrivateLink**

---

# Provider and Consumer Model

PrivateLink uses two sides:

## Service Provider

Owns:

**The service being exposed**

## Service Consumer

Connects through:

**An Interface VPC Endpoint**

Architecture:

Consumer  
↓  
Interface Endpoint  
↓  
PrivateLink  
↓  
Provider Service

### Memory Trick

**Provider = Offers Service**

**Consumer = Uses Service**

---

# Endpoint Service

The provider creates an:

**Endpoint Service**

This represents:

**The private service consumers can connect to**

A classic architecture uses:

**Network Load Balancer**

in front of:

**The provider application**

### Killer Exam Clue

> **Need to publish a private service through PrivateLink**
>
> → **Endpoint Service**

---

# Network Load Balancer

A common provider architecture:

Application Targets  
↓  
[[Network Load Balancer]]  
↓  
Endpoint Service  
↓  
PrivateLink

### Memory Trick

**PrivateLink Provider Side = NLB**

---

# Consumer Interface Endpoint

The consumer creates:

**An Interface Endpoint**

inside:

**Its own VPC**

Architecture:

Consumer Application  
↓  
Interface Endpoint ENI  
↓  
PrivateLink  
↓  
Provider Service

### Killer Exam Clue

> **Consumer needs private access to a PrivateLink service**
>
> → **Interface Endpoint**

---

# ENIs

Interface endpoints create:

**Elastic Network Interfaces**

inside consumer subnets.

These ENIs receive:

**Private IP addresses**

### Memory Trick

**Interface Endpoint = ENI Inside Your VPC**

---

# Security Groups

Interface endpoints use:

[[Security Groups]]

to control:

**Who can connect to the endpoint**

Example:

Consumer Application SG  
↓  
Endpoint SG  
↓  
PrivateLink Service

### Killer Exam Clue

> **Restrict which applications can connect to a PrivateLink service**
>
> → **Interface Endpoint Security Group**

---

# No Public Internet

PrivateLink traffic does not require:

- Public IPs
- Internet Gateway
- NAT Gateway
- Public Internet routing

### Killer Exam Clue

> **Service traffic must remain private**
>
> → **PrivateLink**

---

# No Full VPC Connectivity

This is one of the biggest advantages.

PrivateLink exposes:

**Only the specific service**

It does NOT provide consumers with:

**General access to the provider VPC**

### Memory Trick

**PrivateLink = Service Access**

Not:

**Network Access**

---

# PrivateLink vs VPC Peering

This is the most important comparison.

## [[VPC Peering]]

Provides:

**VPC-to-VPC network connectivity**

## PrivateLink

Provides:

**Private access to a specific service**

### Killer Shortcut

**Need both networks connected**
→ VPC Peering

**Need only one application/service**
→ PrivateLink

---

# CIDR Overlap Advantage

VPC Peering requires:

**Non-overlapping CIDRs**

PrivateLink does not require the consumer and provider to establish:

**Full routed network connectivity**

This makes it useful when:

**CIDR ranges overlap**

### Killer Exam Clue

> **Customer VPCs have overlapping CIDRs but need private access to one service**
>
> → **PrivateLink**

---

# Why Overlapping CIDRs Are Less Problematic

Consumers connect to:

**Private endpoint ENIs inside their own VPC**

They are not routing directly into:

**The provider VPC CIDR**

### Memory Trick

**PrivateLink Hides the Provider Network**

---

# PrivateLink vs Transit Gateway

## [[05-Networking/Transit Gateway]]

Think:

**Connect many networks**

## PrivateLink

Think:

**Expose one service**

### Killer Shortcut

Many VPCs need broad connectivity  
→ Transit Gateway

Many VPCs need one shared application  
→ PrivateLink

---

# PrivateLink vs VPC Endpoint

These terms are closely related.

## PrivateLink

The underlying technology for:

**Private service connectivity**

## Interface VPC Endpoint

The consumer-side resource used to:

**Connect through PrivateLink**

### Memory Trick

**PrivateLink = Technology**

**Interface Endpoint = Door**

---

# AWS Services and PrivateLink

Many AWS services can be accessed through:

**Interface VPC Endpoints**

powered by:

**PrivateLink**

Examples include:

- Secrets Manager
- Systems Manager
- KMS
- SNS
- SQS
- CloudWatch

### Exam Principle

> **Interface Endpoints commonly use PrivateLink**

---

# Private SaaS Architecture

PrivateLink is useful for:

**SaaS providers**

Architecture:

SaaS Provider VPC  
↓  
NLB  
↓  
Endpoint Service  
↓  
PrivateLink  
↓  
Customer Interface Endpoints

Each customer can access:

**The service privately**

without joining:

**The provider network**

### Killer Exam Clue

> **SaaS provider needs private connectivity to many customer VPCs**
>
> → **PrivateLink**

---

# Multi-Account Architecture

PrivateLink works well across:

**AWS accounts**

Example:

Shared Services Account  
↓  
PrivateLink Endpoint Service  
↓  
Application Accounts

### Killer Exam Clue

> **Expose a shared internal service privately across multiple accounts**
>
> → **PrivateLink**

---

# Service Acceptance

Endpoint services can be configured so providers:

**Approve connection requests**

from consumers.

This gives the provider more control over:

**Who can connect**

### Memory Trick

**Provider Can Approve Consumers**

---

# Private DNS

PrivateLink architectures can use:

**Private DNS**

so consumers access the service using:

**Friendly DNS names**

instead of endpoint-specific names.

### Exam Principle

> **Private DNS improves application transparency**

---

# Route Tables

Unlike Gateway Endpoints, Interface Endpoints do not primarily require:

**Route-table entries pointing to the endpoint**

Traffic reaches:

**The endpoint ENI**

using normal VPC routing.

### Killer Shortcut

**Gateway Endpoint**
→ Route table

**PrivateLink Interface Endpoint**
→ ENI + Security Group

---

# PrivateLink and High Availability

For resilient consumer access:

Create Interface Endpoints in:

**Multiple Availability Zones**

where appropriate.

On the provider side:

Use a highly available:

**Network Load Balancer**

across:

**Multiple AZs**

### SAA Principle

> **Design both provider and consumer sides for Multi-AZ availability**

---

# PrivateLink Scaling

PrivateLink is designed to support:

**Large numbers of service consumers**

without requiring:

**Full-mesh VPC peering**

This is a major architectural advantage.

### Memory Trick

**Many Consumers + One Service = PrivateLink**

---

# PrivateLink vs NAT Gateway

## NAT Gateway

Provides:

**General outbound Internet access**

## PrivateLink

Provides:

**Private access to a specific service**

### Killer Shortcut

Need external website  
→ NAT Gateway

Need private internal/SaaS service  
→ PrivateLink

---

# PrivateLink vs VPN

## Site-to-Site VPN

Connects:

**Networks**

## PrivateLink

Connects:

**Consumer to service**

### Memory Trick

**VPN = Network Tunnel**

**PrivateLink = Service Tunnel**

---

# PrivateLink vs Direct Connect

## [[05-Networking/Direct Connect]]

Provides:

**Dedicated hybrid connectivity**

between:

On-premises  
↔  
AWS

## PrivateLink

Provides:

**Private service access**

inside AWS networking architectures.

---

# Security Benefits

PrivateLink can reduce exposure because:

- Provider service need not be public
- Consumer traffic stays private
- Full VPC routing is unnecessary
- Provider network topology is hidden

### Killer Exam Principle

> **Expose only what consumers need**

---

# Architecture Thinking

## Scenario 1 — Shared Internal Service

Company has:

50 application VPCs.

All need access to:

**One central billing API**

They should NOT have:

Full network access to the billing VPC.

Choose:

**PrivateLink**

---

## Scenario 2 — Two VPCs Need Full Connectivity

VPC A and VPC B need:

- Many services
- Broad private routing
- Direct network access

Choose:

**VPC Peering**

rather than PrivateLink.

---

## Scenario 3 — Overlapping CIDRs

Customer VPC:

`10.0.0.0/16`

Provider VPC:

`10.0.0.0/16`

Need private access to:

**One provider application**

Choose:

**PrivateLink**

---

## Scenario 4 — Hundreds of Customer VPCs

SaaS provider must privately expose:

**One API**

to hundreds of customers.

Choose:

**PrivateLink**

not hundreds of peering connections.

---

## Scenario 5 — Consumer Side

Consumer needs to access:

A PrivateLink endpoint service.

Create:

**Interface Endpoint**

---

## Scenario 6 — Provider Side

Provider wants to expose:

Private application

through PrivateLink.

Classic pattern:

Application  
↓  
Network Load Balancer  
↓  
Endpoint Service

---

## Scenario 7 — General Internet Access

Private EC2 needs:

Operating-system updates from Internet.

PrivateLink is NOT a replacement for:

**NAT Gateway**

---

# Scenario Recognition

Immediately think:

**PrivateLink**

when you see:

- Private service exposure
- Specific service only
- SaaS provider
- Many consumer VPCs
- Overlapping CIDRs
- Endpoint service
- Interface endpoint
- No VPC peering
- No public Internet

---

## Think VPC Peering When You See

- Full VPC connectivity
- Two networks
- Non-overlapping CIDRs
- Broad routing

---

## Think Transit Gateway When You See

- Many VPCs
- Broad connectivity
- Hub-and-spoke
- Transitive routing

---

## Think Interface Endpoint When You See

- Consumer side
- ENI
- Security Group
- PrivateLink connection

---

# Exam Traps

## Trap 1 — PrivateLink Connects Entire VPC Networks

❌

It exposes:

**Specific services**

---

## Trap 2 — PrivateLink Requires Non-Overlapping CIDRs Like Peering

❌

It can work well when:

**CIDRs overlap**

because full routed VPC connectivity is not established.

---

## Trap 3 — Consumer Creates an NLB

❌

Classic architecture:

Provider  
→ NLB

Consumer  
→ Interface Endpoint

---

## Trap 4 — PrivateLink Requires Internet Gateway

❌

Traffic remains:

**Private**

---

## Trap 5 — PrivateLink Is the Same as Transit Gateway

❌

Transit Gateway:

**Connect networks**

PrivateLink:

**Expose services**

---

## Trap 6 — PrivateLink Provides General Internet Access

❌

Think:

**NAT Gateway**

---

## Trap 7 — Interface Endpoint Is a Gateway Endpoint

❌

Interface Endpoint:

**ENI + PrivateLink**

Gateway Endpoint:

**S3/DynamoDB + Route Table**

---

# Quick Cheat Sheet

| Exam Clue | Answer |
|---|---|
| Private Specific Service | PrivateLink |
| Consumer Resource | Interface Endpoint |
| Provider Resource | Endpoint Service |
| Classic Provider Front End | NLB |
| Full VPC Connectivity | VPC Peering |
| Many Network Connections | Transit Gateway |
| Overlapping CIDRs + One Service | PrivateLink |
| SaaS Private Access | PrivateLink |
| Interface Endpoint | ENI |
| Endpoint Security | Security Group |
| Public Internet Needed | ❌ |

---

# Connectivity Decision Map

Need:

**One private service**

→ PrivateLink

Need:

**Two VPC networks**

→ VPC Peering

Need:

**Many VPC networks**

→ Transit Gateway

Need:

**Private AWS service access**

→ Interface VPC Endpoint

Need:

**General Internet**

→ NAT Gateway

---

# PrivateLink Architecture Map

> **PROVIDER**
>
> Application
> ↓
> Network Load Balancer
> ↓
> Endpoint Service
>
> **PRIVATE LINK**
> ↓
>
> **CONSUMER**
>
> Interface Endpoint
> ↓
> Consumer Application

### Memory Trick

> **PROVIDER**
> → NLB + ENDPOINT SERVICE
>
> **CONSUMER**
> → INTERFACE ENDPOINT

---

# Final Exam Rapid-Fire

> **ONE PRIVATE SERVICE**
> → PRIVATELINK
>
> **SAAS PRIVATE ACCESS**
> → PRIVATELINK
>
> **OVERLAPPING CIDRs**
> → PRIVATELINK CAN HELP
>
> **PROVIDER**
> → ENDPOINT SERVICE
>
> **PROVIDER LOAD BALANCER**
> → NLB
>
> **CONSUMER**
> → INTERFACE ENDPOINT
>
> **INTERFACE ENDPOINT**
> → ENI
>
> **FULL VPC NETWORK**
> → PEERING
>
> **MANY NETWORKS**
> → TRANSIT GATEWAY
>
> **GENERAL INTERNET**
> → NAT GATEWAY

---

## Master Memory Trick

> [!tip] PrivateLink Master Memory Trick
> Imagine two companies.
>
> Company A has:
>
> **A PRIVATE RESTAURANT**
>
> Company B wants:
>
> **ONLY THE FOOD**
>
> Company A does NOT want to hand Company B:
>
> **THE KEYS TO THE ENTIRE BUILDING**
>
> That's VPC Peering-style broad access.
>
> Instead, Company A builds:
>
> **A PRIVATE SERVICE WINDOW**
>
> Company B can order through:
>
> **THE WINDOW**
>
> but cannot walk around inside:
>
> **THE PROVIDER NETWORK**
>
> That window is:
>
> **PRIVATELINK**

So remember:

> **PRIVATE LINK**
> → ONE SERVICE
>
> **PROVIDER**
> → NLB + ENDPOINT SERVICE
>
> **CONSUMER**
> → INTERFACE ENDPOINT
>
> **CIDR OVERLAP**
> → OK FOR SERVICE MODEL
>
> **VPC PEERING**
> → FULL NETWORK CONNECTION
>
> **TRANSIT GATEWAY**
> → MANY NETWORKS

And the killer SAA question:

> **"Does the provider need to expose one private service to many consumer VPCs without giving them full network connectivity?"**
>
> YES
>
> → **PrivateLink**

---

## Related Notes

- [[VPC]]
- [[VPC Endpoints]]
- [[VPC Peering]]
- [[05-Networking/Transit Gateway]]
- [[Network Load Balancer]]
- [[Security Groups]]
- [[NAT Gateway]]