## What Problem Does It Solve?

[[Client VPN]] provides:

**Secure remote access for individual users and devices into AWS networks**

It is commonly used for:

- Remote employees
- Administrators
- Developers
- Contractors
- Individual client devices

Architecture:

Remote User  
↓  
Encrypted VPN Connection  
↓  
Client VPN Endpoint  
↓  
VPC Resources

> [!tip] Memory Trick
> **Client VPN = User-to-VPC VPN**

---

## Core Concept

Client VPN differs from:

[[Site-to-Site VPN]]

because Client VPN connects:

**Individual users**

rather than:

**Entire networks**

### Killer Exam Clue

> **Remote employees need secure access to resources inside a VPC**
>
> → **Client VPN**

---

# Remote Access

Client VPN allows users outside AWS to securely reach:

**Private AWS resources**

Examples:

- Private EC2 instances
- Internal applications
- Development environments
- Private databases where network and authorization controls permit

### Memory Trick

**Laptop → VPN → VPC**

---

# Client VPN Endpoint

The central AWS resource is a:

**Client VPN Endpoint**

Clients establish encrypted connections to:

**The endpoint**

Architecture:

Client Device  
↓  
Client VPN Endpoint  
↓  
Associated VPC Network  
↓  
Private Resources

---

# Managed Service

Client VPN is:

**AWS-managed**

AWS handles much of the underlying:

- VPN infrastructure
- Scaling
- Availability

This reduces the need to operate:

**Your own remote-access VPN servers**

### Killer Exam Clue

> **Need managed remote-user VPN access without maintaining VPN appliances**
>
> → **Client VPN**

---

# Secure Connectivity

Client VPN uses:

**TLS-based secure connections**

to protect traffic between:

**Client devices and AWS**

### Memory Trick

**Client VPN = Encrypted Remote Access**

---

# Target Network Association

A Client VPN endpoint must be associated with:

**Target networks**

inside a VPC.

These associations allow clients to reach:

**VPC resources**

### Exam Principle

> **Creating the endpoint alone does not automatically provide access to every VPC subnet**

---

# Routes

Client VPN uses:

**Routes**

to determine:

**Which destination networks clients can reach**

Example:

Client VPN  
↓  
Route:

`10.0.0.0/16`

→ VPC

### Killer Exam Trap

> **Client connects to VPN but cannot reach private network**
>
> → Check **Client VPN routes**

---

# Authorization Rules

Client VPN also uses:

**Authorization Rules**

to control:

**Which users can access which networks**

Example:

Developers  
→ Development CIDR

Administrators  
→ Development + Production CIDRs

### Memory Trick

**Route = Where**

**Authorization = Who**

---

# Routes vs Authorization

Both may be required.

A route says:

> **The network is reachable**

An authorization rule says:

> **The user is allowed to access it**

### Killer Exam Principle

> **Reachability and authorization are separate**

---

# Authentication

Client VPN supports authentication mechanisms for:

**Remote users**

Depending on architecture, this can include supported methods such as:

- Certificate-based authentication
- Directory-based authentication
- Federated authentication

For SAA, focus on:

> **Client VPN authenticates individual users before granting remote access**

---

# Mutual Certificate Authentication

Client VPN can use:

**Certificate-based authentication**

where certificates verify:

**Client identity**

### Exam Recognition

> **Mutual certificate authentication for remote VPN users**
>
> → **Client VPN**

---

# Active Directory Authentication

Client VPN can integrate with supported:

**Directory services**

for centralized:

**User authentication**

This is useful for organizations with:

**Enterprise user directories**

---

# Federated Authentication

Client VPN can support:

**Federated authentication**

for organizations using:

**Central identity providers**

### SAA Principle

> **Remote VPN authentication can integrate with enterprise identity systems**

---

# Security Groups

Client VPN target network associations can use:

[[Security Groups]]

to control:

**Network access**

to VPC resources.

### Killer Exam Clue

> **VPN user connects successfully but cannot reach EC2**
>
> → Check **Security Groups**

---

# NACLs

[[NACL]] rules must also permit:

**The required subnet traffic**

because NACLs operate at:

**Subnet level**

---

# DNS

Remote users may need to resolve:

**Private AWS DNS names**

through Client VPN.

DNS configuration should support:

**Private resource resolution**

### Killer Exam Clue

> **VPN users can reach private IPs but not internal hostnames**
>
> → Check **DNS configuration**

---

# Split-Tunnel

Client VPN can support:

**Split-Tunnel**

With split tunneling:

Only traffic destined for:

**Configured private networks**

goes through the VPN.

Other Internet traffic uses:

**The client's normal Internet connection**

### Memory Trick

**Split Tunnel = AWS Traffic Through VPN, Internet Traffic Stays Local**

---

# Full-Tunnel

Without split tunneling, client traffic may be routed more broadly through:

**The VPN path**

depending on configuration.

### Exam Principle

> **Choose split tunneling when only private AWS traffic should use the VPN**

---

# Split-Tunnel Benefits

Benefits can include:

- Lower VPN traffic volume
- Reduced latency for normal Internet traffic
- Less unnecessary AWS routing

### Killer Exam Clue

> **Remote users should access AWS privately but continue using their local Internet connection for normal web browsing**
>
> → **Split-Tunnel Client VPN**

---

# Client VPN vs Site-to-Site VPN

This is the most important comparison.

## Client VPN

Connects:

**Individual users/devices**

Examples:

- Employee laptop
- Administrator workstation

## [[Site-to-Site VPN]]

Connects:

**Entire networks**

Examples:

- Office network
- Data center
- Branch location

### Killer Shortcut

**User → AWS**
→ Client VPN

**Network → AWS**
→ Site-to-Site VPN

---

# Client VPN vs Direct Connect

## [[Direct Connect]]

Provides:

**Dedicated hybrid network connectivity**

## Client VPN

Provides:

**Remote user access**

### Killer Shortcut

Corporate data center  
→ AWS  
→ Direct Connect

Remote employee laptop  
→ AWS  
→ Client VPN

---

# Client VPN vs Bastion Host

## Bastion Host

Provides controlled access to:

**Specific private instances**

usually using:

**SSH/RDP**

## Client VPN

Provides network-level access to:

**Private VPC resources**

### Memory Trick

**Bastion = Jump Host**

**Client VPN = Remote Network Access**

---

# Client VPN vs Session Manager

## [[Systems Manager]] Session Manager

Provides:

**Administrative shell access**

to managed instances without:

- SSH
- Public IP
- Bastion host

## Client VPN

Provides:

**Broader private network access**

### Killer Shortcut

Need shell into EC2  
→ Session Manager

Need remote user to access internal application/network  
→ Client VPN

---

# Client VPN vs VPC Peering

## [[VPC Peering]]

Connects:

**VPC networks**

## Client VPN

Connects:

**Remote clients**

Different problems entirely.

---

# High Availability

Client VPN is:

**Managed by AWS**

and can associate with target networks across:

**Multiple Availability Zones**

for resilient access.

### SAA Principle

> **Use multiple target network associations for resilient remote-access architecture**

---

# Scaling

Client VPN can support:

**Many remote users**

without requiring you to manually manage:

**VPN server instances**

This is a key operational advantage.

---

# Logging

Client VPN connection activity can be logged for:

**Operational and security visibility**

This helps investigate:

- Connection attempts
- User access
- Troubleshooting

### Exam Principle

> **Use connection logging when auditability is required**

---

# CloudWatch Integration

Client VPN can integrate with:

[[CloudWatch]]

for monitoring:

**Operational health and connection activity**

---

# Architecture Thinking

## Scenario 1 — Remote Employees

Employees working from home need access to:

**Private internal applications in AWS**

Choose:

**Client VPN**

---

## Scenario 2 — Data Center

An entire corporate network needs:

**Encrypted connectivity to AWS**

Choose:

**Site-to-Site VPN**

not Client VPN.

---

## Scenario 3 — Dedicated Circuit

Company needs:

**Predictable dedicated hybrid bandwidth**

Choose:

**Direct Connect**

---

## Scenario 4 — Administrator Shell

One administrator needs:

**Shell access to private EC2**

without SSH exposure.

Choose:

**Systems Manager Session Manager**

rather than building VPN access solely for this requirement.

---

## Scenario 5 — Developer Network Access

Developers need access to:

- Private APIs
- Internal websites
- Private EC2 addresses

Choose:

**Client VPN**

---

## Scenario 6 — Limit Developer Access

Developers should access:

Development VPC

but not:

Production CIDR.

Use:

**Client VPN Authorization Rules**

---

## Scenario 7 — VPN Connected but No Reachability

User connects successfully but cannot access:

`10.0.2.0/24`

Check:

- Client VPN route
- Authorization rule
- Security Groups
- NACLs

---

## Scenario 8 — Normal Internet Traffic

Remote workers should use VPN only for:

**AWS private traffic**

while normal web browsing remains local.

Choose:

**Split-Tunnel**

---

# Scenario Recognition

Immediately think:

**Client VPN**

when you see:

- Remote employees
- Individual user VPN
- Laptop to VPC
- Remote administrator
- Managed remote-access VPN
- Client authentication
- Split tunnel

---

## Think Site-to-Site VPN When You See

- Office network
- Branch office
- Data center
- Network-to-network
- Customer Gateway

---

## Think Session Manager When You See

- EC2 administrative shell
- No SSH
- No public IP
- No bastion

---

## Think Direct Connect When You See

- Dedicated hybrid connectivity
- Predictable bandwidth
- Data center connectivity

---

# Exam Traps

## Trap 1 — Client VPN Connects Entire Corporate Networks

❌

Think:

**Site-to-Site VPN**

Client VPN primarily connects:

**Individual users/devices**

---

## Trap 2 — Site-to-Site VPN Is Best for Remote Employees

❌

Think:

**Client VPN**

---

## Trap 3 — Connecting to Client VPN Automatically Allows Every Private Network

❌

Check:

- Routes
- Authorization rules
- Security controls

---

## Trap 4 — Route and Authorization Rule Are the Same Thing

❌

Route:

**Where traffic can go**

Authorization:

**Who may go there**

---

## Trap 5 — Client VPN Requires You to Manage VPN EC2 Servers

❌

It is:

**AWS-managed**

---

## Trap 6 — Client VPN Is Always Necessary for EC2 Administration

❌

For shell access only:

**Session Manager**

may be simpler and more secure.

---

# Quick Cheat Sheet

| Exam Clue | Answer |
|---|---|
| Remote User → AWS | Client VPN |
| Managed Remote-Access VPN | Client VPN |
| Individual Laptop Access | Client VPN |
| Network → AWS | Site-to-Site VPN |
| Dedicated Hybrid Link | Direct Connect |
| VPN Reachability | Client VPN Route |
| User Network Permission | Authorization Rule |
| AWS-Only VPN Traffic | Split-Tunnel |
| EC2 Shell Without SSH | Session Manager |
| Resource Network Control | Security Group |

---

# VPN Decision Map

Need:

**Remote employee access**

→ Client VPN

Need:

**Office/data center connectivity**

→ Site-to-Site VPN

Need:

**Dedicated hybrid connectivity**

→ Direct Connect

Need:

**EC2 shell access only**

→ Systems Manager Session Manager

Need:

**Only AWS traffic through VPN**

→ Split-Tunnel

---

# Final Exam Rapid-Fire

> **REMOTE USER**
> → CLIENT VPN
>
> **LAPTOP → VPC**
> → CLIENT VPN
>
> **NETWORK → VPC**
> → SITE-TO-SITE VPN
>
> **DEDICATED HYBRID**
> → DIRECT CONNECT
>
> **WHERE CAN CLIENT GO?**
> → ROUTE
>
> **WHO CAN ACCESS NETWORK?**
> → AUTHORIZATION RULE
>
> **AWS TRAFFIC ONLY THROUGH VPN**
> → SPLIT-TUNNEL
>
> **EC2 SHELL WITHOUT SSH**
> → SESSION MANAGER

---

## Master Memory Trick

> [!tip] Client VPN Master Memory Trick
> Imagine AWS is:
>
> **A private corporate office**
>
> An entire branch office wants to connect.
>
> That's:
>
> **SITE-TO-SITE VPN**
>
> But one employee working from home opens:
>
> **THEIR LAPTOP**
>
> and needs secure access to:
>
> **PRIVATE AWS RESOURCES**
>
> That's:
>
> **CLIENT VPN**
>
> Once connected:
>
> **ROUTES**
>
> determine where the employee can reach.
>
> **AUTHORIZATION RULES**
>
> determine whether they're allowed to reach it.

So remember:

> **CLIENT VPN**
> → USER
>
> **SITE-TO-SITE VPN**
> → NETWORK
>
> **DIRECT CONNECT**
> → DEDICATED LINK
>
> **ROUTE**
> → WHERE
>
> **AUTHORIZATION**
> → WHO
>
> **SPLIT TUNNEL**
> → ONLY PRIVATE TRAFFIC THROUGH VPN
>
> **SESSION MANAGER**
> → EC2 ADMIN WITHOUT VPN/SSH

And the killer SAA question:

> **"Does an individual remote user or employee need secure network access to private AWS resources?"**
>
> YES
>
> → **Client VPN**

---

## Related Notes

- [[VPC]]
- [[Site-to-Site VPN]]
- [[Direct Connect]]
- [[Systems Manager]]
- [[Security Groups]]
- [[NACL]]
- [[CloudWatch]]