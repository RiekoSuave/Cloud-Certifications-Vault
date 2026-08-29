## Core VPC Architecture

Think of a VPC as:

**Your private network inside AWS**

Typical architecture:

Internet  
↓  
[[Internet Gateway]]  
↓  
Public Subnet  
↓  
[[Application Load Balancer]]  
↓  
Private Application Subnet  
↓  
Private Database Subnet

Key controls:

**Route Tables**
→ Where traffic goes

**[[Security Groups]]**
→ Resource-level firewall

**[[NACL]]**
→ Subnet-level firewall

---

## Public vs Private Subnet

### Public Subnet

A subnet is public when its route table has:

`0.0.0.0/0`

→ **Internet Gateway**

For an EC2 instance to communicate directly with the Internet, it also needs an appropriate:

**Public IPv4 / Elastic IP**

and security rules.

### Private Subnet

No direct route to:

**Internet Gateway**

For outbound IPv4 Internet access:

Private Subnet  
↓  
[[NAT Gateway]]  
↓  
Public Subnet  
↓  
Internet Gateway

### Killer Memory Trick

> **IGW = Public Internet**
>
> **NAT Gateway = Private → Internet**

---

# Internet Gateway

Think:

**Internet connectivity for a VPC**

Key points:

- Attached to VPC
- Used by public subnets
- Route table required
- Supports inbound/outbound Internet connectivity when other requirements are met

### Exam Clue

> **Public EC2 needs Internet connectivity**
>
> → **Internet Gateway**

---

# NAT Gateway

Think:

**Outbound Internet for private IPv4 resources**

Architecture:

Private EC2  
↓  
NAT Gateway  
↓  
Internet Gateway  
↓  
Internet

Key points:

- NAT Gateway belongs in a **public subnet** for public Internet egress
- Private subnet routes to NAT Gateway
- Internet hosts cannot initiate unsolicited connections through it to private instances
- Deploy per AZ when high availability and AZ independence matter

### Exam Clue

> **Private EC2 needs software updates from the Internet**
>
> → **NAT Gateway**

---

# NAT Gateway vs VPC Endpoint

Need:

**General Internet access**

→ NAT Gateway

Need:

**Private access to supported AWS service**

→ [[VPC Endpoints]]

### Killer Cost Pattern

> Heavy private-subnet traffic to S3 through NAT
>
> → Use **S3 Gateway Endpoint**

---

# Security Groups

[[Security Groups]] are:

**Stateful resource-level firewalls**

Key points:

- Allow rules only
- No explicit deny
- Return traffic automatically allowed
- Can reference other Security Groups
- Multiple SG permissions combine

### Killer Pattern

Internet  
↓  
ALB SG  
↓  
Application SG  
↓  
Database SG

Each tier trusts:

**Only the tier that needs access**

### Exam Clue

> **Only ALB should reach EC2**
>
> → Reference **ALB Security Group**

---

# NACL

[[NACL]] is:

**Stateless subnet-level filtering**

Key points:

- Allow + deny
- Numbered rules
- Lowest matching rule evaluated first
- First match wins
- Return traffic must be explicitly permitted
- Ephemeral ports matter

### Killer Exam Clue

> **Explicitly block malicious IP at subnet boundary**
>
> → **NACL**

---

# Security Group vs NACL

| Feature | Security Group | NACL |
|---|---|---|
| Level | Resource / ENI | Subnet |
| Stateful | ✅ | ❌ |
| Allow | ✅ | ✅ |
| Deny | ❌ | ✅ |
| Rule Order | No | Yes |
| Return Traffic | Automatic | Explicit |

### Memory Trick

> **SG = Stateful Guard**
>
> **NACL = Stateless Gate**

---

# VPC Flow Logs

[[VPC Flow Logs]] record:

**Network traffic metadata**

Think:

- Source IP
- Destination IP
- Port
- Protocol
- ACCEPT
- REJECT

They do NOT provide:

**Full packet payloads**

### Killer Exam Clue

> **Determine whether network traffic was accepted or rejected**
>
> → **VPC Flow Logs**

---

# Flow Logs vs CloudTrail

**VPC Flow Logs**

→ Network activity

**[[CloudTrail]]**

→ AWS API activity

### Killer Shortcut

> Who connected?
> → Flow Logs
>
> Who changed the Security Group?
> → CloudTrail

---

# VPC Peering

[[VPC Peering]] provides:

**Direct private connectivity between two VPCs**

Key points:

- Non-overlapping CIDRs
- Route tables required
- Non-transitive
- Cross-account supported
- Inter-Region supported

### Killer Exam Clue

> **Two VPCs need direct private connectivity**
>
> → **VPC Peering**

### Critical Trap

A ↔ B

B ↔ C

does NOT mean:

A ↔ C

> **Peering is non-transitive**

---

# Transit Gateway

[[Transit Gateway]] provides:

**Centralized transitive connectivity**

Think:

**Network hub**

Architecture:

VPC A  
↓  
Transit Gateway  
↑  
VPC B  
↑  
VPC C

Key points:

- Many VPCs
- Hub-and-spoke
- Transitive routing
- Hybrid connectivity
- Route-table segmentation
- Multi-account sharing with RAM
- Central inspection architectures

### Killer Exam Clue

> **Dozens of VPCs need centralized connectivity**
>
> → **Transit Gateway**

---

# Peering vs Transit Gateway

Need:

**Two VPCs**

→ VPC Peering

Need:

**Many VPCs**

→ Transit Gateway

Need:

**Transitive routing**

→ Transit Gateway

### Memory Trick

> **Peering = Private Road**
>
> **TGW = Highway Interchange**

---

# VPC Endpoints

[[VPC Endpoints]] provide:

**Private access to supported AWS services**

without requiring:

- NAT Gateway
- Internet Gateway path
- Public IP

Two major types:

### Gateway Endpoint

Think:

- S3
- DynamoDB
- Route tables

### Interface Endpoint

Think:

- ENI
- Security Group
- PrivateLink
- Many AWS services

### Killer Memory Trick

> **Gateway = S3 + DynamoDB**
>
> **Interface = ENI + PrivateLink**

---

# Endpoint Decision

Need:

**Private S3**

→ Gateway Endpoint

Need:

**Private DynamoDB**

→ Gateway Endpoint

Need:

**Private Secrets Manager**

→ Interface Endpoint

Need:

**Private Systems Manager**

→ Interface Endpoint

Need:

**General Internet**

→ NAT Gateway

---

# PrivateLink

[[PrivateLink]] provides:

**Private access to a specific service**

rather than:

**Full network connectivity**

Classic architecture:

Provider Application  
↓  
Network Load Balancer  
↓  
Endpoint Service  
↓  
PrivateLink  
↓  
Consumer Interface Endpoint

### Killer Exam Clue

> **Expose one private service to many consumer VPCs**
>
> → **PrivateLink**

Especially useful when:

- Full VPC connectivity is unnecessary
- Many consumers exist
- CIDR overlap is problematic

---

# PrivateLink vs Peering vs Transit Gateway

Need:

**One service**

→ PrivateLink

Need:

**Two networks**

→ VPC Peering

Need:

**Many networks**

→ Transit Gateway

### Memory Trick

> **PrivateLink = Service**
>
> **Peering = Pair**
>
> **TGW = Many**

---

# Site-to-Site VPN

[[Site-to-Site VPN]] provides:

**Encrypted network-to-network connectivity over the Internet**

Architecture:

On-Premises  
↓  
Customer Gateway  
↓  
IPsec VPN  
↓  
VGW / Transit Gateway  
↓  
AWS

Key points:

- IPsec encryption
- Two VPN tunnels
- Fast to provision compared with Direct Connect
- BGP can provide dynamic routing
- Useful as Direct Connect backup

### Killer Exam Clue

> **Need encrypted on-premises connectivity quickly**
>
> → **Site-to-Site VPN**

---

# Client VPN

[[Client VPN]] provides:

**Individual user-to-VPC connectivity**

Think:

Remote Employee  
↓  
Laptop  
↓  
Client VPN  
↓  
Private AWS Resources

### Killer Shortcut

**User → AWS**
→ Client VPN

**Network → AWS**
→ Site-to-Site VPN

---

# Direct Connect

[[Direct Connect]] provides:

**Dedicated hybrid connectivity**

Think:

- More predictable performance
- Dedicated network connection
- Large sustained transfers
- Longer provisioning time

### Critical Exam Fact

Direct Connect is:

**Private**

but is not inherently:

**Encrypted by default**

### Killer Exam Clue

> **Need dedicated predictable hybrid connectivity**
>
> → **Direct Connect**

---

# Direct Connect VIFs

### Private VIF

→ Private VPC resources

### Public VIF

→ AWS public endpoints

### Transit VIF

→ Transit Gateway through Direct Connect Gateway architecture

### Memory Trick

> **Private = VPC**
>
> **Public = AWS Public Services**
>
> **Transit = TGW**

---

# VPN vs Direct Connect

| Requirement | Answer |
|---|---|
| Quick Setup | Site-to-Site VPN |
| IPsec Encryption | Site-to-Site VPN |
| Internet-Based | Site-to-Site VPN |
| Dedicated Connection | Direct Connect |
| Predictable Performance | Direct Connect |
| DX Backup | Site-to-Site VPN |
| Dedicated + IPsec | VPN over Direct Connect |

### Killer Memory Trick

> **VPN = Quick + Encrypted**
>
> **DX = Dedicated + Predictable**

---

# Route 53 Resolver

[[Route 53 Resolver]] provides:

**Hybrid DNS resolution**

Two critical endpoint types:

### Inbound

On-Prem  
→ AWS DNS

### Outbound

AWS  
→ On-Prem DNS

### Killer Memory Trick

> **INBOUND = DNS comes INTO AWS**
>
> **OUTBOUND = DNS leaves AWS**

---

# Resolver Rules

Used primarily with:

**Outbound Resolver Endpoints**

to determine:

**Which domains should be forwarded where**

Example:

`corp.internal`

→ On-Prem DNS

### Exam Clue

> **EC2 must resolve corporate on-premises domain**
>
> → Outbound Resolver Endpoint + Resolver Rule

---

# Network Firewall

[[Network Firewall]] provides:

**Advanced managed VPC network inspection**

Think:

- Stateful inspection
- Stateless inspection
- Intrusion prevention
- Suricata-compatible rules
- Central inspection architectures

Common architecture:

Spoke VPCs  
↓  
Transit Gateway  
↓  
Inspection VPC  
↓  
Network Firewall

### Killer Exam Clue

> **Need centralized advanced traffic inspection**
>
> → **Network Firewall**

---

# Network Firewall vs NACL vs Security Group

Need:

**Resource access control**

→ Security Group

Need:

**Subnet allow/deny**

→ NACL

Need:

**Advanced traffic inspection**

→ Network Firewall

---

# Hybrid Architecture Map

> **REMOTE USER**
> ↓
> Client VPN
> ↓
> AWS
>
> **ON-PREM NETWORK**
> ↓
> Site-to-Site VPN
> ↓
> AWS
>
> **ON-PREM + DEDICATED**
> ↓
> Direct Connect
> ↓
> AWS
>
> **ON-PREM + MANY VPCs**
> ↓
> VPN / Direct Connect
> ↓
> Transit Gateway
> ↓
> VPCs

---

# Connectivity Decision Map

Need:

**Public Internet for public resource**

→ Internet Gateway

Need:

**Private IPv4 resource → Internet**

→ NAT Gateway

Need:

**Private access to S3/DynamoDB**

→ Gateway Endpoint

Need:

**Private access to supported AWS service via ENI**

→ Interface Endpoint

Need:

**Two VPCs**

→ VPC Peering

Need:

**Many VPCs**

→ Transit Gateway

Need:

**One private service**

→ PrivateLink

Need:

**On-premises network quickly**

→ Site-to-Site VPN

Need:

**Dedicated on-premises connection**

→ Direct Connect

Need:

**Remote employee**

→ Client VPN

Need:

**Hybrid DNS**

→ Route 53 Resolver

---

# Troubleshooting Decision Map

## EC2 Cannot Reach Internet

Check:

1. Route table
2. IGW / NAT Gateway
3. Public/private IP configuration
4. Security Group
5. NACL

---

## Peered VPCs Cannot Communicate

Check:

1. Peering status
2. Non-overlapping CIDRs
3. Route tables
4. Security Groups
5. NACLs
6. DNS if hostname-based

---

## Private EC2 Cannot Reach AWS Service

Ask:

**Does it need general Internet?**

YES  
→ NAT Gateway

NO, supported AWS service  
→ VPC Endpoint

---

## VPN Connected but Traffic Fails

Check:

1. Routes
2. BGP/static routing
3. Security Groups
4. NACLs
5. Tunnel status

---

## Client VPN Connects but Resource Fails

Check:

1. Client VPN routes
2. Authorization rules
3. Security Groups
4. NACLs
5. DNS

---

## Hybrid DNS Fails

Ask:

On-Prem → AWS?

→ Inbound Resolver Endpoint

AWS → On-Prem?

→ Outbound Resolver Endpoint + Resolver Rule

---

# Major Exam Traps

## Trap 1

**Public subnet = EC2 automatically has Internet**

❌

You still need appropriate:

- Route
- IGW
- Public addressing
- Security controls

---

## Trap 2

**NAT Gateway belongs in private subnet**

❌

For public Internet egress:

**NAT Gateway belongs in a public subnet**

---

## Trap 3

**Security Groups can deny traffic**

❌

They use:

**Allow rules only**

---

## Trap 4

**NACL is stateful**

❌

It is:

**Stateless**

---

## Trap 5

**VPC Peering is transitive**

❌

Use:

**Transit Gateway**

---

## Trap 6

**PrivateLink connects entire networks**

❌

It exposes:

**Specific services**

---

## Trap 7

**VPC Endpoint provides general Internet**

❌

Use:

**NAT Gateway**

---

## Trap 8

**Direct Connect is encrypted by default**

❌

Private connectivity does not automatically mean:

**Encrypted**

---

## Trap 9

**Site-to-Site VPN is for remote employees**

❌

Use:

**Client VPN**

---

## Trap 10

**Direct Connect automatically solves hybrid DNS**

❌

Use:

**Route 53 Resolver**

---

# Quick Cheat Sheet

| Exam Clue | Answer |
|---|---|
| Public Internet | Internet Gateway |
| Private → Internet | NAT Gateway |
| Resource Firewall | Security Group |
| Subnet Firewall | NACL |
| Explicit Deny | NACL |
| Network Metadata | VPC Flow Logs |
| Two VPCs | VPC Peering |
| Many VPCs | Transit Gateway |
| Transitive Routing | Transit Gateway |
| Private S3 | Gateway Endpoint |
| Private DynamoDB | Gateway Endpoint |
| Private AWS Service ENI | Interface Endpoint |
| One Private Service | PrivateLink |
| Network → AWS | Site-to-Site VPN |
| User → AWS | Client VPN |
| Dedicated Hybrid | Direct Connect |
| Hybrid DNS | Route 53 Resolver |
| On-Prem → AWS DNS | Inbound Resolver |
| AWS → On-Prem DNS | Outbound Resolver |
| Advanced VPC Inspection | Network Firewall |

---

# Master Exam Decision Tree

> **INTERNET?**
>
> Public resource
> → IGW
>
> Private resource outbound
> → NAT Gateway
>
> ---
>
> **AWS SERVICE PRIVATELY?**
>
> S3 / DynamoDB
> → Gateway Endpoint
>
> Other supported service
> → Interface Endpoint
>
> ---
>
> **CONNECT NETWORKS?**
>
> Two VPCs
> → VPC Peering
>
> Many VPCs
> → Transit Gateway
>
> One service only
> → PrivateLink
>
> ---
>
> **HYBRID?**
>
> Quick + encrypted
> → Site-to-Site VPN
>
> Dedicated + predictable
> → Direct Connect
>
> Remote individual user
> → Client VPN
>
> ---
>
> **DNS?**
>
> On-Prem → AWS
> → Inbound Resolver
>
> AWS → On-Prem
> → Outbound Resolver
>
> ---
>
> **SECURITY?**
>
> Resource
> → Security Group
>
> Subnet
> → NACL
>
> Advanced inspection
> → Network Firewall
>
> Network evidence
> → VPC Flow Logs

---

## Master Memory Trick

> [!tip] VPC Master Memory Trick
> Imagine AWS networking as:
>
> **A CITY**
>
> The:
>
> **VPC**
>
> is your private city.
>
> **SUBNETS**
>
> are neighborhoods.
>
> **ROUTE TABLES**
>
> are road signs.
>
> **INTERNET GATEWAY**
>
> is the highway entrance.
>
> **NAT GATEWAY**
>
> lets private residents drive out without letting strangers initiate the trip back in.
>
> **SECURITY GROUP**
>
> is the security guard at the building.
>
> **NACL**
>
> is the checkpoint around the neighborhood.
>
> **FLOW LOGS**
>
> are the traffic cameras.
>
> **VPC PEERING**
>
> is a private road between two cities.
>
> **TRANSIT GATEWAY**
>
> is the giant highway interchange connecting many cities.
>
> **VPC ENDPOINT**
>
> is a private hallway to an AWS service.
>
> **PRIVATELINK**
>
> is a private service window.
>
> **SITE-TO-SITE VPN**
>
> is an encrypted tunnel from your company's network.
>
> **DIRECT CONNECT**
>
> is a dedicated private road from your company.
>
> **CLIENT VPN**
>
> is an employee's private entrance.
>
> **ROUTE 53 RESOLVER**
>
> is the translator between AWS and on-premises phone books.
>
> **NETWORK FIREWALL**
>
> is the advanced inspection checkpoint.

So for the exam, keep asking:

> **WHO needs to connect to WHAT?**
>
> **Does it need Internet or private connectivity?**
>
> **One resource, one service, two networks, or many networks?**
>
> **Is the requirement routing, security, logging, or DNS?**

Those four questions eliminate:

**Most wrong VPC answers quickly.**

---

## Related Notes

- [[VPC]]
- [[Internet Gateway]]
- [[NAT Gateway]]
- [[Security Groups]]
- [[NACL]]
- [[VPC Flow Logs]]
- [[VPC Peering]]
- [[VPC Endpoints]]
- [[PrivateLink]]
- [[Transit Gateway]]
- [[Site-to-Site VPN]]
- [[Direct Connect]]
- [[Client VPN]]
- [[Route 53 Resolver]]
- [[Network Firewall]]