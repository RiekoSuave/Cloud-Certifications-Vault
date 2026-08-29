## What Problem Does It Solve?

[[VPC]] gives you:

**A logically isolated virtual network inside AWS**

It lets you control:

- IP address ranges
- Subnets
- Route tables
- Internet access
- Private connectivity
- Network security
- Traffic flow

Architecture:

AWS Region  
↓  
VPC  
↓  
Subnets  
↓  
AWS Resources

> [!tip] Memory Trick
> **VPC = Your Private Network in AWS**

---

## Core Concept

A VPC is:

**Regional**

It can span:

**Multiple Availability Zones**

Inside the VPC, you create:

**Subnets**

and each subnet exists in:

**One Availability Zone**

### Killer Exam Clue

> **Need an isolated AWS network with control over IP addressing, routing, and security**
>
> → **VPC**

---

# VPC Is Regional

A VPC exists within:

**One AWS Region**

Example:

`us-east-1`

Within that Region, the VPC can contain subnets in:

- us-east-1a
- us-east-1b
- us-east-1c

### Memory Trick

**VPC = Region**

**Subnet = AZ**

---

# CIDR Blocks

When creating a VPC, you assign:

**CIDR blocks**

CIDR defines:

**The IP address range available to the VPC**

Example:

`10.0.0.0/16`

This provides a range of:

**Private IP addresses**

for resources.

### Killer Exam Concept

> **Plan VPC CIDR ranges carefully to avoid overlap with connected networks**

---

# RFC 1918 Private IPv4 Ranges

Common private IPv4 ranges include:

`10.0.0.0/8`

`172.16.0.0/12`

`192.168.0.0/16`

These addresses are:

**Not directly routable on the public Internet**

---

# CIDR Planning

Poor CIDR planning can cause problems when connecting:

- VPCs
- On-premises networks
- Other cloud environments

Example:

VPC A:

`10.0.0.0/16`

VPC B:

`10.0.0.0/16`

These ranges:

**Overlap**

which complicates direct routing.

### Killer Exam Clue

> **Need future VPC peering or hybrid connectivity**
>
> → Avoid overlapping CIDR ranges.

---

# Secondary CIDR Blocks

A VPC can have:

**Additional CIDR blocks**

added when more address space is required.

This can help expand:

**Available private IP capacity**

without replacing the VPC.

---

# Subnets

A:

**Subnet**

is a range of IP addresses inside:

**A VPC**

Every subnet belongs to:

**Exactly one Availability Zone**

Architecture:

VPC  
↓  
├── Public Subnet — AZ A
├── Private Subnet — AZ A
├── Public Subnet — AZ B
└── Private Subnet — AZ B

### Memory Trick

**Subnet = Slice of VPC in One AZ**

---

# Public Subnet

A subnet is considered:

**Public**

when its route table has a route to:

**An Internet Gateway**

Example:

`0.0.0.0/0`
→ Internet Gateway

### Killer Exam Principle

> **A subnet is public because of routing, not because of its name**

---

# Private Subnet

A:

**Private Subnet**

does not have a direct route to:

**An Internet Gateway**

Resources can still access the Internet through mechanisms such as:

**NAT Gateway**

for outbound-only IPv4 access.

---

# Public vs Private Subnet

| Requirement | Public Subnet | Private Subnet |
|---|---:|---:|
| Direct IGW Route | ✅ | ❌ |
| Internet-Facing ALB | ✅ | ❌ |
| Private App Servers | Possible but Less Ideal | ✅ |
| Databases | Usually Avoid | ✅ |
| NAT Gateway Location | ✅ | ❌ |

### Memory Trick

**Public = Route to IGW**

**Private = No Direct IGW Route**

---

# Internet Gateway

An:

**Internet Gateway — IGW**

allows communication between:

**A VPC and the Internet**

Architecture:

Internet  
↓  
Internet Gateway  
↓  
VPC

### Killer Exam Clue

> **Need Internet connectivity for public IPv4 resources in a VPC**
>
> → **Internet Gateway**

---

# IGW Characteristics

An Internet Gateway is:

- Horizontally scalable
- Highly available
- Managed by AWS

It is attached to:

**A VPC**

### Exam Principle

> You do not provision individual IGW instances.

---

# Public IPv4 Internet Access

For an EC2 instance to access the Internet directly using IPv4, typically it needs:

1. Public IPv4 address or Elastic IP
2. Route to Internet Gateway
3. Security Group allowing traffic
4. NACL allowing traffic

### Killer Exam Trap

> **IGW route alone does NOT make an EC2 instance Internet-accessible**

---

# Route Tables

A:

**Route Table**

determines:

**Where network traffic should go**

Each route has:

- Destination
- Target

Example:

`10.0.0.0/16`
→ local

`0.0.0.0/0`
→ Internet Gateway

### Memory Trick

**Route Table = Network GPS**

---

# Local Route

Every VPC route table contains a:

**Local route**

that enables communication within:

**The VPC CIDR**

Example:

`10.0.0.0/16`
→ local

This allows resources in different subnets to communicate if:

**Security controls permit it**

---

# Longest Prefix Match

AWS routing uses:

**Longest Prefix Match**

The most specific matching route wins.

Example:

`10.0.0.0/16`
→ Target A

`10.0.1.0/24`
→ Target B

Traffic to:

`10.0.1.50`

uses:

`10.0.1.0/24`

because it is:

**More specific**

### Killer Exam Clue

> **Which route does traffic use?**
>
> → Choose the most specific matching CIDR.

---

# Main Route Table

Every VPC has a:

**Main Route Table**

Subnets without an explicit route-table association use:

**The main route table**

---

# Custom Route Tables

You can create:

**Custom Route Tables**

for different subnet behaviors.

Example:

Public Route Table  
→ IGW

Private Route Table  
→ NAT Gateway

This is common in:

**Multi-tier architectures**

---

# NAT Gateway

A:

**NAT Gateway**

allows resources in private subnets to initiate:

**Outbound IPv4 Internet connections**

without allowing unsolicited inbound Internet connections.

Architecture:

Private EC2  
↓  
Private Route Table  
↓  
NAT Gateway  
↓  
Internet Gateway  
↓  
Internet

### Killer Exam Clue

> **Private EC2 instances need outbound Internet access for updates**
>
> → **NAT Gateway**

---

# NAT Gateway Placement

A NAT Gateway is placed in:

**A public subnet**

and uses:

**An Elastic IP**

Architecture:

Private Subnet  
↓  
Route to NAT Gateway  
↓  
Public Subnet  
↓  
Internet Gateway

### Memory Trick

**Private Instance → NAT → IGW**

---

# NAT Gateway High Availability

A NAT Gateway is:

**Highly available within one Availability Zone**

For AZ-resilient architecture:

Deploy:

**One NAT Gateway per AZ**

and route each private subnet to:

**The NAT Gateway in its own AZ**

### Killer Exam Clue

> **Need resilient private-subnet Internet access across AZ failures**
>
> → **NAT Gateway per AZ**

---

# NAT Gateway Cost Optimization

NAT Gateway pricing can include:

- Hourly charge
- Data processing charges

Cross-AZ routing to a NAT Gateway can also create:

**Additional cost**

### SAA Principle

> **Use one NAT Gateway per AZ when availability and cross-AZ traffic costs matter**

---

# NAT Gateway vs NAT Instance

## NAT Gateway

Think:

- Managed
- Scalable
- Highly available within AZ
- Minimal administration

## NAT Instance

Think:

- EC2-based
- You manage it
- Security Groups
- Scaling required
- Legacy/custom situations

### Killer Shortcut

**Production managed NAT**
→ NAT Gateway

---

# NAT Is Outbound Only

Private instances can:

**Initiate outbound connections**

External systems cannot use the NAT Gateway to initiate:

**New inbound sessions to the private instance**

### Memory Trick

**NAT = Private Gets Out**

Not:

**Internet Gets In**

---

# IPv6

IPv6 addresses are generally:

**Globally routable**

IPv6 does not use traditional IPv4 NAT in the same way.

For outbound-only IPv6 access, use:

**Egress-Only Internet Gateway**

---

# Egress-Only Internet Gateway

An:

**Egress-Only Internet Gateway**

allows IPv6 resources to:

**Initiate outbound Internet connections**

while preventing:

**Unsolicited inbound IPv6 connections**

### Killer Exam Clue

> **Private IPv6 resources need outbound Internet access only**
>
> → **Egress-Only Internet Gateway**

### Memory Trick

**IPv4 Outbound Private**
→ NAT Gateway

**IPv6 Outbound Private**
→ Egress-Only IGW

---

# Security Groups

[[Security Groups]] operate at:

**Resource / ENI level**

Characteristics:

- Stateful
- Allow rules only
- Inbound and outbound rules
- Return traffic automatically allowed

### Memory Trick

**Security Group = Resource Firewall**

---

# NACL

[[NACL]] operates at:

**Subnet level**

Characteristics:

- Stateless
- Allow rules
- Deny rules
- Numbered rule evaluation

### Memory Trick

**NACL = Subnet Firewall**

---

# Security Group vs NACL

| Feature | Security Group | NACL |
|---|---|---|
| Level | Resource/ENI | Subnet |
| Stateful | ✅ | ❌ |
| Allow Rules | ✅ | ✅ |
| Deny Rules | ❌ | ✅ |
| Return Traffic Automatic | ✅ | ❌ |
| Rule Order | All Evaluated | Number Order |

### Killer Shortcut

**Resource-level stateful firewall**
→ Security Group

**Subnet-level stateless deny**
→ NACL

---

# Stateful vs Stateless

## Stateful

If inbound traffic is allowed:

**Return traffic is automatically allowed**

Think:

Security Group

## Stateless

Inbound and outbound traffic must both be:

**Explicitly allowed**

Think:

NACL

### Memory Trick

**Stateful = Remembers**

**Stateless = Forgets**

---

# Ephemeral Ports

Stateless filtering often requires understanding:

**Ephemeral ports**

Clients use temporary high-numbered ports for:

**Return traffic**

This matters especially with:

**NACLs**

### Killer Exam Trap

> **NACL rules may need ephemeral-port ranges for return traffic**

---

# VPC Peering

**VPC Peering**

provides private connectivity between:

**Two VPCs**

Architecture:

VPC A  
↔  
VPC Peering Connection  
↔  
VPC B

### Killer Exam Clue

> **Privately connect two VPCs directly**
>
> → **VPC Peering**

---

# VPC Peering Is Non-Transitive

This is extremely important.

If:

VPC A ↔ VPC B

and:

VPC B ↔ VPC C

VPC A cannot automatically communicate with:

VPC C

through:

VPC B.

### Memory Trick

**Peering = No Transit**

---

# Peering CIDR Requirement

Peered VPCs cannot have:

**Overlapping CIDR blocks**

### Killer Exam Trap

> **Overlapping VPC CIDRs**
>
> → Cannot directly use standard VPC peering.

---

# Transit Gateway

[[05-Networking/Transit Gateway]] acts as:

**A hub for connecting many VPCs and networks**

Architecture:

VPC A  
↓  
Transit Gateway  
↑  
VPC B  
↑  
VPC C  
↑  
VPN / On-Premises

### Killer Exam Clue

> **Need scalable hub-and-spoke connectivity among many VPCs**
>
> → **Transit Gateway**

---

# Peering vs Transit Gateway

## VPC Peering

Best for:

**Simple direct VPC-to-VPC connectivity**

## Transit Gateway

Best for:

**Many VPCs / hub-and-spoke architecture**

### Memory Trick

**Peering = 1-to-1**

**Transit Gateway = Hub**

---

# VPC Endpoints

A:

**VPC Endpoint**

allows private access to supported services without requiring:

- Internet Gateway
- NAT Gateway
- Public Internet

Architecture:

Private Subnet  
↓  
VPC Endpoint  
↓  
AWS Service

### Killer Exam Clue

> **Private resources need to access AWS services without Internet/NAT**
>
> → **VPC Endpoint**

---

# Gateway Endpoints

Gateway endpoints are used for:

- [[S3]]
- [[DynamoDB]]

They are added to:

**Route tables**

### Memory Trick

**Gateway Endpoint = S3 + DynamoDB**

---

# Interface Endpoints

Interface endpoints use:

**AWS PrivateLink**

and create:

**Elastic Network Interfaces**

inside your VPC.

They support many AWS services.

### Memory Trick

**Interface Endpoint = ENI + PrivateLink**

---

# Gateway vs Interface Endpoint

| Feature | Gateway Endpoint | Interface Endpoint |
|---|---|---|
| S3 | ✅ | Supported Alternative Patterns |
| DynamoDB | ✅ | Different Support Model |
| ENI Created | ❌ | ✅ |
| Route Table Integration | ✅ | ❌ Primary |
| PrivateLink | ❌ | ✅ |
| Hourly Cost | Generally No Endpoint Hourly Fee | Typically Yes |

### Killer Shortcut

**S3/DynamoDB**
→ Gateway Endpoint

**Most other supported AWS services**
→ Interface Endpoint

---

# PrivateLink

**AWS PrivateLink**

allows private connectivity to:

**Services through interface endpoints**

without exposing traffic to:

**The public Internet**

Architecture:

Consumer VPC  
↓  
Interface Endpoint  
↓  
PrivateLink  
↓  
Service

### Killer Exam Clue

> **Privately expose a service to many consumer VPCs without peering**
>
> → **PrivateLink**

---

# PrivateLink vs VPC Peering

## PrivateLink

Think:

**Expose a specific service privately**

## Peering

Think:

**Connect entire VPC networks**

### Killer Shortcut

**Specific service**
→ PrivateLink

**Network-to-network**
→ Peering

---

# VPC Flow Logs

[[05-Networking/VPC Flow Logs]] capture:

**Network traffic metadata**

They can be configured for:

- VPC
- Subnet
- Network interface

Useful fields include:

- Source IP
- Destination IP
- Source port
- Destination port
- Protocol
- ACCEPT / REJECT

### Killer Exam Clue

> **Troubleshoot whether network traffic was accepted or rejected**
>
> → **VPC Flow Logs**

---

# Flow Logs Do Not Capture Packet Contents

VPC Flow Logs record:

**Metadata**

They do NOT provide:

**Full packet payload inspection**

### Memory Trick

**Flow Logs = Who Talked to Whom**

Not:

**What They Said**

---

# Flow Logs Destinations

VPC Flow Logs can be delivered to supported destinations such as:

- CloudWatch Logs
- S3

This enables:

**Monitoring and analysis**

---

# VPC DNS

VPC provides built-in:

**DNS capabilities**

through Route 53 Resolver.

Important settings include concepts such as:

- DNS resolution
- DNS hostnames

These matter when instances need:

**AWS-provided DNS names**

---

# DHCP Options Set

A:

**DHCP Options Set**

can provide network configuration to instances, such as:

- DNS servers
- Domain name information

For most workloads:

**Default AWS DNS behavior is sufficient**

---

# Elastic Network Interface

An:

**Elastic Network Interface — ENI**

is a virtual:

**Network interface**

that can contain:

- Private IPv4 addresses
- IPv6 addresses
- Security Groups
- MAC address
- Public IP association depending on configuration

### Memory Trick

**ENI = Virtual Network Card**

---

# Elastic IP

An:

**Elastic IP — EIP**

is a:

**Static public IPv4 address**

It can be associated with supported AWS resources.

### Killer Exam Clue

> **Need a stable public IPv4 address**
>
> → **Elastic IP**

---

# Bastion Host

A:

**Bastion Host**

is an EC2 instance used to provide controlled administrative access to:

**Private instances**

Architecture:

Administrator  
↓  
Bastion Host in Public Subnet  
↓  
Private EC2

### Exam Principle

> Modern architectures may use Systems Manager Session Manager instead to avoid maintaining bastion hosts.

---

# Systems Manager Session Manager

[[Systems Manager]] Session Manager allows administrative access to instances without requiring:

- Public IP
- Inbound SSH
- Bastion host

### Killer Exam Clue

> **Need secure shell-like access to private EC2 without opening port 22**
>
> → **Systems Manager Session Manager**

---

# VPC + VPN

A:

**Site-to-Site VPN**

can connect:

**On-premises network**

to:

**AWS**

over:

**Encrypted Internet tunnels**

Architecture:

On-Premises  
↓  
VPN  
↓  
AWS VPC

### Memory Trick

**VPN = Encrypted Over Internet**

---

# Direct Connect

[[05-Networking/Direct Connect]] provides:

**Dedicated private connectivity**

between:

**On-premises infrastructure and AWS**

### Killer Shortcut

**Quick encrypted hybrid connection**
→ VPN

**Dedicated private network connection**
→ Direct Connect

---

# VPN + Direct Connect

Some architectures combine:

**Direct Connect**

with:

**VPN**

for additional:

- Encryption
- Backup
- Resilience

---

# Multi-Tier VPC Architecture

A common SAA architecture:

Internet  
↓  
Internet Gateway  
↓  
Public ALB  
↓  
Private Application Subnets  
↓  
Private Database Subnets

Private app servers may use:

NAT Gateway  
↓  
Internet

for outbound updates.

### Killer Exam Pattern

> **Internet-facing load balancer + private application/database tiers**
>
> → Classic highly available VPC architecture

---

# Multi-AZ Design

For high availability:

Public Subnet — AZ A  
Public Subnet — AZ B

Private App Subnet — AZ A  
Private App Subnet — AZ B

Private DB Subnet — AZ A  
Private DB Subnet — AZ B

### SAA Principle

> **Distribute critical architecture across multiple AZs**

---

# Architecture Thinking

## Scenario 1 — Public Website

Need:

Internet-facing ALB

Choose:

Public subnets  
+  
Internet Gateway

---

## Scenario 2 — Private Application Servers

Application servers should not accept:

**Direct Internet connections**

Place them in:

**Private subnets**

behind:

**ALB**

---

## Scenario 3 — Private EC2 Updates

Private EC2 needs:

**Outbound Internet access**

Choose:

**NAT Gateway**

---

## Scenario 4 — Private IPv6

IPv6 workload needs:

**Outbound Internet only**

Choose:

**Egress-Only Internet Gateway**

---

## Scenario 5 — S3 Without NAT

Private instances need S3 access without:

**NAT Gateway**

Choose:

**S3 Gateway Endpoint**

---

## Scenario 6 — Secrets Manager Without Internet

Private EC2 needs to access:

Secrets Manager

without NAT/public Internet.

Choose:

**Interface VPC Endpoint**

---

## Scenario 7 — Two VPCs

Need simple private connectivity between:

Two non-overlapping VPCs.

Choose:

**VPC Peering**

---

## Scenario 8 — Fifty VPCs

Need scalable:

**Hub-and-spoke connectivity**

Choose:

**Transit Gateway**

---

## Scenario 9 — SaaS Service Exposure

Provider wants consumers to privately access:

**One service**

without full VPC connectivity.

Choose:

**PrivateLink**

---

## Scenario 10 — Troubleshoot Rejected Traffic

Need to determine whether packets are:

**ACCEPTED or REJECTED**

Choose:

**VPC Flow Logs**

---

# Scenario Recognition

Immediately think:

**VPC**

when you see:

- Subnets
- Routing
- Private network
- Internet Gateway
- NAT Gateway
- Security Groups
- NACL
- VPC Endpoint
- Peering
- CIDR
- Hybrid connectivity

---

# Exam Traps

## Trap 1 — A Public Subnet Is Public Because It Has "Public" in Its Name

❌

It is public because its route table has:

**A route to an Internet Gateway**

---

## Trap 2 — IGW Route Alone Gives EC2 Internet Access

❌

EC2 also needs:

- Public IPv4/EIP
- Security controls permitting traffic

---

## Trap 3 — NAT Gateway Belongs in a Private Subnet

❌

A public NAT Gateway belongs in:

**A public subnet**

---

## Trap 4 — NAT Gateway Allows New Inbound Internet Connections

❌

It is used primarily for:

**Outbound connections initiated by private resources**

---

## Trap 5 — Security Groups Are Stateless

❌

Security Groups are:

**Stateful**

---

## Trap 6 — NACLs Are Stateful

❌

NACLs are:

**Stateless**

---

## Trap 7 — VPC Peering Is Transitive

❌

It is:

**Non-transitive**

---

## Trap 8 — Peered VPCs Can Have Overlapping CIDRs

❌

Standard peering requires:

**Non-overlapping CIDRs**

---

## Trap 9 — S3 Always Requires NAT From Private Subnet

❌

Use:

**Gateway VPC Endpoint**

---

## Trap 10 — Flow Logs Capture Full Packet Contents

❌

They capture:

**Traffic metadata**

---

# Quick Cheat Sheet

| Exam Clue | Answer |
|---|---|
| Isolated AWS Network | VPC |
| VPC Scope | Region |
| Subnet Scope | Availability Zone |
| Public Subnet | Route to IGW |
| Internet Access | Internet Gateway |
| Private IPv4 Outbound Internet | NAT Gateway |
| Private IPv6 Outbound Internet | Egress-Only IGW |
| Resource Firewall | Security Group |
| Subnet Firewall | NACL |
| Simple VPC-to-VPC | VPC Peering |
| Many VPCs | Transit Gateway |
| Private S3/DynamoDB | Gateway Endpoint |
| Private AWS Service Access | Interface Endpoint |
| Private Service Exposure | PrivateLink |
| Network Traffic Metadata | VPC Flow Logs |
| Static Public IPv4 | Elastic IP |
| Virtual Network Card | ENI |

---

# VPC Decision Map

Need:

**Internet-facing resource**

→ Public Subnet + IGW

Need:

**Private EC2 outbound IPv4**

→ NAT Gateway

Need:

**Private IPv6 outbound**

→ Egress-Only IGW

Need:

**S3 privately**

→ Gateway Endpoint

Need:

**Other supported AWS service privately**

→ Interface Endpoint

Need:

**Two VPCs**

→ Peering

Need:

**Many VPCs**

→ Transit Gateway

Need:

**Specific private service**

→ PrivateLink

Need:

**Traffic troubleshooting**

→ VPC Flow Logs

---

# Final Exam Rapid-Fire

> **VPC**
> → REGIONAL
>
> **SUBNET**
> → ONE AZ
>
> **PUBLIC SUBNET**
> → ROUTE TO IGW
>
> **PRIVATE IPv4 OUTBOUND**
> → NAT GATEWAY
>
> **PRIVATE IPv6 OUTBOUND**
> → EGRESS-ONLY IGW
>
> **RESOURCE FIREWALL**
> → SECURITY GROUP
>
> **SUBNET FIREWALL**
> → NACL
>
> **STATEFUL**
> → SECURITY GROUP
>
> **STATELESS**
> → NACL
>
> **2 VPCs**
> → PEERING
>
> **MANY VPCs**
> → TRANSIT GATEWAY
>
> **S3/DYNAMODB PRIVATE**
> → GATEWAY ENDPOINT
>
> **PRIVATE AWS SERVICE**
> → INTERFACE ENDPOINT
>
> **PRIVATE SERVICE EXPOSURE**
> → PRIVATELINK
>
> **NETWORK METADATA**
> → VPC FLOW LOGS

---

## Master Memory Trick

> [!tip] VPC Master Memory Trick
> Imagine a VPC is:
>
> **YOUR PRIVATE CITY**
>
> The city boundary is:
>
> **VPC CIDR**
>
> Neighborhoods are:
>
> **SUBNETS**
>
> Roads are:
>
> **ROUTE TABLES**
>
> The highway to the Internet is:
>
> **INTERNET GATEWAY**
>
> Private neighborhoods get outbound Internet through:
>
> **NAT GATEWAY**
>
> Building security guards are:
>
> **SECURITY GROUPS**
>
> Neighborhood checkpoints are:
>
> **NACLs**
>
> A private road to AWS services is:
>
> **VPC ENDPOINT**
>
> A private road to another VPC is:
>
> **VPC PEERING**
>
> The giant transportation hub connecting many cities is:
>
> **TRANSIT GATEWAY**

So remember:

> **VPC**
> → REGION
>
> **SUBNET**
> → AZ
>
> **ROUTE TABLE**
> → WHERE TRAFFIC GOES
>
> **IGW**
> → INTERNET
>
> **NAT**
> → PRIVATE GETS OUT
>
> **SECURITY GROUP**
> → RESOURCE
>
> **NACL**
> → SUBNET
>
> **ENDPOINT**
> → PRIVATE AWS ACCESS
>
> **PEERING**
> → TWO VPCs
>
> **TRANSIT GATEWAY**
> → MANY VPCs

And the killer SAA question:

> **"Does the requirement involve controlling IP addressing, routing, subnets, private connectivity, or network security inside AWS?"**
>
> YES
>
> → **VPC**

---

## Related Notes

- [[Security Groups]]
- [[NACL]]
- [[05-Networking/VPC Flow Logs]]
- [[05-Networking/Transit Gateway]]
- [[05-Networking/Direct Connect]]
- [[Systems Manager]]
- [[S3]]
- [[DynamoDB]]
- [[20-SAA/15-Security/Network Firewall]]