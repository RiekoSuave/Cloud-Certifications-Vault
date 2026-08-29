## What Problem Does It Solve?

[[Transit Gateway]] provides:

**Centralized connectivity between many VPCs and on-premises networks**

Instead of creating many individual connections:

VPC A ↔ VPC B  
VPC A ↔ VPC C  
VPC B ↔ VPC C

you create:

VPC A  
↓  
Transit Gateway  
↑  
VPC B  
↑  
VPC C

> [!tip] Memory Trick
> **Transit Gateway = Network Hub**

---

## Core Concept

Transit Gateway acts as:

**A regional network transit hub**

It can connect:

- Multiple VPCs
- Site-to-Site VPNs
- Direct Connect connectivity through supported integration
- Transit Gateways in other Regions through peering

### Killer Exam Clue

> **Need centralized connectivity between many VPCs and hybrid networks**
>
> → **Transit Gateway**

---

# Hub-and-Spoke Architecture

Transit Gateway commonly uses:

**Hub-and-spoke**

Architecture:

VPC A  
↓  
&nbsp;&nbsp;&nbsp;&nbsp;Transit Gateway  
↑ &nbsp;&nbsp;&nbsp;&nbsp;↑  
VPC B &nbsp;&nbsp; VPC C

Each VPC connects to:

**The central Transit Gateway**

instead of maintaining:

**A full mesh of peerings**

### Memory Trick

**Many Spokes → One Hub**

---

# Why Transit Gateway?

Imagine:

50 VPCs

need to communicate.

Using VPC Peering could require:

**Large numbers of individual peering relationships**

Transit Gateway simplifies this to:

VPCs  
↓  
Central Transit Gateway  
↓  
Routing

### Killer Exam Clue

> **Simplify a complex full-mesh VPC peering architecture**
>
> → **Transit Gateway**

---

# Transit Gateway Attachments

Networks connect to Transit Gateway using:

**Attachments**

Common attachment types include:

- VPC attachments
- VPN attachments
- Transit Gateway peering attachments

### Memory Trick

**Attachment = Plug Into the Hub**

---

# VPC Attachment

A:

**VPC Attachment**

connects a VPC to:

**Transit Gateway**

Architecture:

VPC  
↓  
TGW Attachment  
↓  
Transit Gateway

---

# Transit Gateway Routing

Transit Gateway has its own:

**Route Tables**

These determine:

**Which attachments can communicate**

Example:

TGW Route Table:

`10.1.0.0/16`
→ VPC B Attachment

`10.2.0.0/16`
→ VPC C Attachment

### Memory Trick

**TGW Route Table = Hub's Traffic Map**

---

# VPC Route Tables Still Matter

Connecting a VPC to Transit Gateway is not enough.

The VPC's:

**Route Tables**

must direct appropriate traffic toward:

**Transit Gateway**

Example:

VPC A route:

`10.1.0.0/16`
→ Transit Gateway

### Killer Exam Trap

> **Transit Gateway attachment exists but VPC cannot communicate**
>
> → Check both **VPC routes and TGW routes**

---

# Transitive Routing

This is one of the biggest differences from:

[[VPC Peering]]

Transit Gateway supports:

**Transitive routing**

Example:

VPC A  
↓  
Transit Gateway  
↓  
VPC B

and:

VPC A  
↓  
Transit Gateway  
↓  
VPC C

The Transit Gateway acts as:

**The routing hub**

### Killer Exam Clue

> **Need transitive routing among VPCs**
>
> → **Transit Gateway**

### Memory Trick

**Peering = No Transit**

**Transit Gateway = Transit**

---

# Transit Gateway vs VPC Peering

## [[VPC Peering]]

Think:

- Direct 1-to-1
- Non-transitive
- Simple
- Few VPCs

## Transit Gateway

Think:

- Hub-and-spoke
- Transitive
- Central routing
- Many VPCs

### Killer Shortcut

**Two VPCs**
→ VPC Peering

**Many VPCs**
→ Transit Gateway

---

# Full-Mesh Problem

With VPC Peering:

Every VPC may need connections to:

**Every other VPC**

As the environment grows:

**Complexity explodes**

Transit Gateway changes:

Many-to-many peering

into:

**Hub-and-spoke**

### Memory Trick

**Peering = Spiderweb**

**Transit Gateway = Wheel Hub**

---

# Network Segmentation

Transit Gateway route tables can create:

**Network segmentation**

Example:

Production VPCs  
→ Production TGW Route Table

Development VPCs  
→ Development TGW Route Table

Shared Services VPC  
→ Accessible by both

### Killer Exam Clue

> **Need centralized connectivity but isolate production from development**
>
> → **Transit Gateway Route Tables**

---

# Multiple Route Tables

A Transit Gateway can use:

**Multiple route tables**

to control:

**Which attachments communicate**

This allows architectures such as:

Production  
↓  
Shared Services

Development  
↓  
Shared Services

but:

Production  
❌  
Development

### Memory Trick

**Same Hub Does Not Mean Everyone Can Talk**

---

# Route Propagation

Transit Gateway attachments can:

**Propagate routes**

into Transit Gateway route tables.

This helps simplify:

**Route management**

### Killer Exam Concept

> **Attachments can advertise routes into TGW route tables through propagation**

---

# Static Routes

Transit Gateway route tables can also contain:

**Static routes**

These explicitly direct traffic toward:

**Specific attachments**

---

# Blackhole Routes

A route can be configured as:

**Blackhole**

Traffic matching that route is:

**Dropped**

### Killer Exam Clue

> **Need to intentionally prevent certain routed traffic**
>
> → **Transit Gateway blackhole route**

---

# Transit Gateway + Site-to-Site VPN

Transit Gateway can serve as the AWS-side hub for:

**Site-to-Site VPN connectivity**

Architecture:

On-Premises  
↓  
Site-to-Site VPN  
↓  
Transit Gateway  
↓  
Multiple VPCs

### Killer Exam Clue

> **On-premises network needs VPN connectivity to many VPCs**
>
> → **VPN + Transit Gateway**

### Memory Trick

**One VPN Hub → Many VPCs**

---

# Why TGW Helps Hybrid Networking

Without Transit Gateway:

On-Prem  
↓  
VPN  
↓  
VPC A

On-Prem  
↓  
VPN  
↓  
VPC B

On-Prem  
↓  
VPN  
↓  
VPC C

With Transit Gateway:

On-Prem  
↓  
VPN  
↓  
Transit Gateway  
↓  
All Required VPCs

---

# Transit Gateway + Direct Connect

Transit Gateway can integrate with:

[[05-Networking/Direct Connect]]

through:

**Direct Connect Gateway**

Architecture:

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

> **Dedicated on-premises connectivity to many VPCs**
>
> → **Direct Connect + Direct Connect Gateway + Transit Gateway**

---

# Transit Gateway + Network Firewall

A very important centralized security architecture:

Spoke VPCs  
↓  
Transit Gateway  
↓  
Inspection VPC  
↓  
[[20-SAA/15-Security/Network Firewall]]  
↓  
Destination

This allows:

**Centralized traffic inspection**

### Killer Exam Clue

> **Inspect traffic centrally for many VPCs**
>
> → **Transit Gateway + Network Firewall**

### Memory Trick

**TGW = Connect**

**Network Firewall = Inspect**

---

# Inspection VPC

Organizations may create a dedicated:

**Inspection VPC**

containing security appliances or:

**Network Firewall**

Transit Gateway routes traffic through:

**The inspection architecture**

before it reaches:

**Its destination**

---

# Appliance Mode

Stateful network appliances require traffic to maintain:

**Consistent bidirectional paths**

Transit Gateway provides:

**Appliance Mode**

for supported VPC attachment architectures.

This helps preserve:

**Flow symmetry**

through stateful appliances.

### Killer Exam Clue

> **Stateful firewall behind Transit Gateway requires symmetric routing**
>
> → Consider **Appliance Mode**

### Memory Trick

**Stateful Appliance → Same Path**

---

# Transit Gateway Peering

Transit Gateways in different Regions can connect using:

**Transit Gateway Peering**

Architecture:

Region A  
Transit Gateway  
↓  
TGW Peering  
↓  
Transit Gateway  
Region B

### Killer Exam Clue

> **Need centralized inter-Region network connectivity between Transit Gateway environments**
>
> → **Transit Gateway Peering**

---

# Inter-Region Architecture

Example:

US VPCs  
↓  
US Transit Gateway  
↓  
TGW Peering  
↓  
EU Transit Gateway  
↓  
EU VPCs

This provides:

**Private inter-Region network connectivity**

---

# Transit Gateway vs Inter-Region VPC Peering

## Inter-Region VPC Peering

Best for:

**Direct connectivity between individual VPCs**

## Transit Gateway Peering

Best for:

**Connecting larger regional network hubs**

### Killer Shortcut

**VPC ↔ VPC**
→ Inter-Region VPC Peering

**Hub ↔ Hub**
→ Transit Gateway Peering

---

# Transit Gateway vs PrivateLink

## [[PrivateLink]]

Think:

**Expose one specific service**

## Transit Gateway

Think:

**Connect networks**

### Killer Shortcut

Many VPCs need one API  
→ PrivateLink

Many VPCs need broad network connectivity  
→ Transit Gateway

---

# Transit Gateway vs VPC Endpoint

## [[VPC Endpoints]]

Think:

**Private AWS service access**

## Transit Gateway

Think:

**Network-to-network connectivity**

### Memory Trick

**Endpoint = Service**

**TGW = Networks**

---

# Transit Gateway vs VPN

## Site-to-Site VPN

Provides:

**Encrypted network connection**

## Transit Gateway

Provides:

**Central routing hub**

They can work:

**Together**

### Killer Shortcut

Encrypted tunnel  
→ VPN

Central routing  
→ Transit Gateway

---

# Transit Gateway vs Direct Connect

## Direct Connect

Provides:

**Dedicated physical connectivity**

## Transit Gateway

Provides:

**Centralized network routing**

Again:

They can be:

**Combined**

---

# Cross-Account Sharing

Transit Gateway can be shared across:

**Multiple AWS accounts**

using:

**AWS Resource Access Manager — RAM**

### Killer Exam Clue

> **Multiple AWS accounts need to use one centrally managed Transit Gateway**
>
> → **Transit Gateway + RAM**

---

# AWS Organizations Architecture

Large organizations often use:

**A dedicated networking account**

Architecture:

Networking Account  
↓  
Transit Gateway  
↓  
RAM  
↓  
Application Accounts

This allows:

**Centralized network administration**

### Memory Trick

**Networking Account Owns the Hub**

---

# Transit Gateway Bandwidth

Transit Gateway is:

**AWS-managed**

and designed to scale for:

**Large network architectures**

This removes the need to manage:

**Your own transit routers**

---

# Multicast

Transit Gateway supports:

**Multicast**

for supported architectures.

### Exam Recognition

> **Need AWS VPC multicast networking**
>
> → **Transit Gateway**

This is a less common but recognizable:

**SAA exam clue**

---

# Architecture Thinking

## Scenario 1 — 100 VPCs

Company has:

100 VPCs

that need:

**Centralized connectivity**

Choose:

**Transit Gateway**

---

## Scenario 2 — Two VPCs

Only:

Two VPCs

need simple private connectivity.

Choose:

**VPC Peering**

when appropriate.

---

## Scenario 3 — Transitive Routing

VPC A must reach:

VPC B and VPC C

through:

**A central router**

Choose:

**Transit Gateway**

---

## Scenario 4 — Hybrid Network

On-premises data center needs:

**VPN access to 30 VPCs**

Choose:

Site-to-Site VPN  
↓  
Transit Gateway  
↓  
VPCs

---

## Scenario 5 — Dedicated Hybrid Connection

Company needs:

**Direct Connect connectivity to many VPCs**

Choose:

Direct Connect  
↓  
Direct Connect Gateway  
↓  
Transit Gateway

---

## Scenario 6 — Central Firewall

All VPC traffic must pass through:

**Central security inspection**

Choose:

Transit Gateway  
↓  
Inspection VPC  
↓  
Network Firewall

---

## Scenario 7 — Production Isolation

Production and development attach to:

**Same Transit Gateway**

but must not communicate.

Use:

**Separate Transit Gateway Route Tables**

---

## Scenario 8 — Multiple Accounts

Networking team owns:

Transit Gateway.

Application teams in other accounts need to attach VPCs.

Use:

**Resource Access Manager**

---

## Scenario 9 — Multiple Regions

Regional network hubs need:

**Private connectivity**

Choose:

**Transit Gateway Peering**

---

# Scenario Recognition

Immediately think:

**Transit Gateway**

when you see:

- Many VPCs
- Hub-and-spoke
- Transitive routing
- Central router
- Hybrid networking hub
- Centralized inspection
- Multi-account networking
- TGW route tables
- Network segmentation

---

## Think VPC Peering When You See

- Two VPCs
- Direct connectivity
- Non-transitive
- Simple architecture

---

## Think PrivateLink When You See

- One service
- Many consumers
- No broad network access

---

## Think Direct Connect When You See

- Dedicated on-premises connection
- Predictable private hybrid connectivity

---

# Exam Traps

## Trap 1 — Transit Gateway Is Non-Transitive

❌

That describes:

**VPC Peering**

Transit Gateway supports:

**Transitive routing**

---

## Trap 2 — Every VPC Must Peer With Every Other VPC

❌

Transit Gateway eliminates the need for:

**Full-mesh peering**

---

## Trap 3 — Connecting a VPC Automatically Fixes All Routing

❌

Check:

- VPC route tables
- Transit Gateway route tables
- Attachments
- Security controls

---

## Trap 4 — Everyone Attached to TGW Must Communicate

❌

TGW route tables can provide:

**Segmentation**

---

## Trap 5 — Transit Gateway Replaces Direct Connect

❌

Direct Connect:

**Connectivity**

Transit Gateway:

**Routing hub**

They can work together.

---

## Trap 6 — Transit Gateway Replaces Network Firewall

❌

Transit Gateway:

**Routes**

Network Firewall:

**Inspects**

---

## Trap 7 — Transit Gateway Is Best for Exposing One Service

❌

Think:

**PrivateLink**

---

# Quick Cheat Sheet

| Exam Clue | Answer |
|---|---|
| Many VPCs | Transit Gateway |
| Hub-and-Spoke | Transit Gateway |
| Transitive Routing | Transit Gateway |
| Central Network Hub | Transit Gateway |
| Two Simple VPCs | VPC Peering |
| One Private Service | PrivateLink |
| Central Inspection | TGW + Network Firewall |
| Many VPCs + VPN | VPN + TGW |
| Direct Connect to Many VPCs | DX Gateway + TGW |
| Multi-Account TGW | RAM |
| Network Segmentation | TGW Route Tables |
| Inter-Region Hubs | TGW Peering |
| Stateful Appliance Symmetry | Appliance Mode |
| Multicast | Transit Gateway |

---

# Connectivity Decision Map

Need:

**Two VPCs**

→ VPC Peering

Need:

**Many VPCs**

→ Transit Gateway

Need:

**Transitive routing**

→ Transit Gateway

Need:

**One private service**

→ PrivateLink

Need:

**Many VPCs + on-premises VPN**

→ VPN + Transit Gateway

Need:

**Dedicated hybrid connectivity**

→ Direct Connect

Need:

**Central VPC traffic inspection**

→ Transit Gateway + Network Firewall

---

# Final Exam Rapid-Fire

> **MANY VPCs**
> → TRANSIT GATEWAY
>
> **HUB-AND-SPOKE**
> → TRANSIT GATEWAY
>
> **TRANSITIVE ROUTING**
> → TRANSIT GATEWAY
>
> **TWO VPCs**
> → VPC PEERING
>
> **ONE SERVICE**
> → PRIVATELINK
>
> **NETWORK SEGMENTATION**
> → TGW ROUTE TABLES
>
> **MULTI-ACCOUNT TGW**
> → RAM
>
> **VPN TO MANY VPCs**
> → VPN + TGW
>
> **DIRECT CONNECT TO MANY VPCs**
> → DX GATEWAY + TGW
>
> **CENTRAL FIREWALL**
> → TGW + NETWORK FIREWALL
>
> **INTER-REGION HUBS**
> → TGW PEERING
>
> **STATEFUL APPLIANCE**
> → APPLIANCE MODE
>
> **MULTICAST**
> → TRANSIT GATEWAY

---

## Master Memory Trick

> [!tip] Transit Gateway Master Memory Trick
> Imagine AWS contains:
>
> **50 CITIES**
>
> Each city is:
>
> **A VPC**
>
> With VPC Peering, you build:
>
> **A ROAD BETWEEN EVERY PAIR OF CITIES**
>
> Eventually you get:
>
> **A GIANT SPIDERWEB**
>
> Instead, build:
>
> **ONE CENTRAL HIGHWAY INTERCHANGE**
>
> Every city connects to:
>
> **THE HUB**
>
> That's:
>
> **TRANSIT GATEWAY**
>
> The hub can also connect:
>
> **ON-PREMISES**
>
> through VPN or Direct Connect.
>
> And traffic can be routed through:
>
> **A CENTRAL FIREWALL**

So remember:

> **PEERING**
> → DIRECT ROAD
>
> **TRANSIT GATEWAY**
> → CENTRAL HUB
>
> **TGW ROUTE TABLE**
> → WHO CAN TALK
>
> **VPN**
> → ENCRYPTED HYBRID CONNECTION
>
> **DIRECT CONNECT**
> → DEDICATED HYBRID CONNECTION
>
> **NETWORK FIREWALL**
> → CENTRAL INSPECTION
>
> **RAM**
> → SHARE THE HUB

And the killer SAA question:

> **"Does the architecture need scalable, centralized, transitive connectivity between many VPCs and/or on-premises networks?"**
>
> YES
>
> → **Transit Gateway**

---

## Related Notes

- [[VPC]]
- [[VPC Peering]]
- [[PrivateLink]]
- [[VPC Endpoints]]
- [[20-SAA/15-Security/Network Firewall]]
- [[05-Networking/Direct Connect]]
- [[Security Groups]]
- [[NACL]]