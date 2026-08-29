## What Problem Does It Solve?

[[Site-to-Site VPN]] provides:

**Encrypted connectivity between an on-premises network and AWS over the public Internet**

Architecture:

On-Premises Network  
↓  
Customer Gateway  
↓  
Encrypted VPN Tunnels  
↓  
AWS VPN Endpoint  
↓  
VPC / Transit Gateway

> [!tip] Memory Trick
> **Site-to-Site VPN = Encrypted Tunnel to AWS**

---

## Core Concept

Site-to-Site VPN is used for:

**Hybrid connectivity**

between:

- Corporate data centers
- Branch offices
- On-premises networks

and:

**AWS**

### Killer Exam Clue

> **Need encrypted connectivity from an on-premises network to AWS quickly over the Internet**
>
> → **Site-to-Site VPN**

---

# Hybrid Connectivity

Hybrid networking connects:

**On-Premises Infrastructure**

with:

**AWS**

Site-to-Site VPN provides that connectivity through:

**Encrypted IPsec tunnels**

### Memory Trick

**VPN = Hybrid Over Internet**

---

# IPsec

Site-to-Site VPN uses:

**IPsec**

to encrypt:

**Network traffic**

between AWS and:

**The customer network**

### Killer Exam Clue

> **Need encrypted network-level connectivity between on-premises and AWS**
>
> → **Site-to-Site VPN**

---

# Customer Gateway

A:

**Customer Gateway**

represents the customer side of:

**The VPN connection**

It commonly corresponds to:

- Router
- Firewall
- VPN appliance

in the on-premises environment.

### Memory Trick

**Customer Gateway = Your Side**

---

# AWS Side

The AWS side of the VPN can terminate on architectures using:

- Virtual Private Gateway
- [[Transit Gateway]]

depending on the design.

### Memory Trick

**Customer Gateway = On-Prem**

**AWS Gateway = AWS Side**

---

# Virtual Private Gateway

A:

**Virtual Private Gateway — VGW**

can act as the AWS-side endpoint for a VPN connection associated with:

**A VPC**

Architecture:

On-Prem  
↓  
VPN  
↓  
VGW  
↓  
VPC

### Killer Exam Clue

> **Single VPC needs Site-to-Site VPN connectivity**
>
> → **Virtual Private Gateway**

---

# Transit Gateway VPN

For larger environments:

On-Premises  
↓  
VPN  
↓  
[[Transit Gateway]]  
↓  
Multiple VPCs

This allows one central connectivity architecture to reach:

**Many VPCs**

### Killer Exam Clue

> **On-premises network needs VPN access to many VPCs**
>
> → **Site-to-Site VPN + Transit Gateway**

---

# Two VPN Tunnels

An AWS Site-to-Site VPN connection provides:

**Two VPN tunnels**

for:

**High availability**

Architecture:

On-Prem Router  
↓  
├── Tunnel 1
└── Tunnel 2  
↓  
AWS

### Killer Exam Fact

> **AWS Site-to-Site VPN provides two tunnels for redundancy**

### Memory Trick

**VPN = Always Think Two Tunnels**

---

# Why Two Tunnels?

If one tunnel becomes:

**Unavailable**

traffic can fail over to:

**The other tunnel**

For resilient architecture:

Configure the customer gateway to use:

**Both tunnels**

---

# High Availability

A VPN connection is only as resilient as:

**Both sides of the architecture**

For stronger on-premises resilience, organizations may use:

**Multiple customer gateway devices**

rather than depending on:

**One physical router**

---

# Static Routing

Site-to-Site VPN can use:

**Static Routes**

where routes are manually configured.

Think:

**Simple but manually maintained**

---

# Dynamic Routing

VPN connections can use:

**BGP — Border Gateway Protocol**

for dynamic route exchange.

### Killer Exam Clue

> **Need AWS and on-premises networks to dynamically exchange routes**
>
> → **BGP**

### Memory Trick

**BGP = Routers Tell Each Other the Routes**

---

# BGP

BGP can advertise:

**Available network prefixes**

between:

AWS  
↔  
Customer network

This can simplify routing when:

**Networks change**

---

# Static vs Dynamic Routing

## Static

Think:

- Manual routes
- Simpler
- Less dynamic

## BGP

Think:

- Dynamic route advertisement
- Automatic route updates
- Better for changing networks

### Killer Shortcut

**Dynamic hybrid routing**
→ BGP

---

# Route Propagation

AWS routing can use:

**Route propagation**

to automatically add routes learned from:

**VPN connections**

into supported:

**Route tables**

### Memory Trick

**Propagation = Learned Routes Appear Automatically**

---

# Site-to-Site VPN Uses Internet

This is an important distinction.

VPN traffic travels through:

**The public Internet**

but is:

**Encrypted**

### Memory Trick

**Public Path**

**Private Encryption**

---

# VPN vs Direct Connect

This is one of the biggest hybrid-networking comparisons.

## Site-to-Site VPN

Think:

- Internet-based
- Encrypted
- Faster to establish
- Lower setup complexity
- Variable Internet performance

## [[05-Networking/Direct Connect]]

Think:

- Dedicated private connection
- More predictable bandwidth
- More consistent performance
- Longer provisioning time

### Killer Shortcut

**Need connectivity quickly**
→ VPN

**Need dedicated predictable connectivity**
→ Direct Connect

---

# VPN Can Be Faster to Deploy

Direct Connect can require:

**Physical provisioning**

Site-to-Site VPN can usually be established:

**Much faster**

### Killer Exam Clue

> **Company needs hybrid connectivity immediately while waiting for Direct Connect**
>
> → **Site-to-Site VPN**

---

# VPN as Direct Connect Backup

A common resilient architecture:

On-Premises  
↓  
Primary: Direct Connect  
↓  
AWS

Backup:

On-Premises  
↓  
Site-to-Site VPN  
↓  
AWS

### Killer Exam Clue

> **Need backup connectivity if Direct Connect fails**
>
> → **Site-to-Site VPN**

---

# Direct Connect Does Not Encrypt by Default

Direct Connect provides:

**Private connectivity**

but does not inherently provide:

**IPsec encryption**

If encryption is required:

A VPN can be layered over supported Direct Connect architectures.

### Killer Exam Clue

> **Need dedicated connection AND IPsec encryption**
>
> → **VPN over Direct Connect**

---

# VPN vs Client VPN

Do not confuse:

Site-to-Site VPN

with:

**Client VPN**

## Site-to-Site VPN

Connects:

**Networks**

## Client VPN

Connects:

**Individual users/devices**

### Memory Trick

**Site-to-Site = Network-to-Network**

**Client VPN = User-to-Network**

---

# VPN vs VPC Peering

## [[VPC Peering]]

Connects:

**VPC to VPC**

## Site-to-Site VPN

Connects:

**On-premises network to AWS**

### Killer Shortcut

VPC ↔ VPC  
→ Peering

Office ↔ AWS  
→ Site-to-Site VPN

---

# VPN vs Transit Gateway

These are complementary.

## Site-to-Site VPN

Provides:

**Encrypted hybrid tunnel**

## [[Transit Gateway]]

Provides:

**Central routing hub**

Architecture:

On-Prem  
↓  
VPN  
↓  
Transit Gateway  
↓  
VPCs

### Memory Trick

**VPN = Tunnel**

**TGW = Hub**

---

# VPN vs PrivateLink

## [[PrivateLink]]

Think:

**Private access to one service**

## Site-to-Site VPN

Think:

**Network connectivity between on-premises and AWS**

---

# VPN Performance

Because Site-to-Site VPN travels over:

**The Internet**

performance can be affected by:

- Internet congestion
- Network path
- Latency variability

For very predictable performance:

Think:

**Direct Connect**

---

# Accelerated Site-to-Site VPN

AWS supports:

**Accelerated Site-to-Site VPN**

using:

**Global Accelerator**

for supported configurations.

This can improve:

**Network path performance**

by using the AWS global network sooner.

### Killer Exam Clue

> **Need improved VPN performance over long distances using AWS global networking**
>
> → **Accelerated Site-to-Site VPN**

---

# VPN Monitoring

VPN connections can be monitored using:

[[CloudWatch]]

for metrics related to:

- Tunnel status
- Traffic
- Availability

### Killer Exam Clue

> **Need an alarm when a VPN tunnel goes down**
>
> → **CloudWatch**

---

# Tunnel Status

Because there are:

**Two tunnels**

monitor both.

A resilient environment should not ignore:

**A failed secondary tunnel**

just because traffic still works.

### Exam Principle

> **Redundancy only helps if you monitor it**

---

# Security

Site-to-Site VPN provides:

**Encryption in transit**

through:

**IPsec**

This protects network traffic traversing:

**The public Internet**

---

# CIDR Planning

Connected networks should use:

**Non-overlapping CIDR ranges**

for straightforward routing.

Example:

AWS VPC:

`10.0.0.0/16`

On-Premises:

`172.16.0.0/16`

### Killer Exam Principle

> **Overlapping IP ranges complicate hybrid routing**

---

# Architecture Thinking

## Scenario 1 — Quick Hybrid Connection

Company needs:

**On-premises to AWS connectivity this week**

Choose:

**Site-to-Site VPN**

---

## Scenario 2 — Dedicated Connection

Company requires:

- Predictable bandwidth
- Consistent performance
- Dedicated private connectivity

Choose:

**Direct Connect**

---

## Scenario 3 — Encrypted Direct Connect

Company requires:

- Direct Connect
- IPsec encryption

Choose:

**VPN over Direct Connect**

---

## Scenario 4 — Direct Connect Backup

Direct Connect is primary.

Need:

**Backup hybrid path**

Choose:

**Site-to-Site VPN**

---

## Scenario 5 — One VPC

On-premises network needs access to:

**One VPC**

Choose:

Site-to-Site VPN  
↓  
Virtual Private Gateway

---

## Scenario 6 — Many VPCs

On-premises network needs access to:

**50 VPCs**

Choose:

Site-to-Site VPN  
↓  
Transit Gateway  
↓  
VPCs

---

## Scenario 7 — Dynamic Routes

On-premises routes frequently change.

Need automatic exchange.

Choose:

**BGP**

---

## Scenario 8 — Remote Employees

Individual employees need:

**Secure remote access into AWS**

Do NOT choose Site-to-Site VPN.

Think:

**Client VPN**

---

## Scenario 9 — Tunnel Failure

One VPN tunnel fails.

Application should continue using:

**Second tunnel**

assuming customer equipment is:

**Correctly configured**

---

# Scenario Recognition

Immediately think:

**Site-to-Site VPN**

when you see:

- On-premises to AWS
- IPsec
- Encrypted tunnel
- Customer Gateway
- Virtual Private Gateway
- Two VPN tunnels
- Quick hybrid connectivity
- Direct Connect backup
- BGP

---

## Think Direct Connect When You See

- Dedicated physical connection
- Consistent performance
- Predictable bandwidth
- Long-term hybrid connectivity

---

## Think Client VPN When You See

- Remote employees
- Individual clients
- User-to-VPC access

---

## Think Transit Gateway When You See

- Many VPCs
- Central hybrid routing
- Hub-and-spoke networking

---

# Exam Traps

## Trap 1 — Site-to-Site VPN Uses a Dedicated Private Circuit

❌

That is:

**Direct Connect**

Site-to-Site VPN normally uses:

**The Internet**

---

## Trap 2 — VPN Traffic Is Unencrypted Because It Uses the Internet

❌

It uses:

**IPsec encryption**

---

## Trap 3 — AWS Provides Only One VPN Tunnel

❌

A Site-to-Site VPN connection provides:

**Two tunnels**

---

## Trap 4 — Site-to-Site VPN Is for Individual Remote Users

❌

Think:

**Client VPN**

---

## Trap 5 — Transit Gateway Encrypts the On-Prem Connection

❌

Transit Gateway:

**Routes**

VPN:

**Encrypts the tunnel**

---

## Trap 6 — Direct Connect Is Always Encrypted by Default

❌

Direct Connect itself does not inherently provide:

**IPsec encryption**

---

## Trap 7 — Static Routes Are Required

❌

Dynamic routing can use:

**BGP**

---

# Quick Cheat Sheet

| Exam Clue | Answer |
|---|---|
| On-Prem → AWS Over Internet | Site-to-Site VPN |
| Encryption | IPsec |
| Customer Side | Customer Gateway |
| AWS Side for VPC | Virtual Private Gateway |
| AWS Hub for Many VPCs | Transit Gateway |
| Redundancy | Two VPN Tunnels |
| Dynamic Routing | BGP |
| Quick Hybrid Connectivity | Site-to-Site VPN |
| Dedicated Connection | Direct Connect |
| Direct Connect Backup | Site-to-Site VPN |
| Individual Remote Users | Client VPN |
| VPN Monitoring | CloudWatch |

---

# Hybrid Connectivity Decision Map

Need:

**Fast encrypted hybrid connectivity**

→ Site-to-Site VPN

Need:

**Dedicated private connection**

→ Direct Connect

Need:

**Dedicated + encrypted**

→ VPN over Direct Connect

Need:

**VPN to many VPCs**

→ VPN + Transit Gateway

Need:

**Individual user access**

→ Client VPN

Need:

**Direct Connect backup**

→ Site-to-Site VPN

---

# Final Exam Rapid-Fire

> **ON-PREM → AWS**
> → SITE-TO-SITE VPN
>
> **ENCRYPTION**
> → IPSEC
>
> **CUSTOMER SIDE**
> → CUSTOMER GATEWAY
>
> **AWS VPC SIDE**
> → VIRTUAL PRIVATE GATEWAY
>
> **TWO TUNNELS**
> → HIGH AVAILABILITY
>
> **DYNAMIC ROUTING**
> → BGP
>
> **QUICK HYBRID CONNECTION**
> → VPN
>
> **DEDICATED CONNECTION**
> → DIRECT CONNECT
>
> **DX BACKUP**
> → VPN
>
> **MANY VPCs**
> → VPN + TRANSIT GATEWAY
>
> **REMOTE USER**
> → CLIENT VPN
>
> **TUNNEL MONITORING**
> → CLOUDWATCH

---

## Master Memory Trick

> [!tip] Site-to-Site VPN Master Memory Trick
> Imagine your company's data center and AWS are:
>
> **TWO BUILDINGS**
>
> between them is:
>
> **THE PUBLIC INTERNET**
>
> Instead of sending your data openly across the street, you build:
>
> **AN ARMORED TUNNEL**
>
> That's:
>
> **IPSEC VPN**
>
> Your building entrance is:
>
> **CUSTOMER GATEWAY**
>
> AWS's entrance is:
>
> **VIRTUAL PRIVATE GATEWAY**
>
> or:
>
> **TRANSIT GATEWAY**
>
> And AWS gives you:
>
> **TWO TUNNELS**
>
> so one can survive if:
>
> **THE OTHER FAILS**

So remember:

> **SITE-TO-SITE VPN**
> → ENCRYPTED INTERNET TUNNEL
>
> **CUSTOMER GATEWAY**
> → YOUR SIDE
>
> **VGW / TGW**
> → AWS SIDE
>
> **TWO TUNNELS**
> → REDUNDANCY
>
> **BGP**
> → DYNAMIC ROUTING
>
> **DIRECT CONNECT**
> → DEDICATED CONNECTION

And the killer SAA question:

> **"Does the company need encrypted network connectivity between its on-premises environment and AWS without waiting for a dedicated circuit?"**
>
> YES
>
> → **Site-to-Site VPN**

---

## Related Notes

- [[VPC]]
- [[Transit Gateway]]
- [[05-Networking/Direct Connect]]
- [[VPC Peering]]
- [[CloudWatch]]