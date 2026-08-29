## What Problem Does It Solve?

[[VPC Peering]] provides:

**Private connectivity between two VPCs**

It allows resources in separate VPCs to communicate using:

**Private IP addresses**

Architecture:

VPC A  
↔  
VPC Peering Connection  
↔  
VPC B

> [!tip] Memory Trick
> **VPC Peering = Private 1-to-1 VPC Connection**

---

## Core Concept

A VPC Peering connection creates:

**Direct private network connectivity**

between:

**Two VPCs**

It does not require traffic to traverse:

**The public Internet**

### Killer Exam Clue

> **Need private connectivity between two VPCs with non-overlapping CIDR ranges**
>
> → **VPC Peering**

---

# Non-Overlapping CIDR Requirement

Peered VPCs must use:

**Non-overlapping IP ranges**

Example:

VPC A:

`10.0.0.0/16`

VPC B:

`10.1.0.0/16`

✅ Can peer

But:

VPC A:

`10.0.0.0/16`

VPC B:

`10.0.0.0/16`

❌ Overlapping CIDRs

### Killer Exam Clue

> **VPCs have overlapping CIDR blocks**
>
> → Standard VPC Peering is not the answer.

### Memory Trick

**Peering Needs Unique Address Space**

---

# Route Table Updates

Creating a peering connection alone does NOT automatically route traffic.

You must update:

**Route Tables**

in both VPCs.

Example:

VPC A Route Table:

`10.1.0.0/16`
→ Peering Connection

VPC B Route Table:

`10.0.0.0/16`
→ Peering Connection

### Killer Exam Trap

> **Peering exists but traffic still fails**
>
> → Check **route tables**

---

# Bidirectional Routing

Each side needs:

**A route to the other VPC**

Architecture:

VPC A  
↓  
Route to VPC B CIDR  
↓  
Peering

and:

VPC B  
↓  
Route to VPC A CIDR  
↓  
Peering

### Memory Trick

**Peering Connection + Routes = Connectivity**

---

# Security Groups

Routing alone is not enough.

Traffic must also be allowed by:

[[Security Groups]]

Example:

App in VPC A  
↓  
Peering  
↓  
Database in VPC B

Database SG must allow:

**The required traffic**

### Killer Exam Principle

> **Route tables decide where traffic goes**
>
> **Security Groups decide whether the resource accepts it**

---

# NACLs

[[NACL]] rules must also permit:

**The required subnet traffic**

Because NACLs are:

**Stateless**

remember to consider:

**Both directions**

---

# VPC Peering Is Non-Transitive

This is the single most important exam fact.

Suppose:

VPC A ↔ VPC B

and:

VPC B ↔ VPC C

Can VPC A communicate with VPC C through VPC B?

**NO**

### Killer Exam Clue

> **Need transitive connectivity across multiple VPCs**
>
> → Do NOT choose VPC Peering.
>
> Think **Transit Gateway**.

### Memory Trick

**Peering = No Transit**

---

# Non-Transitive Example

Architecture:

VPC A  
↔  
VPC B  
↔  
VPC C

This does NOT create:

VPC A  
↔  
VPC C

You would need either:

- A separate A ↔ C peering connection
- A different architecture such as [[05-Networking/Transit Gateway]]

---

# Full Mesh Problem

With a small number of VPCs:

Peering works well.

But as the number of VPCs grows:

**The number of connections grows rapidly**

Example:

3 VPCs  
→ 3 peerings for full mesh

10 VPCs  
→ Many more connections

### Killer Exam Clue

> **Need connectivity between dozens or hundreds of VPCs**
>
> → **Transit Gateway**

### Memory Trick

**Few VPCs = Peering**

**Many VPCs = Transit Gateway**

---

# VPC Peering vs Transit Gateway

## VPC Peering

Think:

- Direct
- 1-to-1
- Non-transitive
- Simple
- Few VPCs

## [[05-Networking/Transit Gateway]]

Think:

- Hub-and-spoke
- Transitive routing
- Many VPCs
- Central connectivity

### Killer Shortcut

**Two VPCs**
→ Peering

**Many VPCs**
→ Transit Gateway

---

# Same-Region Peering

VPC Peering can connect VPCs in:

**The same Region**

This is useful for:

- Separate application VPCs
- Shared-service access
- Environment separation

---

# Inter-Region VPC Peering

VPC Peering can also support:

**Inter-Region connectivity**

between VPCs in:

**Different AWS Regions**

Architecture:

VPC A — Region A  
↔  
Inter-Region Peering  
↔  
VPC B — Region B

### Killer Exam Clue

> **Need private VPC-to-VPC connectivity across Regions**
>
> → **Inter-Region VPC Peering**

---

# Inter-Region Traffic

Inter-Region peering traffic stays on:

**The AWS global network**

rather than traversing:

**The public Internet**

### Memory Trick

**Private IPs Across Regions**

---

# Cross-Account Peering

VPC Peering can connect VPCs owned by:

**Different AWS accounts**

This is useful when:

- Teams have separate accounts
- Organizations separate workloads by account

### Killer Exam Clue

> **Two AWS accounts need direct private VPC connectivity**
>
> → **Cross-Account VPC Peering**

---

# Accepter and Requester

A VPC Peering connection has:

**Requester**

and:

**Accepter**

One side creates:

**The peering request**

The other side must:

**Accept it**

### Memory Trick

**Requester Asks**

**Accepter Approves**

---

# DNS Resolution

Peered VPCs can support:

**DNS resolution behavior**

with appropriate configuration.

This can allow resources to resolve:

**Private DNS names across peered VPCs**

### Exam Principle

> **If connectivity works by IP but not hostname, check DNS configuration**

---

# VPC Peering Does Not Create Shared Security

Peering does not automatically:

- Merge Security Groups
- Merge NACLs
- Merge route tables
- Create one large VPC

Each VPC remains:

**Administratively separate**

### Memory Trick

**Connected ≠ Merged**

---

# VPC Peering vs PrivateLink

This is another important distinction.

## VPC Peering

Provides:

**Network-to-network connectivity**

Resources in both VPCs can potentially communicate according to routing and security.

## [[05-Networking/PrivateLink]]

Provides:

**Private access to a specific service**

### Killer Shortcut

**Connect entire VPC networks**
→ Peering

**Expose one service privately**
→ PrivateLink

---

# Why Choose PrivateLink Instead?

Suppose a provider wants to expose:

**One application service**

to many customer VPCs.

Using peering would create:

**Large numbers of network relationships**

Instead:

Provider Service  
↓  
PrivateLink  
↓  
Consumer Interface Endpoint

### Killer Exam Clue

> **Privately expose one service to many consumer VPCs without full network connectivity**
>
> → **PrivateLink**

---

# Peering vs Site-to-Site VPN

## VPC Peering

Connects:

**VPC to VPC**

## Site-to-Site VPN

Connects:

**On-premises network to AWS**

over:

**Encrypted Internet tunnels**

### Memory Trick

**VPC ↔ VPC**
→ Peering

**Office ↔ AWS**
→ VPN

---

# Peering vs Direct Connect

## VPC Peering

AWS private connectivity between:

**VPCs**

## [[05-Networking/Direct Connect]]

Dedicated connection between:

**On-premises and AWS**

---

# Peering and Internet Gateways

Traffic across a peering connection does NOT require:

**Internet Gateways**

because peering uses:

**Private networking**

### Killer Exam Concept

> **VPC Peering is not Internet-based connectivity**

---

# No Edge-to-Edge Routing

A peered VPC cannot generally use the other VPC as:

**A transit path to external connectivity**

Example:

VPC A  
↔  
VPC B  
↓  
Internet Gateway

VPC A cannot automatically use:

**VPC B's Internet Gateway**

through the peering connection.

### Killer Exam Trap

> **VPC Peering does not provide edge-to-edge transit**

---

# No NAT Gateway Sharing Through Peering

Similarly:

VPC A cannot simply peer to VPC B and use:

**VPC B's NAT Gateway**

as though peering were:

**A transit router**

### Memory Trick

**Peering Connects VPCs**

It does not turn one VPC into:

**A transit network**

---

# No VPN Transit

If:

VPC B has a VPN to on-premises

and:

VPC A peers with VPC B

VPC A does not automatically get:

**On-premises connectivity through B**

This is another example of:

**Non-transitive behavior**

---

# Architecture Thinking

## Scenario 1 — Two Application VPCs

App VPC:

`10.0.0.0/16`

Database VPC:

`10.1.0.0/16`

Need:

**Private direct connectivity**

Choose:

**VPC Peering**

---

## Scenario 2 — Overlapping CIDRs

VPC A:

`10.0.0.0/16`

VPC B:

`10.0.0.0/16`

Need connectivity.

Standard VPC Peering:

**Not appropriate**

because CIDRs overlap.

---

## Scenario 3 — Three VPC Transit

A peers with B.

B peers with C.

Need A to communicate with C through B.

Do NOT choose:

VPC Peering alone.

Choose:

**Transit Gateway**

or create additional direct connectivity.

---

## Scenario 4 — 50 VPCs

Company needs:

**All VPCs connected**

Avoid huge full-mesh peering.

Choose:

**Transit Gateway**

---

## Scenario 5 — Cross-Region

VPC in:

us-east-1

needs private connectivity to VPC in:

eu-west-1.

Choose:

**Inter-Region VPC Peering**

when direct VPC-to-VPC connectivity fits.

---

## Scenario 6 — Different Accounts

Shared-services account has:

A private service.

Application account needs:

Private network access.

For broad VPC connectivity:

**Cross-Account VPC Peering**

may be appropriate.

---

## Scenario 7 — One Shared Service

Provider has one application that:

100 consumer VPCs

must privately access.

Do NOT create:

100 full network peering relationships unless architecture truly requires it.

Think:

**PrivateLink**

---

## Scenario 8 — Peering Exists but No Connectivity

Peering status:

Active

but traffic fails.

Check:

1. Route tables
2. Security Groups
3. NACLs
4. CIDRs
5. DNS if hostname-based

---

# Scenario Recognition

Immediately think:

**VPC Peering**

when you see:

- Two VPCs
- Direct private connection
- Non-overlapping CIDRs
- Cross-account VPC connection
- Inter-Region private VPC connection
- 1-to-1 connectivity

---

## Think Transit Gateway When You See

- Many VPCs
- Hub-and-spoke
- Transitive routing
- Central networking

---

## Think PrivateLink When You See

- Specific service
- Many consumers
- No full network connectivity
- Private service exposure

---

# Exam Traps

## Trap 1 — VPC Peering Is Transitive

❌

It is:

**Non-transitive**

---

## Trap 2 — Overlapping VPC CIDRs Are Fine

❌

Peered VPCs require:

**Non-overlapping CIDRs**

---

## Trap 3 — Creating Peering Automatically Updates Routes

❌

You must configure:

**Route tables**

---

## Trap 4 — Peering Merges Security Groups and NACLs

❌

Each VPC keeps:

**Its own security controls**

---

## Trap 5 — VPC A Can Use VPC B's Internet Gateway Through Peering

❌

No:

**Edge-to-edge transit**

---

## Trap 6 — VPC A Can Automatically Reach On-Prem Through VPC B's VPN

❌

Peering is:

**Non-transitive**

---

## Trap 7 — Peering Is Best for Hundreds of VPCs

❌

Think:

**Transit Gateway**

---

# Quick Cheat Sheet

| Exam Clue | Answer |
|---|---|
| Direct Private VPC-to-VPC | VPC Peering |
| 1-to-1 Connectivity | VPC Peering |
| Non-Transitive | VPC Peering |
| CIDR Requirement | Non-Overlapping |
| Routes Required | Both VPC Route Tables |
| Cross-Account | Supported |
| Cross-Region | Supported |
| Many VPCs | Transit Gateway |
| Specific Private Service | PrivateLink |
| Use Peer VPC as Internet Transit | ❌ |
| Use Peer VPC as VPN Transit | ❌ |

---

# Connectivity Decision Map

Need:

**Two VPCs directly connected**

→ VPC Peering

Need:

**Many VPCs connected**

→ Transit Gateway

Need:

**Transitive routing**

→ Transit Gateway

Need:

**Specific service privately exposed**

→ PrivateLink

Need:

**On-premises encrypted connection**

→ Site-to-Site VPN

Need:

**Dedicated on-premises connection**

→ Direct Connect

---

# Final Exam Rapid-Fire

> **TWO VPCs**
> → VPC PEERING
>
> **PRIVATE VPC-TO-VPC**
> → PEERING
>
> **NON-TRANSITIVE**
> → VPC PEERING
>
> **OVERLAPPING CIDR**
> → NO STANDARD PEERING
>
> **ROUTES**
> → REQUIRED ON BOTH SIDES
>
> **CROSS-ACCOUNT**
> → SUPPORTED
>
> **INTER-REGION**
> → SUPPORTED
>
> **MANY VPCs**
> → TRANSIT GATEWAY
>
> **TRANSITIVE**
> → TRANSIT GATEWAY
>
> **SPECIFIC PRIVATE SERVICE**
> → PRIVATELINK
>
> **PEER'S IGW/NAT/VPN AS TRANSIT**
> → NO

---

## Master Memory Trick

> [!tip] VPC Peering Master Memory Trick
> Imagine two private neighborhoods:
>
> **VPC A**
>
> and:
>
> **VPC B**
>
> They build:
>
> **A PRIVATE ROAD DIRECTLY BETWEEN THEM**
>
> That's:
>
> **VPC PEERING**
>
> But the road connects only:
>
> **A ↔ B**
>
> If B also has a road to:
>
> **VPC C**
>
> A cannot simply drive:
>
> **A → B → C**
>
> because peering does not provide:
>
> **TRANSIT**

So remember:

> **PEERING**
> → DIRECT
>
> **CIDRs**
> → MUST NOT OVERLAP
>
> **ROUTES**
> → MUST BE ADDED
>
> **TRANSITIVE**
> → NO
>
> **TWO VPCs**
> → PEERING
>
> **MANY VPCs**
> → TRANSIT GATEWAY
>
> **ONE SERVICE**
> → PRIVATELINK

And the killer SAA question:

> **"Do two non-overlapping VPCs need direct private connectivity without a requirement for transitive routing?"**
>
> YES
>
> → **VPC Peering**

---

## Related Notes

- [[VPC]]
- [[05-Networking/Transit Gateway]]
- [[05-Networking/PrivateLink]]
- [[Security Groups]]
- [[NACL]]
- [[05-Networking/Direct Connect]]