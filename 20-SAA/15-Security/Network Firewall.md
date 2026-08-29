## What Problem Does It Solve?

[[20-SAA/15-Security/Network Firewall]] provides:

**Managed network traffic filtering and inspection for VPCs**

It can inspect traffic entering, leaving, or moving through your network based on:

- IP addresses
- Ports
- Protocols
- Domains
- Stateful rules
- Stateless rules
- Traffic patterns

Architecture:

Traffic  
↓  
Network Firewall  
↓  
Inspect Against Rules  
↓  
Allow / Drop / Alert  
↓  
Destination

> [!tip] Memory Trick
> **Network Firewall = VPC Traffic Inspector**

---

## Core Concept

Network Firewall protects:

**VPC network traffic**

It provides more advanced inspection capabilities than basic controls such as:

- Security Groups
- NACLs

### Killer Exam Clue

> **Need a managed stateful firewall to inspect and filter VPC network traffic**
>
> → **Network Firewall**

---

# Where Does It Operate?

Network Firewall is deployed inside:

**A VPC**

using:

**Firewall endpoints**

Traffic must be routed through these endpoints for:

**Inspection**

Architecture:

Source  
↓  
Route Table  
↓  
Firewall Endpoint  
↓  
Network Firewall  
↓  
Destination

### Killer Exam Principle

> **Traffic must be routed through the firewall endpoint to be inspected**

---

# Firewall Endpoints

Network Firewall creates:

**Firewall endpoints**

in designated subnets.

These endpoints act as:

**Traffic inspection points**

### Memory Trick

**Route to Endpoint → Inspect Traffic**

---

# Dedicated Firewall Subnets

A common architecture uses:

**Dedicated firewall subnets**

Architecture:

Internet Gateway  
↓  
Firewall Subnet  
↓  
Network Firewall Endpoint  
↓  
Application Subnet

This helps create:

**Centralized inspection paths**

---

# Stateless Inspection

Network Firewall supports:

**Stateless rules**

These inspect each packet:

**Independently**

without maintaining:

**Connection state**

Rules can evaluate information such as:

- Source IP
- Destination IP
- Source port
- Destination port
- Protocol

### Memory Trick

**Stateless = Packet by Packet**

---

# Stateful Inspection

Network Firewall also supports:

**Stateful rules**

These understand:

**Connection context**

and can inspect traffic based on:

**The state of the network session**

### Killer Exam Clue

> **Need connection-aware VPC traffic inspection**
>
> → **Network Firewall Stateful Rules**

### Memory Trick

**Stateful = Remembers the Conversation**

---

# Stateless vs Stateful

| Feature | Stateless | Stateful |
|---|---|---|
| Tracks Connection | ❌ | ✅ |
| Evaluates Packets Independently | ✅ | ❌ |
| Connection Context | ❌ | ✅ |
| Advanced Traffic Inspection | Limited | ✅ |

---

# Firewall Policy

A:

**Firewall Policy**

defines how Network Firewall processes:

**Traffic**

It can reference:

- Stateless rule groups
- Stateful rule groups
- Default actions

### Memory Trick

**Firewall Policy = How the Firewall Behaves**

---

# Rule Groups

Rules can be organized into:

**Rule Groups**

These provide reusable collections of:

**Traffic-inspection rules**

Architecture:

Firewall  
↓  
Firewall Policy  
↓  
Rule Groups  
↓  
Rules

---

# Stateful Rule Groups

Stateful rules can inspect:

- Network sessions
- Protocol behavior
- Domain information
- Traffic patterns

This provides:

**Deeper inspection**

than simple packet filtering.

---

# Domain Filtering

Network Firewall can filter traffic based on:

**Domain names**

Example:

EC2  
↓  
Outbound Request  
↓  
Network Firewall  
↓  
Blocked Malicious Domain

### Killer Exam Clue

> **Prevent VPC workloads from connecting to known malicious domains**
>
> → **Network Firewall**

---

# IP Filtering

Network Firewall can allow or deny traffic based on:

**IP addresses and CIDR ranges**

Example:

Known Malicious CIDR  
↓  
Network Firewall  
↓  
DROP

---

# Port and Protocol Filtering

Rules can inspect:

- TCP
- UDP
- Ports
- IP protocols

This makes Network Firewall useful for:

**Centralized network security policies**

---

# Intrusion Prevention

Network Firewall supports:

**Intrusion prevention capabilities**

through advanced stateful inspection.

It can identify and block:

**Known malicious network patterns**

### Killer Exam Clue

> **Need managed intrusion prevention for VPC traffic**
>
> → **Network Firewall**

---

# Suricata-Compatible Rules

Network Firewall supports:

**Suricata-compatible stateful rules**

This allows advanced rules for:

- Protocol inspection
- Traffic signatures
- Intrusion detection
- Intrusion prevention

### Exam Recognition

> **Suricata rules**
>
> → **Network Firewall**

---

# Ingress Inspection

Network Firewall can inspect:

**Traffic entering a VPC**

Example:

Internet  
↓  
Internet Gateway  
↓  
Network Firewall  
↓  
Application

### Memory Trick

**Ingress = Coming In**

---

# Egress Inspection

Network Firewall can inspect:

**Traffic leaving a VPC**

Example:

Private EC2  
↓  
Network Firewall  
↓  
NAT Gateway / Internet  
↓  
External Destination

This is useful for:

- Domain restrictions
- Malicious destination blocking
- Egress security policies

### Killer Exam Clue

> **Centrally restrict which external destinations VPC workloads can access**
>
> → **Network Firewall**

---

# East-West Traffic

Network Firewall can also be used in architectures that inspect:

**Traffic between network segments**

This is sometimes called:

**East-West traffic**

Example:

VPC A  
↓  
Inspection  
↓  
VPC B

### Memory Trick

**North-South = In/Out**

**East-West = Between Networks**

---

# Centralized Inspection

Large organizations may create:

**A centralized inspection VPC**

Architecture:

Spoke VPCs  
↓  
[[05-Networking/Transit Gateway]]  
↓  
Inspection VPC  
↓  
Network Firewall  
↓  
Destination

### Killer Exam Clue

> **Need centralized network inspection for many VPCs**
>
> → **Transit Gateway + Network Firewall**

---

# Network Firewall + Transit Gateway

[[05-Networking/Transit Gateway]] provides:

**Centralized VPC connectivity**

Network Firewall provides:

**Centralized traffic inspection**

Together:

Spoke VPC A  
↓  
Transit Gateway  
↓  
Inspection VPC  
↓  
Network Firewall  
↓  
Transit Gateway  
↓  
Spoke VPC B

### Memory Trick

**Transit Gateway = Connect**

**Network Firewall = Inspect**

---

# High Availability

Network Firewall is designed as:

**A managed highly available service**

For resilient architecture, firewall endpoints are deployed appropriately across:

**Availability Zones**

### SAA Principle

> **Design routing so each AZ can use an appropriate firewall endpoint**

---

# Symmetric Routing

Stateful firewalls require careful:

**Symmetric routing**

Traffic for a connection should flow through:

**The same firewall path**

for both directions.

### Killer Exam Clue

> **Stateful firewall traffic behaves unexpectedly because return traffic follows another path**
>
> → Check **symmetric routing**

### Memory Trick

**Same Conversation → Same Firewall Path**

---

# Network Firewall Logging

Network Firewall can generate logs for:

- Alerts
- Network traffic
- Rule matches

These can be sent to supported:

**Logging destinations**

for investigation and monitoring.

---

# CloudWatch Integration

Network Firewall integrates with:

[[CloudWatch]]

for:

- Metrics
- Monitoring
- Operational visibility

### Memory Trick

**Firewall Filters**

**CloudWatch Monitors**

---

# Network Firewall vs Security Groups

This is an important comparison.

## Security Groups

Think:

**Resource-level network access**

Characteristics:

- Stateful
- Attached to resources/ENIs
- Allow rules
- Basic port/protocol/source control

## Network Firewall

Think:

**Centralized advanced network inspection**

Characteristics:

- Stateful + stateless inspection
- Advanced rules
- Domain filtering
- Intrusion prevention
- Centralized routing architecture

### Killer Shortcut

**Can EC2 receive traffic on port 443?**
→ Security Group

**Inspect VPC traffic for malicious patterns**
→ Network Firewall

---

# Network Firewall vs NACL

## NACL

Think:

**Subnet-level packet filtering**

Characteristics:

- Stateless
- Allow + deny rules
- Basic IP/port/protocol filtering

## Network Firewall

Think:

**Advanced traffic inspection**

Characteristics:

- Stateful + stateless
- Intrusion prevention
- Domain filtering
- Advanced rule engine

### Memory Trick

**NACL = Basic Subnet Filter**

**Network Firewall = Advanced Network Inspector**

---

# Network Firewall vs WAF

This is one of the most important distinctions.

## [[WAF]]

Think:

**HTTP(S) application-layer attacks**

Examples:

- SQL injection
- XSS
- Malicious URLs
- HTTP rate rules

## Network Firewall

Think:

**VPC network traffic**

Examples:

- IP filtering
- Domain filtering
- Protocol inspection
- Intrusion prevention

### Killer Shortcut

**SQL Injection**
→ WAF

**Malicious VPC Network Traffic**
→ Network Firewall

---

# Network Firewall vs Shield

## [[Shield]]

Think:

**DDoS protection**

## Network Firewall

Think:

**Network traffic inspection**

### Killer Shortcut

Volumetric DDoS  
→ Shield

Inspect/block VPC traffic  
→ Network Firewall

---

# Network Firewall vs GuardDuty

## [[GuardDuty]]

Think:

**Detect suspicious behavior**

## Network Firewall

Think:

**Inspect and block network traffic**

Example:

GuardDuty says:

> EC2 is communicating with a malicious host.

Network Firewall can:

> Block traffic to that destination.

### Memory Trick

**GuardDuty = Detect**

**Network Firewall = Filter**

---

# Network Firewall vs Route 53 Resolver DNS Firewall

These sound similar but solve different problems.

## Network Firewall

Filters:

**Network traffic**

## Route 53 Resolver DNS Firewall

Filters:

**DNS queries**

### Killer Shortcut

Block network connection  
→ Network Firewall

Block DNS lookup for malicious domain  
→ DNS Firewall

---

# Network Firewall vs NAT Gateway

## NAT Gateway

Provides:

**Outbound Internet connectivity**

for private subnets.

## Network Firewall

Provides:

**Traffic inspection**

They may be used together.

Architecture:

Private Subnet  
↓  
Network Firewall  
↓  
NAT Gateway  
↓  
Internet

### Memory Trick

**NAT = Connect Out**

**Firewall = Inspect Out**

---

# Architecture Thinking

## Scenario 1 — Malicious Outbound Traffic

Company needs to prevent EC2 instances from connecting to:

**Known malicious destinations**

Choose:

**Network Firewall**

---

## Scenario 2 — SQL Injection

Web application receives:

**SQL injection attacks**

Choose:

**WAF**

not Network Firewall as the primary answer.

---

## Scenario 3 — DDoS

Public application experiences:

**Large volumetric attack**

Choose:

**Shield**

---

## Scenario 4 — EC2 Port Access

Need to allow:

**HTTPS on port 443**

to EC2.

Choose:

**Security Group**

---

## Scenario 5 — Subnet Deny Rule

Need a basic:

**Stateless subnet-level deny rule**

Choose:

**NACL**

---

## Scenario 6 — Intrusion Prevention

Company requires:

**Managed intrusion prevention for VPC traffic**

Choose:

**Network Firewall**

---

## Scenario 7 — Multiple VPCs

Enterprise has:

50 VPCs

and wants:

**Centralized traffic inspection**

Choose:

Transit Gateway  
↓  
Inspection VPC  
↓  
Network Firewall

---

## Scenario 8 — Suricata

Security team needs:

**Suricata-compatible network rules**

Choose:

**Network Firewall**

---

## Scenario 9 — Stateful Routing Problem

Outbound traffic passes through firewall:

Path A

Return traffic uses:

Path B

Connection fails.

Think:

**Symmetric Routing**

---

# Scenario Recognition

Immediately think:

**Network Firewall**

when you see:

- Managed VPC firewall
- Stateful network inspection
- Stateless network inspection
- Intrusion prevention
- Suricata
- Centralized VPC inspection
- Domain-based network filtering
- Advanced network firewall
- Inspection VPC

---

## Think WAF When You See

- SQL injection
- XSS
- HTTP request inspection
- Web ACL

---

## Think Security Groups When You See

- Instance access
- Port rules
- Stateful resource firewall

---

## Think NACL When You See

- Subnet-level filtering
- Stateless rules
- Explicit deny

---

## Think Shield When You See

- DDoS
- Volumetric attack

---

# Exam Traps

## Trap 1 — Network Firewall and WAF Are the Same

❌

WAF:

**Web application requests**

Network Firewall:

**VPC network traffic**

---

## Trap 2 — Network Firewall Replaces Security Groups

❌

They serve:

**Different layers and purposes**

and can be used together.

---

## Trap 3 — Network Firewall Is Only Stateless

❌

It supports:

**Stateless + Stateful**

inspection.

---

## Trap 4 — NACL Provides the Same Advanced Inspection

❌

NACL provides:

**Basic stateless subnet filtering**

---

## Trap 5 — Network Firewall Is Primarily a DDoS Service

❌

Think:

**Shield**

---

## Trap 6 — Traffic Is Automatically Inspected Just Because a Firewall Exists

❌

Traffic must be:

**Routed through the firewall endpoint**

---

## Trap 7 — Stateful Firewall Routing Can Be Asymmetric

❌

Maintain:

**Symmetric traffic paths**

---

# Quick Cheat Sheet

| Exam Clue | Answer |
|---|---|
| Managed VPC Firewall | Network Firewall |
| Stateful Inspection | Network Firewall |
| Stateless Inspection | Network Firewall |
| Intrusion Prevention | Network Firewall |
| Suricata Rules | Network Firewall |
| Centralized VPC Inspection | Network Firewall + Transit Gateway |
| Web Attack Filtering | WAF |
| DDoS Protection | Shield |
| Resource Port Rules | Security Group |
| Subnet Filtering | NACL |
| Threat Detection | GuardDuty |
| DNS Query Filtering | DNS Firewall |

---

# Network Security Decision Map

Need:

**Advanced VPC traffic inspection**

→ Network Firewall

Need:

**SQL injection/XSS protection**

→ WAF

Need:

**DDoS protection**

→ Shield

Need:

**EC2 port access control**

→ Security Group

Need:

**Subnet-level deny rule**

→ NACL

Need:

**Detect suspicious activity**

→ GuardDuty

Need:

**Central inspection across VPCs**

→ Transit Gateway + Network Firewall

---

# Firewall Comparison

| Service | Main Job | Stateful? |
|---|---|---:|
| Security Group | Resource Access | ✅ |
| NACL | Subnet Filtering | ❌ |
| WAF | HTTP(S) Filtering | Application-Level |
| Network Firewall | Advanced VPC Inspection | ✅ + Stateless |
| Shield | DDoS Protection | Different Purpose |

---

# Final Exam Rapid-Fire

> **ADVANCED VPC FIREWALL**
> → NETWORK FIREWALL
>
> **STATEFUL NETWORK INSPECTION**
> → NETWORK FIREWALL
>
> **SURICATA**
> → NETWORK FIREWALL
>
> **INTRUSION PREVENTION**
> → NETWORK FIREWALL
>
> **CENTRAL VPC INSPECTION**
> → TRANSIT GATEWAY + NETWORK FIREWALL
>
> **SQL INJECTION**
> → WAF
>
> **DDoS**
> → SHIELD
>
> **INSTANCE PORT**
> → SECURITY GROUP
>
> **SUBNET DENY**
> → NACL
>
> **THREAT DETECTION**
> → GUARDDUTY
>
> **DNS QUERY FILTERING**
> → DNS FIREWALL

---

## Master Memory Trick

> [!tip] Network Firewall Master Memory Trick
> Imagine your VPC is:
>
> **A city**
>
> Security Groups are:
>
> **Locks on individual buildings**
>
> NACLs are:
>
> **Checkpoints at neighborhood entrances**
>
> WAF is:
>
> **Security at the web application's front door**
>
> But Network Firewall is:
>
> **THE CENTRAL HIGHWAY INSPECTION STATION**
>
> Traffic is deliberately routed through it.
>
> It can inspect:
>
> **WHERE YOU'RE GOING**
>
> **WHAT PROTOCOL YOU'RE USING**
>
> **WHETHER THE CONNECTION IS SUSPICIOUS**
>
> and then:
>
> **ALLOW**
>
> **DROP**
>
> **ALERT**

So remember:

> **SECURITY GROUP**
> → RESOURCE
>
> **NACL**
> → SUBNET
>
> **WAF**
> → WEB REQUEST
>
> **NETWORK FIREWALL**
> → VPC TRAFFIC
>
> **SHIELD**
> → DDoS
>
> **GUARDDUTY**
> → DETECT THREAT
>
> **TRANSIT GATEWAY**
> → CENTRALIZE NETWORKS

And the killer SAA question:

> **"Does the requirement involve centralized, stateful inspection or advanced filtering of VPC network traffic?"**
>
> YES
>
> → **Network Firewall**

---

## Related Notes

- [[WAF]]
- [[Shield]]
- [[GuardDuty]]
- [[05-Networking/VPC]]
- [[05-Networking/Transit Gateway]]
- [[Security Groups]]
- [[NACL]]
- [[CloudWatch]]