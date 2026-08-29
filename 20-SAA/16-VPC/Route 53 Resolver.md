## What Problem Does It Solve?

[[Route 53 Resolver]] provides:

**DNS resolution between AWS VPCs and on-premises networks**

It is especially important in:

**Hybrid DNS architectures**

Architecture:

On-Premises  
↕  
Route 53 Resolver Endpoints  
↕  
VPC DNS / AWS Private DNS

> [!tip] Memory Trick
> **Route 53 Resolver = DNS Bridge Between AWS and On-Prem**

---

## Core Concept

Hybrid environments often have two DNS worlds:

**AWS DNS**

and:

**On-Premises DNS**

Route 53 Resolver allows DNS queries to move:

**Between them**

### Killer Exam Clue

> **On-premises systems need to resolve private DNS names inside AWS**
>
> → **Route 53 Resolver Inbound Endpoint**

> **AWS resources need to resolve on-premises DNS names**
>
> → **Route 53 Resolver Outbound Endpoint**

---

# Route 53 Resolver

Every VPC includes access to:

**Amazon-provided DNS resolution**

Route 53 Resolver can resolve:

- Public DNS names
- VPC-specific DNS names
- Private hosted zone records associated with the VPC

For hybrid DNS, you extend this capability using:

**Resolver Endpoints**

---

# Two Endpoint Types

The two critical endpoint types are:

1. **Inbound Endpoint**
2. **Outbound Endpoint**

### Master Shortcut

> **INBOUND**
> → Queries coming **INTO AWS**
>
> **OUTBOUND**
> → Queries going **OUT OF AWS**

This distinction is:

**Extremely important for SAA**

---

# Inbound Resolver Endpoint

An:

**Inbound Resolver Endpoint**

allows DNS queries from:

**On-premises**

to enter:

**AWS Route 53 Resolver**

Architecture:

On-Prem DNS  
↓  
Direct Connect / VPN  
↓  
Inbound Resolver Endpoint  
↓  
Route 53 Resolver  
↓  
Private AWS DNS

### Killer Exam Clue

> **On-premises servers must resolve records in a Route 53 Private Hosted Zone**
>
> → **Inbound Resolver Endpoint**

---

# Inbound Endpoint IP Addresses

Inbound endpoints create:

**Elastic Network Interfaces**

inside selected VPC subnets.

These receive:

**Private IP addresses**

On-premises DNS servers can forward queries to:

**Those private IP addresses**

### Memory Trick

**Inbound Endpoint = Private DNS Listener Inside AWS**

---

# Inbound Example

Suppose AWS hosts:

`database.internal.example.com`

inside:

**A Private Hosted Zone**

An on-premises application needs to resolve it.

Flow:

On-Prem Application  
↓  
On-Prem DNS Server  
↓  
Inbound Resolver Endpoint  
↓  
Route 53 Private Hosted Zone  
↓  
Private IP

### Killer Shortcut

**On-Prem → AWS DNS**
→ Inbound

---

# Outbound Resolver Endpoint

An:

**Outbound Resolver Endpoint**

allows AWS DNS queries to be forwarded to:

**External DNS servers**

such as:

**On-premises DNS**

Architecture:

EC2  
↓  
Route 53 Resolver  
↓  
Outbound Resolver Endpoint  
↓  
VPN / Direct Connect  
↓  
On-Prem DNS Server

### Killer Exam Clue

> **EC2 instances must resolve on-premises domain names**
>
> → **Outbound Resolver Endpoint**

---

# Outbound Example

Suppose on-premises hosts:

`database.corp.example.com`

AWS applications need to resolve it.

Flow:

EC2  
↓  
Route 53 Resolver  
↓  
Outbound Endpoint  
↓  
On-Prem DNS  
↓  
Private On-Prem IP

### Killer Shortcut

**AWS → On-Prem DNS**
→ Outbound

---

# Resolver Rules

Outbound Resolver Endpoints work with:

**Resolver Rules**

Rules specify:

**Which DNS queries should be forwarded**

and:

**Where they should go**

Example:

Domain:

`corp.example.com`

Forward to:

`10.50.0.10`

### Memory Trick

**Resolver Rule = Which Domain Goes Where**

---

# Conditional Forwarding

Resolver Rules enable:

**Conditional DNS forwarding**

Example:

Queries for:

`corp.example.com`

→ Forward to on-premises DNS

Other queries:

→ Resolve normally through Route 53 Resolver

### Killer Exam Clue

> **Only queries for the corporate domain should be sent to on-prem DNS**
>
> → **Resolver Rule**

---

# Forward Rule

A:

**Forward Rule**

sends matching DNS queries to:

**Specified target DNS servers**

Example:

`company.local`

↓  

On-Prem DNS Server

---

# System Rule

Route 53 Resolver also uses:

**System Rules**

for certain AWS-managed DNS behavior.

For SAA, focus primarily on:

**Forwarding rules**

for hybrid DNS.

---

# Recursive DNS Resolution

Route 53 Resolver acts as:

**A recursive DNS resolver**

for resources inside VPCs.

Applications ask:

> What IP belongs to this hostname?

Resolver determines:

**The answer**

using the appropriate DNS path.

---

# Route 53 Resolver + Private Hosted Zones

A:

[[Route 53]] Private Hosted Zone

contains DNS records accessible within:

**Associated VPCs**

Inbound Resolver Endpoints can extend access so:

**On-premises systems**

can resolve those private records.

### Killer Exam Pattern

On-Prem  
↓  
Inbound Endpoint  
↓  
Private Hosted Zone

---

# Route 53 Resolver + On-Prem DNS

Outbound endpoints extend AWS DNS resolution toward:

**On-premises DNS servers**

### Killer Exam Pattern

AWS  
↓  
Outbound Endpoint  
↓  
On-Prem DNS

---

# Bidirectional Hybrid DNS

Many hybrid environments need:

**Both directions**

Architecture:

On-Prem DNS  
↓  
Inbound Endpoint  
↓  
AWS DNS

and:

AWS DNS  
↓  
Outbound Endpoint  
↓  
On-Prem DNS

### Memory Trick

**Hybrid DNS = Inbound + Outbound**

---

# Direct Connect

[[Direct Connect]] can provide:

**Network connectivity**

between on-premises and AWS.

Route 53 Resolver provides:

**DNS connectivity**

### Killer Exam Principle

> **Direct Connect does NOT automatically solve hybrid DNS**

### Memory Trick

**Direct Connect = Network Path**

**Resolver = DNS Path**

---

# Site-to-Site VPN

[[Site-to-Site VPN]] can also provide:

**Network connectivity**

for Resolver traffic.

Architecture:

On-Prem DNS  
↓  
VPN  
↓  
Resolver Endpoint

### Exam Principle

> **Resolver endpoints require underlying network connectivity**

---

# Transit Gateway

[[Transit Gateway]] may provide centralized:

**Network connectivity**

between VPCs and:

**On-premises**

But again:

Transit Gateway handles:

**Routing**

Route 53 Resolver handles:

**DNS resolution**

---

# Security Groups

Resolver endpoints use:

[[Security Groups]]

because they create:

**ENIs**

inside VPC subnets.

Security Groups must allow:

**DNS traffic**

as required.

DNS commonly uses:

- UDP 53
- TCP 53

### Killer Exam Clue

> **Resolver Endpoint exists but DNS queries fail**
>
> → Check **Security Group port 53**

---

# High Availability

Resolver endpoints should be deployed across:

**Multiple Availability Zones**

for resilient DNS architectures.

### SAA Principle

> **DNS is critical infrastructure — design Resolver endpoints for HA**

---

# Multiple IP Addresses

Resolver endpoints can use:

**Multiple IP addresses**

across:

**Multiple subnets/AZs**

On-premises DNS systems can forward to:

**Multiple endpoint addresses**

for resilience.

---

# Resolver Rules Across VPCs

Resolver Rules can be shared with:

**Other AWS accounts**

using:

**AWS Resource Access Manager — RAM**

### Killer Exam Clue

> **Central networking account manages DNS forwarding rules for many AWS accounts**
>
> → **Route 53 Resolver Rules + RAM**

---

# Centralized DNS Architecture

Large organizations may create:

**A centralized DNS VPC**

Architecture:

Application VPCs  
↓  
Central DNS Architecture  
↓  
Resolver Endpoints  
↓  
On-Prem DNS

This reduces:

**Duplicate endpoint infrastructure**

and centralizes:

**DNS administration**

---

# Route 53 Resolver vs Route 53 Hosted Zone

Do not confuse these.

## Route 53 Hosted Zone

Stores:

**DNS records**

## Route 53 Resolver

Answers and forwards:

**DNS queries**

### Memory Trick

**Hosted Zone = Phone Book**

**Resolver = Person Looking Up the Number**

---

# Resolver vs Private Hosted Zone

## Private Hosted Zone

Stores:

**Private AWS DNS records**

## Resolver Endpoint

Allows:

**DNS queries to cross hybrid boundaries**

### Killer Shortcut

Need to create private DNS records  
→ Private Hosted Zone

Need on-prem to resolve those records  
→ Inbound Resolver Endpoint

---

# Resolver vs VPC Peering

[[VPC Peering]] provides:

**Network connectivity**

It does not automatically provide:

**Complete hybrid DNS forwarding architecture**

### Memory Trick

**Peering = Network**

**Resolver = DNS**

---

# Resolver vs PrivateLink

[[PrivateLink]] provides:

**Private service connectivity**

Route 53 Resolver provides:

**DNS resolution**

Private DNS may be used alongside PrivateLink, but they solve:

**Different problems**

---

# DNS Firewall

Route 53 Resolver also integrates with:

**DNS Firewall**

for controlling DNS queries.

DNS Firewall can:

- Allow domains
- Block domains
- Alert on domains

### Killer Exam Clue

> **Need to block VPC workloads from resolving known malicious domains**
>
> → **Route 53 Resolver DNS Firewall**

---

# DNS Firewall vs Network Firewall

## DNS Firewall

Filters:

**DNS queries**

## [[20-SAA/15-Security/Network Firewall]]

Inspects:

**Network traffic**

### Killer Shortcut

Block malicious domain resolution  
→ DNS Firewall

Inspect network packets/flows  
→ Network Firewall

---

# DNS Firewall Rule Groups

DNS Firewall uses:

**Rule Groups**

containing rules that specify:

- Domain lists
- Actions
- Priority

Possible actions include:

- ALLOW
- BLOCK
- ALERT

### Memory Trick

**DNS Firewall = Domain-Level Guard**

---

# Query Logging

Route 53 Resolver supports:

**DNS query logging**

This provides visibility into:

**DNS queries made by VPC resources**

### Killer Exam Clue

> **Need to investigate which domain names EC2 instances are resolving**
>
> → **Route 53 Resolver Query Logging**

---

# Resolver Query Logging vs VPC Flow Logs

## [[VPC Flow Logs]]

Show:

- Source IP
- Destination IP
- Ports
- ACCEPT/REJECT

## Resolver Query Logs

Show:

**DNS queries**

### Killer Shortcut

Which IP did EC2 contact?  
→ VPC Flow Logs

Which domain did EC2 resolve?  
→ Resolver Query Logs

---

# Architecture Thinking

## Scenario 1 — On-Prem Resolves AWS

On-premises servers need to resolve:

`db.aws.internal`

stored in:

**Route 53 Private Hosted Zone**

Choose:

**Inbound Resolver Endpoint**

---

## Scenario 2 — AWS Resolves On-Prem

EC2 needs to resolve:

`database.corp.internal`

hosted by:

**On-premises DNS**

Choose:

**Outbound Resolver Endpoint + Resolver Rule**

---

## Scenario 3 — Both Directions

AWS and on-premises applications need:

**Mutual private DNS resolution**

Choose:

- Inbound Endpoint
- Outbound Endpoint
- Resolver Rules

---

## Scenario 4 — Direct Connect Exists

Company already has:

**Direct Connect**

but EC2 cannot resolve:

**On-premises hostnames**

Direct Connect alone is not enough.

Add:

**Outbound Resolver Endpoint**

---

## Scenario 5 — On-Prem Cannot Resolve AWS Private Zone

Network connectivity works.

Private Hosted Zone exists.

On-premises DNS still cannot resolve it.

Add:

**Inbound Resolver Endpoint**

---

## Scenario 6 — Corporate Domain Only

Only:

`corp.example.com`

should go to:

**On-prem DNS**

Create:

**Resolver Forward Rule**

---

## Scenario 7 — Central DNS Across Accounts

Networking account manages:

**Hybrid DNS forwarding**

for many AWS accounts.

Use:

**Resolver Rules + RAM**

---

## Scenario 8 — Malicious DNS

Security team wants to block:

`malware.example`

from being resolved by VPC workloads.

Choose:

**Route 53 Resolver DNS Firewall**

---

## Scenario 9 — DNS Investigation

Security team wants to determine:

**Which domains an EC2 instance queried**

Choose:

**Resolver Query Logging**

---

# Scenario Recognition

Immediately think:

**Route 53 Resolver**

when you see:

- Hybrid DNS
- On-prem DNS
- AWS private DNS
- DNS forwarding
- Resolver Endpoint
- Inbound DNS
- Outbound DNS
- Conditional forwarding

---

## Think Inbound When You See

- On-prem → AWS DNS
- Resolve Private Hosted Zone from on-prem
- Queries entering AWS

---

## Think Outbound When You See

- AWS → On-prem DNS
- EC2 resolves corporate domain
- Queries leaving AWS

---

## Think DNS Firewall When You See

- Malicious domains
- Block DNS resolution
- Domain allow/deny lists

---

# Exam Traps

## Trap 1 — Inbound Means AWS Queries On-Prem

❌

Inbound means:

**DNS queries come INTO AWS**

---

## Trap 2 — Outbound Means On-Prem Queries AWS

❌

Outbound means:

**DNS queries leave AWS**

---

## Trap 3 — Direct Connect Automatically Provides Hybrid DNS

❌

Direct Connect provides:

**Network connectivity**

Resolver provides:

**DNS resolution**

---

## Trap 4 — Private Hosted Zone Automatically Works From On-Prem

❌

Typically use:

**Inbound Resolver Endpoint**

---

## Trap 5 — Outbound Endpoint Alone Knows Which Domains to Forward

❌

Use:

**Resolver Rules**

---

## Trap 6 — Resolver Endpoints Do Not Need Security Groups

❌

They create:

**ENIs**

and use:

**Security Groups**

---

## Trap 7 — Route 53 Resolver Is Only for Public DNS

❌

It is especially important for:

**Private and hybrid DNS**

---

# Quick Cheat Sheet

| Exam Clue | Answer |
|---|---|
| Hybrid DNS | Route 53 Resolver |
| On-Prem → AWS DNS | Inbound Endpoint |
| AWS → On-Prem DNS | Outbound Endpoint |
| Conditional Forwarding | Resolver Rule |
| Private DNS Records | Private Hosted Zone |
| Network Path | VPN / Direct Connect |
| DNS Endpoint Security | Security Group |
| DNS Port | TCP/UDP 53 |
| Share Resolver Rules | RAM |
| Block Malicious Domains | DNS Firewall |
| DNS Query Investigation | Resolver Query Logging |

---

# Hybrid DNS Decision Map

Need:

**On-prem resolve AWS private DNS**

→ Inbound Resolver Endpoint

Need:

**AWS resolve on-prem DNS**

→ Outbound Resolver Endpoint

Need:

**Specific domain forwarded**

→ Resolver Rule

Need:

**Private DNS records**

→ Private Hosted Zone

Need:

**Block malicious domain resolution**

→ DNS Firewall

Need:

**See DNS queries**

→ Resolver Query Logging

---

# Direction Memory Map

> **ON-PREM → AWS**
> → INBOUND
>
> **AWS → ON-PREM**
> → OUTBOUND

### Master Direction Trick

Ask:

> **From AWS's perspective, which direction is the DNS query moving?**

Entering AWS:

**INBOUND**

Leaving AWS:

**OUTBOUND**

---

# Final Exam Rapid-Fire

> **HYBRID DNS**
> → ROUTE 53 RESOLVER
>
> **ON-PREM → AWS DNS**
> → INBOUND ENDPOINT
>
> **AWS → ON-PREM DNS**
> → OUTBOUND ENDPOINT
>
> **DOMAIN FORWARDING**
> → RESOLVER RULE
>
> **PRIVATE DNS RECORDS**
> → PRIVATE HOSTED ZONE
>
> **NETWORK CONNECTIVITY**
> → VPN / DIRECT CONNECT
>
> **DNS PORT**
> → 53
>
> **SHARE RULES**
> → RAM
>
> **BLOCK MALICIOUS DOMAIN**
> → DNS FIREWALL
>
> **LOG DNS QUERIES**
> → RESOLVER QUERY LOGGING

---

## Master Memory Trick

> [!tip] Route 53 Resolver Master Memory Trick
> Imagine AWS and your data center are:
>
> **TWO COUNTRIES**
>
> Each country has:
>
> **ITS OWN PHONE BOOK**
>
> Your on-premises server asks:
>
> **"What's the number for db.aws.internal?"**
>
> The question must travel:
>
> **INTO AWS**
>
> so use:
>
> **INBOUND RESOLVER**
>
> Then EC2 asks:
>
> **"What's the number for server.corp.internal?"**
>
> The question must travel:
>
> **OUT OF AWS**
>
> so use:
>
> **OUTBOUND RESOLVER**

So remember:

> **INBOUND**
> → ON-PREM ASKS AWS
>
> **OUTBOUND**
> → AWS ASKS ON-PREM
>
> **RESOLVER RULE**
> → WHICH DOMAIN GOES WHERE
>
> **PRIVATE HOSTED ZONE**
> → AWS PRIVATE PHONE BOOK
>
> **VPN / DX**
> → NETWORK ROAD
>
> **RESOLVER**
> → DNS BRIDGE

And the killer SAA question:

> **"Does the architecture need DNS queries to cross between AWS and an on-premises environment?"**
>
> YES
>
> → **Route 53 Resolver**

---

## Related Notes

- [[Route 53]]
- [[VPC]]
- [[Direct Connect]]
- [[Site-to-Site VPN]]
- [[Transit Gateway]]
- [[VPC Flow Logs]]
- [[20-SAA/15-Security/Network Firewall]]
- [[Security Groups]]