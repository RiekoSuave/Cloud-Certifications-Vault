## What Problem Does It Solve?

[[Direct Connect]] provides:

**Dedicated private network connectivity between on-premises environments and AWS**

It is designed for workloads that need:

- More consistent network performance
- Predictable bandwidth
- Dedicated private connectivity
- Reduced reliance on the public Internet
- Large or sustained data transfers

Architecture:

On-Premises  
↓  
Direct Connect Connection  
↓  
AWS Direct Connect Location  
↓  
AWS Network  
↓  
VPC / AWS Services

> [!tip] Memory Trick
> **Direct Connect = Dedicated Private Connection to AWS**

---

## Core Concept

Direct Connect creates:

**A dedicated network connection**

between:

**Your network**

and:

**AWS**

Unlike Site-to-Site VPN, it does not primarily rely on:

**The public Internet**

### Killer Exam Clue

> **Need dedicated, predictable hybrid connectivity between on-premises and AWS**
>
> → **Direct Connect**

---

# Dedicated Connectivity

Direct Connect is useful when:

**Internet-based connectivity is not sufficient**

because the workload needs:

- Consistent throughput
- Lower network variability
- Large data transfer capability
- Private hybrid networking

### Memory Trick

**VPN = Internet Tunnel**

**Direct Connect = Dedicated Line**

---

# Direct Connect Location

A Direct Connect connection terminates at:

**A Direct Connect location**

This is a physical location where:

**Customer or partner networking equipment connects to AWS**

### Exam Principle

> **Direct Connect requires physical network provisioning**

---

# Physical Connection

Direct Connect is different from most AWS networking services because it may involve:

**Physical circuits and networking providers**

This means provisioning generally takes:

**Longer than a VPN**

### Killer Exam Clue

> **Need hybrid connectivity immediately**
>
> → Site-to-Site VPN
>
> **Need dedicated long-term connectivity**
>
> → Direct Connect

---

# Dedicated Connection

A:

**Dedicated Connection**

provides a physical Ethernet connection dedicated to:

**One customer**

It offers supported bandwidth options depending on:

**Direct Connect capabilities**

### Memory Trick

**Dedicated Connection = Your Physical Port**

---

# Hosted Connection

A:

**Hosted Connection**

is provided through an:

**AWS Direct Connect Partner**

This can provide more flexible:

**Bandwidth options**

without requiring the customer to directly provision a full dedicated port.

### Killer Exam Concept

> **Direct Connect Partner**
>
> → Hosted Connection

---

# Virtual Interfaces

Direct Connect uses:

**Virtual Interfaces — VIFs**

to access:

**Different types of AWS resources**

The important types for SAA include:

- Private VIF
- Public VIF
- Transit VIF

### Memory Trick

**Physical Connection = Road**

**VIF = Which AWS Destination the Road Reaches**

---

# Private Virtual Interface

A:

**Private VIF**

provides private access to:

**VPC resources**

typically through:

**Virtual Private Gateway or Direct Connect Gateway architectures**

### Killer Exam Clue

> **Need Direct Connect access to private VPC resources**
>
> → **Private VIF**

---

# Public Virtual Interface

A:

**Public VIF**

provides access to:

**AWS public service endpoints**

using AWS public IP ranges.

Examples can include:

- S3 public endpoint
- Other AWS public services

### Important Distinction

Public VIF traffic uses:

**Dedicated Direct Connect connectivity**

rather than normal Internet routing.

---

# Transit Virtual Interface

A:

**Transit VIF**

provides connectivity to:

**Transit Gateway**

through:

**Direct Connect Gateway**

Architecture:

On-Premises  
↓  
Direct Connect  
↓  
Transit VIF  
↓  
Direct Connect Gateway  
↓  
[[Transit Gateway]]  
↓  
Multiple VPCs

### Killer Exam Clue

> **Need Direct Connect connectivity to many VPCs through Transit Gateway**
>
> → **Transit VIF + Direct Connect Gateway**

---

# Direct Connect Gateway

A:

**Direct Connect Gateway**

helps connect Direct Connect to:

**Multiple VPCs or Transit Gateway architectures**

without tying the connection to:

**One single VPC**

### Memory Trick

**DX Gateway = Bridge Between Direct Connect and AWS Networks**

---

# Direct Connect + Transit Gateway

A common large-scale hybrid architecture:

On-Premises  
↓  
Direct Connect  
↓  
Direct Connect Gateway  
↓  
Transit Gateway  
↓  
Multiple VPCs

### Killer Exam Clue

> **Need dedicated on-premises connectivity to many VPCs**
>
> → **Direct Connect + Direct Connect Gateway + Transit Gateway**

---

# Direct Connect + Virtual Private Gateway

For simpler architectures:

On-Premises  
↓  
Direct Connect  
↓  
Private VIF  
↓  
Virtual Private Gateway  
↓  
VPC

This is useful when:

**One or a smaller number of VPCs**

need dedicated connectivity.

---

# BGP

Direct Connect uses:

**BGP — Border Gateway Protocol**

for dynamic route exchange.

BGP helps advertise:

**Network prefixes**

between:

On-premises  
↔  
AWS

### Killer Exam Clue

> **Dynamic route exchange over Direct Connect**
>
> → **BGP**

### Memory Trick

**Direct Connect + Routes = BGP**

---

# Direct Connect Does Not Encrypt by Default

This is one of the most important exam facts.

Direct Connect provides:

**Private connectivity**

but not necessarily:

**Encryption in transit by default**

### Killer Exam Trap

> **Private does NOT automatically mean encrypted**

If encryption is required:

Think about:

**VPN over Direct Connect**

or supported encrypted DX options where applicable.

---

# VPN Over Direct Connect

Architecture:

On-Premises  
↓  
Direct Connect  
↓  
IPsec VPN  
↓  
AWS

This provides:

- Dedicated connectivity
- IPsec encryption

### Killer Exam Clue

> **Need both dedicated hybrid connectivity and IPsec encryption**
>
> → **VPN over Direct Connect**

---

# MACsec

Direct Connect supports:

**MACsec**

for supported dedicated connections and locations.

This can provide:

**Layer 2 encryption**

between supported Direct Connect endpoints.

### Exam Principle

> **When the question explicitly mentions MACsec, think Direct Connect**

---

# Direct Connect vs Site-to-Site VPN

This comparison is critical.

## [[Site-to-Site VPN]]

Think:

- Public Internet
- IPsec encrypted
- Quick to deploy
- Variable Internet performance

## Direct Connect

Think:

- Dedicated connection
- More predictable performance
- More consistent bandwidth
- Longer provisioning time

### Killer Shortcut

**Quick + Encrypted**
→ VPN

**Dedicated + Predictable**
→ Direct Connect

---

# Direct Connect Is Not Automatically Highly Available

A single Direct Connect connection can become:

**A single point of failure**

For resilient architecture, use:

**Redundant connections**

### Killer Exam Clue

> **Need highly available Direct Connect**
>
> → **Multiple DX connections in resilient locations**

---

# High Availability Design

Possible resilient design:

On-Premises  
↓  
├── Direct Connect Connection A
└── Direct Connect Connection B  
↓  
AWS

Connections should ideally terminate through:

**Separate devices and/or locations**

depending on availability requirements.

### Memory Trick

**One DX = One Risk**

**Two DX = Resilience**

---

# Maximum Resiliency

For critical workloads:

Use:

**Multiple Direct Connect connections**

across:

**Multiple Direct Connect locations**

This protects against:

- Device failure
- Connection failure
- Location failure

### SAA Principle

> **Redundancy should eliminate shared failure points**

---

# VPN Backup

A very common exam architecture:

Primary:

**Direct Connect**

Backup:

**Site-to-Site VPN**

Architecture:

On-Premises  
↓  
Direct Connect  
↓  
AWS

If DX fails:

On-Premises  
↓  
VPN  
↓  
AWS

### Killer Exam Clue

> **Need backup connectivity while using Direct Connect**
>
> → **Site-to-Site VPN**

---

# Temporary VPN During Provisioning

Because Direct Connect can take:

**Time to provision**

a company may use:

**Site-to-Site VPN temporarily**

then switch to:

**Direct Connect**

when ready.

### Killer Exam Pattern

> **Need hybrid connectivity now, but Direct Connect is being provisioned**
>
> → **Use VPN first**

---

# Bandwidth and Performance

Direct Connect can provide:

**More consistent network performance**

because traffic avoids normal:

**Public Internet paths**

This is useful for:

- Large database replication
- Hybrid workloads
- Large file transfers
- Steady data movement

---

# Cost Considerations

Direct Connect can reduce costs for:

**Large sustained data transfers**

in some architectures compared with:

**Internet-based transfer**

But it introduces:

- Port charges
- Partner/provider costs
- Circuit costs
- Operational complexity

### Exam Principle

> **Choose DX for architecture requirements, not merely because it sounds faster**

---

# Direct Connect vs Internet Gateway

## Internet Gateway

Provides:

**Public Internet connectivity**

## Direct Connect

Provides:

**Dedicated hybrid connectivity**

These solve:

**Different networking problems**

---

# Direct Connect vs Transit Gateway

## [[Transit Gateway]]

Think:

**Central routing hub**

## Direct Connect

Think:

**Dedicated on-premises connection**

They are often used:

**Together**

### Memory Trick

**DX = Get Into AWS**

**TGW = Get Around AWS**

---

# Direct Connect vs VPC Peering

## [[VPC Peering]]

Think:

**VPC-to-VPC private connectivity**

## Direct Connect

Think:

**On-premises-to-AWS dedicated connectivity**

---

# Direct Connect vs PrivateLink

## [[PrivateLink]]

Think:

**Private service access**

## Direct Connect

Think:

**Hybrid network connectivity**

### Killer Shortcut

On-prem network  
→ AWS  
→ Direct Connect

Consumer VPC  
→ One private service  
→ PrivateLink

---

# Direct Connect and S3

Direct Connect can access AWS services through:

**Appropriate VIF architecture**

If private subnet workloads only need S3 within AWS:

A:

**Gateway VPC Endpoint**

may be simpler.

### Exam Principle

> **Do not over-engineer with Direct Connect when the requirement is only private VPC-to-S3 access**

---

# Direct Connect and DNS

Hybrid architectures may also require:

**DNS resolution between on-premises and AWS**

This can involve:

**Route 53 Resolver endpoints**

Direct Connect itself provides:

**Network connectivity**

not:

**Complete hybrid DNS configuration**

---

# Architecture Thinking

## Scenario 1 — Predictable Hybrid Connectivity

Company transfers:

Large datasets continuously

between:

On-premises and AWS

and wants:

**Consistent network performance**

Choose:

**Direct Connect**

---

## Scenario 2 — Immediate Connectivity

Company needs:

Hybrid connectivity tomorrow.

Direct Connect will take too long.

Choose:

**Site-to-Site VPN**

---

## Scenario 3 — Encryption Required

Company has Direct Connect but requires:

**IPsec encryption**

Choose:

**VPN over Direct Connect**

---

## Scenario 4 — One VPC

On-premises needs dedicated connectivity to:

**One VPC**

Think:

Private VIF  
↓  
Virtual Private Gateway

---

## Scenario 5 — Many VPCs

On-premises needs dedicated connectivity to:

**50 VPCs**

Choose:

Direct Connect  
↓  
Direct Connect Gateway  
↓  
Transit Gateway

---

## Scenario 6 — High Availability

Company cannot tolerate:

**Direct Connect connection failure**

Choose:

**Redundant Direct Connect connections**

plus potentially:

**VPN backup**

---

## Scenario 7 — Public AWS Services

On-premises needs dedicated connectivity to:

**AWS public endpoints**

Think:

**Public VIF**

---

## Scenario 8 — Private VPC Resources

On-premises needs access to:

**Private EC2 addresses**

Think:

**Private VIF**

---

## Scenario 9 — Transit Gateway

Need connectivity into:

**Transit Gateway**

Think:

**Transit VIF**

---

# Scenario Recognition

Immediately think:

**Direct Connect**

when you see:

- Dedicated connection
- Predictable hybrid bandwidth
- Consistent performance
- Private on-premises connectivity
- Direct Connect location
- Private VIF
- Public VIF
- Transit VIF
- Direct Connect Gateway

---

## Think Site-to-Site VPN When You See

- Quick setup
- IPsec
- Internet-based hybrid connectivity
- Backup connection

---

## Think Transit Gateway When You See

- Many VPCs
- Central routing hub
- Hub-and-spoke connectivity

---

# Exam Traps

## Trap 1 — Direct Connect Is Encrypted by Default

❌

It provides:

**Private connectivity**

but not necessarily:

**Encryption by default**

---

## Trap 2 — Direct Connect Is Faster to Provision Than VPN

❌

Physical provisioning usually takes:

**Longer**

---

## Trap 3 — One Direct Connect Connection Is Fully Redundant

❌

Use:

**Multiple connections**

for high availability.

---

## Trap 4 — Public VIF Means Traffic Uses the Public Internet

❌

It accesses:

**AWS public endpoints through Direct Connect**

---

## Trap 5 — Direct Connect Gateway Is the Same as Transit Gateway

❌

DX Gateway helps connect:

**Direct Connect to AWS network targets**

Transit Gateway:

**Routes among networks**

---

## Trap 6 — Direct Connect Replaces VPN in Every Architecture

❌

VPN is still useful for:

- Encryption
- Backup
- Rapid deployment

---

## Trap 7 — Direct Connect Is Needed for Private S3 Access From an EC2 Instance

❌

Within a VPC, consider:

**S3 Gateway Endpoint**

---

# Quick Cheat Sheet

| Exam Clue | Answer |
|---|---|
| Dedicated Hybrid Connectivity | Direct Connect |
| Predictable Network Performance | Direct Connect |
| Dynamic Routing | BGP |
| Private VPC Access | Private VIF |
| AWS Public Endpoint Access | Public VIF |
| Transit Gateway Access | Transit VIF |
| Connect DX to Many Networks | Direct Connect Gateway |
| Encryption by Default | ❌ |
| Dedicated + IPsec | VPN over Direct Connect |
| Quick Hybrid Setup | Site-to-Site VPN |
| DX Backup | Site-to-Site VPN |
| High Availability | Redundant DX Connections |

---

# Hybrid Connectivity Decision Map

Need:

**Quick encrypted connection**

→ Site-to-Site VPN

Need:

**Dedicated predictable connection**

→ Direct Connect

Need:

**Dedicated + encrypted**

→ VPN over Direct Connect

Need:

**DX to one private VPC**

→ Private VIF

Need:

**DX to AWS public endpoints**

→ Public VIF

Need:

**DX to Transit Gateway**

→ Transit VIF

Need:

**DX to many VPCs**

→ DX Gateway + Transit Gateway

Need:

**DX backup**

→ Site-to-Site VPN

---

# VIF Decision Map

> **PRIVATE VIF**
> → PRIVATE VPC RESOURCES
>
> **PUBLIC VIF**
> → AWS PUBLIC ENDPOINTS
>
> **TRANSIT VIF**
> → TRANSIT GATEWAY

### Memory Trick

**Private = VPC**

**Public = AWS Public Services**

**Transit = TGW**

---

# Final Exam Rapid-Fire

> **DEDICATED HYBRID CONNECTION**
> → DIRECT CONNECT
>
> **PREDICTABLE BANDWIDTH**
> → DIRECT CONNECT
>
> **DYNAMIC ROUTES**
> → BGP
>
> **PRIVATE VPC ACCESS**
> → PRIVATE VIF
>
> **AWS PUBLIC ENDPOINT**
> → PUBLIC VIF
>
> **TRANSIT GATEWAY**
> → TRANSIT VIF
>
> **MANY VPCs**
> → DX GATEWAY + TGW
>
> **ENCRYPTION BY DEFAULT**
> → NO
>
> **DEDICATED + IPSEC**
> → VPN OVER DX
>
> **FAST SETUP**
> → SITE-TO-SITE VPN
>
> **DX BACKUP**
> → VPN
>
> **HIGH AVAILABILITY**
> → REDUNDANT DX CONNECTIONS

---

## Master Memory Trick

> [!tip] Direct Connect Master Memory Trick
> Imagine your company has:
>
> **A private office**
>
> and AWS has:
>
> **A huge data center**
>
> Site-to-Site VPN gives you:
>
> **AN ARMORED CAR DRIVING ON THE PUBLIC HIGHWAY**
>
> The cargo is encrypted,
>
> but you're still using:
>
> **THE INTERNET**
>
> Direct Connect builds:
>
> **A PRIVATE ROAD DIRECTLY TO AWS**
>
> Traffic does not depend on:
>
> **THE PUBLIC INTERNET PATH**
>
> But here's the catch:
>
> The private road is not automatically:
>
> **AN ENCRYPTED TUNNEL**
>
> If you need both:
>
> **PRIVATE ROAD + ENCRYPTION**
>
> combine:
>
> **DIRECT CONNECT + VPN**

So remember:

> **VPN**
> → QUICK + ENCRYPTED
>
> **DIRECT CONNECT**
> → DEDICATED + PREDICTABLE
>
> **BGP**
> → ROUTES
>
> **PRIVATE VIF**
> → VPC
>
> **PUBLIC VIF**
> → AWS PUBLIC SERVICES
>
> **TRANSIT VIF**
> → TGW
>
> **DX GATEWAY**
> → CONNECT DX TO NETWORKS
>
> **REDUNDANT DX**
> → HIGH AVAILABILITY

And the killer SAA question:

> **"Does the company need a dedicated, more predictable network connection between its on-premises environment and AWS?"**
>
> YES
>
> → **Direct Connect**

---

## Related Notes

- [[VPC]]
- [[Site-to-Site VPN]]
- [[Transit Gateway]]
- [[VPC Peering]]
- [[PrivateLink]]
- [[VPC Endpoints]]