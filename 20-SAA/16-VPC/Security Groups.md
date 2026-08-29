## What Problem Does It Solve?

[[Security Groups]] provide:

**Stateful network access control for AWS resources**

They control:

- Inbound traffic
- Outbound traffic
- Allowed ports
- Allowed protocols
- Allowed sources and destinations

They are commonly associated with:

- EC2
- ENIs
- Load balancers
- RDS
- Other supported resources

Architecture:

Traffic  
↓  
Security Group Rules  
↓  
Allowed?  
↓  
Resource

> [!tip] Memory Trick
> **Security Group = Stateful Firewall Around a Resource**

---

## Core Concept

Security Groups operate at the:

**Resource / Elastic Network Interface level**

They use:

**Allow rules only**

and are:

**Stateful**

### Killer Exam Clue

> **Need to control which IPs or resources can reach an EC2 instance**
>
> → **Security Group**

---

# Stateful

Security Groups are:

**Stateful**

This means:

If traffic is allowed in one direction:

**Return traffic is automatically allowed**

Example:

Client  
↓  
Inbound HTTPS Allowed  
↓  
EC2

Return traffic:

EC2  
↓  
Client

is automatically allowed.

### Memory Trick

**Stateful = Remembers the Connection**

---

# Inbound Rules

Inbound rules control:

**Traffic entering the resource**

Examples:

- TCP 443 from Internet
- TCP 22 from bastion host
- TCP 3306 from application servers

### Killer Exam Clue

> **Allow HTTPS traffic to EC2**
>
> → Add inbound rule for **TCP 443**

---

# Outbound Rules

Outbound rules control:

**Traffic leaving the resource**

Example:

Application server  
↓  
Outbound HTTPS  
↓  
External API

### Exam Principle

> **Inbound and outbound rules are separate**

---

# Allow Rules Only

Security Groups support:

**Allow rules**

They do NOT support:

**Explicit deny rules**

### Killer Exam Trap

> **Need explicit deny at subnet level**
>
> → Think **NACL**

### Memory Trick

**Security Group = Allow**

**NACL = Allow + Deny**

---

# Default Security Group

Every VPC has a:

**Default Security Group**

Resources associated with it can communicate according to:

**Its default rules**

For production architecture, it is usually better to use:

**Purpose-built Security Groups**

rather than relying heavily on:

**The default group**

---

# Security Group References

One of the most important features is:

**Referencing another Security Group**

instead of using:

**IP addresses**

Example:

ALB Security Group  
↓  
Application Security Group

Rule:

Allow TCP 80  
From:

**ALB Security Group**

### Killer Exam Clue

> **Only application traffic from the load balancer should reach EC2**
>
> → Reference the **ALB Security Group**

---

# Why Reference Security Groups?

Security Group references are better than hardcoded IPs when:

- Instances scale dynamically
- Private IPs change
- Auto Scaling adds/removes instances

### Memory Trick

**Reference the Role, Not the IP**

---

# Classic Three-Tier Pattern

A very important architecture:

Internet  
↓  
ALB Security Group  
↓  
Application Security Group  
↓  
Database Security Group

Example rules:

ALB SG  
→ Allow HTTPS from Internet

App SG  
→ Allow application port from ALB SG

DB SG  
→ Allow database port from App SG

### Killer Exam Pattern

> **Use Security Group references between application tiers**

---

# Web Tier

Example:

ALB Security Group

Inbound:

TCP 443  
From:

`0.0.0.0/0`

This allows:

**Public HTTPS**

---

# Application Tier

Application Security Group:

Inbound:

TCP 8080  
From:

**ALB Security Group**

This prevents:

**Direct Internet access to application instances**

---

# Database Tier

Database Security Group:

Inbound:

TCP 3306  
From:

**Application Security Group**

This ensures:

**Only application servers can connect to the database**

### Memory Trick

**Internet → ALB → App → DB**

Each layer trusts:

**Only the layer before it**

---

# Security Group IDs

Security Groups are identified by:

**Security Group IDs**

Example:

`sg-0123456789abcdef0`

Rules can reference:

**Other Security Group IDs**

within supported networking relationships.

---

# Multiple Security Groups

A resource can often have:

**Multiple Security Groups**

attached.

The effective permissions are:

**The union of all allow rules**

### Killer Exam Concept

> **Security Groups do not override each other with deny rules**

If any attached Security Group allows traffic:

**That traffic is allowed**

subject to other controls.

---

# No Rule Priority

Security Group rules do NOT use:

**Numbered priority evaluation**

There is no:

- Rule 100 first
- Rule 200 second

All applicable allow rules are considered.

### Memory Trick

**Security Groups = No Rule Order**

---

# Security Groups and Ports

Common examples:

HTTP  
→ TCP 80

HTTPS  
→ TCP 443

SSH  
→ TCP 22

RDP  
→ TCP 3389

MySQL  
→ TCP 3306

PostgreSQL  
→ TCP 5432

### Exam Principle

> **Match the required application protocol and port**

---

# Source CIDR

A rule can allow traffic from:

**CIDR blocks**

Example:

TCP 443  
From:

`0.0.0.0/0`

means:

**Anywhere on IPv4 Internet**

---

# IPv6

IPv6 rules can use CIDRs such as:

`::/0`

which means:

**Anywhere on IPv6 Internet**

### Killer Exam Trap

> `0.0.0.0/0` = all IPv4
>
> `::/0` = all IPv6

---

# Least Privilege

Security Group design should follow:

**Least privilege**

Bad:

SSH 22  
From:

`0.0.0.0/0`

Better:

SSH 22  
From:

**Administrator's trusted IP**

Even better when appropriate:

Use:

[[Systems Manager]] Session Manager

instead of opening:

**Port 22**

---

# Security Group + Systems Manager

A common secure administration pattern:

Administrator  
↓  
Systems Manager Session Manager  
↓  
Private EC2

No need for:

- Public IP
- Bastion host
- Inbound SSH

### Killer Exam Clue

> **Need administrative access without exposing port 22**
>
> → **Systems Manager Session Manager**

---

# Security Group + ALB

[[Application Load Balancer]] has its own:

**Security Group**

A common architecture:

Internet  
↓  
ALB SG  
↓  
ALB  
↓  
EC2 SG

EC2 SG allows:

**Only ALB SG**

### Killer Exam Clue

> **Backend EC2 should only accept traffic from ALB**
>
> → Security Group reference

---

# Security Group + RDS

[[RDS]] can use:

**Security Groups**

Example:

RDS Security Group

Inbound:

TCP 5432  
From:

**Application Security Group**

This prevents:

**Arbitrary clients**

from reaching the database.

---

# Security Group + Lambda

Lambda functions attached to a VPC use:

**Elastic Network Interfaces**

and can be associated with:

**Security Groups**

This controls:

**The Lambda function's network access inside the VPC**

---

# Security Group + VPC Endpoints

Interface VPC endpoints create:

**ENIs**

and use:

**Security Groups**

to control access to:

**The endpoint**

### Killer Exam Clue

> **Need to restrict which VPC resources can connect to an interface endpoint**
>
> → Endpoint Security Group

---

# Security Group vs NACL

This comparison is critical.

## Security Group

Think:

- Resource/ENI level
- Stateful
- Allow only
- No rule order
- Automatic return traffic

## [[NACL]]

Think:

- Subnet level
- Stateless
- Allow + deny
- Numbered rule order
- Return traffic must be explicitly allowed

### Memory Trick

**SG = Stateful Resource**

**NACL = Stateless Subnet**

---

# Security Group vs WAF

## [[WAF]]

Think:

**HTTP application-layer inspection**

## Security Group

Think:

**IP / port / protocol access**

### Killer Shortcut

SQL injection  
→ WAF

Allow TCP 443  
→ Security Group

---

# Security Group vs Network Firewall

## [[20-SAA/15-Security/Network Firewall]]

Think:

**Advanced VPC traffic inspection**

## Security Group

Think:

**Basic resource-level access control**

### Killer Shortcut

Allow app server to reach database  
→ Security Group

Inspect traffic for intrusion signatures  
→ Network Firewall

---

# Security Group vs Shield

## [[Shield]]

Think:

**DDoS protection**

## Security Group

Think:

**Network access rules**

They solve:

**Different problems**

---

# Security Group vs IAM

## [[IAM]]

Controls:

**Who can call AWS APIs**

## Security Group

Controls:

**What network traffic can reach a resource**

### Memory Trick

**IAM = Identity Access**

**Security Group = Network Access**

---

# Connection Tracking

Because Security Groups are stateful, they maintain:

**Connection tracking**

This allows return traffic for established sessions.

### Example

Inbound request:

Client → EC2:443

Allowed.

Return:

EC2 → Client ephemeral port

Automatically allowed.

---

# Rule Changes

Changes to Security Group rules are generally:

**Applied automatically**

to associated resources.

You usually do not need to:

**Restart EC2 instances**

for rule changes to take effect.

### Killer Exam Clue

> **Need to change EC2 network access without restarting the instance**
>
> → Modify Security Group

---

# Shared Security Groups

In some multi-VPC architectures using supported capabilities, Security Groups can participate in:

**Cross-resource connectivity patterns**

For SAA, focus primarily on:

**Security Group references and least privilege**

rather than memorizing every edge case.

---

# Architecture Thinking

## Scenario 1 — Public HTTPS

Internet users need:

**HTTPS access**

to an ALB.

Choose:

ALB Security Group:

TCP 443  
From:

`0.0.0.0/0`

---

## Scenario 2 — Backend Protection

EC2 instances should only receive traffic from:

**The ALB**

Choose:

EC2 Security Group:

Application Port  
From:

**ALB Security Group**

---

## Scenario 3 — Database Isolation

RDS should only accept connections from:

**Application servers**

Choose:

RDS Security Group:

DB Port  
From:

**Application Security Group**

---

## Scenario 4 — Block Specific IP

Need to explicitly deny:

**One malicious IP**

Security Group cannot create:

**Deny rule**

Think:

**NACL**

or another appropriate filtering service.

---

## Scenario 5 — SSH Administration

Only office IP should access:

EC2 port 22.

Choose:

Security Group:

TCP 22  
From:

**Office CIDR**

---

## Scenario 6 — No SSH Exposure

Need administrative access without:

**Opening port 22**

Choose:

**Systems Manager Session Manager**

---

## Scenario 7 — Return Traffic

Inbound HTTPS request is allowed.

Do you need a separate outbound rule specifically for the client's ephemeral port because of the inbound connection?

Security Group is:

**Stateful**

so return traffic is automatically allowed.

---

## Scenario 8 — Two Attached Security Groups

SG A allows:

TCP 443

SG B does not contain:

TCP 443

Is TCP 443 allowed?

YES.

Effective permissions are:

**Union of allow rules**

---

# Scenario Recognition

Immediately think:

**Security Groups**

when you see:

- EC2 inbound/outbound
- Stateful firewall
- Resource-level network access
- Allow ports
- Security Group reference
- ALB → EC2
- App → DB
- ENI access

---

## Think NACL When You See

- Explicit deny
- Subnet filtering
- Stateless
- Numbered rules

---

## Think WAF When You See

- SQL injection
- XSS
- HTTP inspection

---

## Think Network Firewall When You See

- Intrusion prevention
- Advanced VPC inspection
- Suricata

---

# Exam Traps

## Trap 1 — Security Groups Are Stateless

❌

They are:

**Stateful**

---

## Trap 2 — Security Groups Support Explicit Deny Rules

❌

They support:

**Allow rules only**

---

## Trap 3 — Security Groups Apply at Subnet Level

❌

Think:

**NACL**

Security Groups apply to:

**Resources / ENIs**

---

## Trap 4 — Rule Order Matters

❌

Security Group rules do not use:

**Numbered priority evaluation**

---

## Trap 5 — Return Traffic Requires Explicit Matching Rule

❌

Because Security Groups are:

**Stateful**

return traffic is automatically allowed.

---

## Trap 6 — Hardcode EC2 IPs Behind an ALB

❌

Better:

**Reference the ALB Security Group**

---

## Trap 7 — Multiple Security Groups Can Deny Each Other

❌

There are no deny rules.

Effective permissions are:

**Combined allow rules**

---

# Quick Cheat Sheet

| Exam Clue | Answer |
|---|---|
| Resource Firewall | Security Group |
| Stateful | Security Group |
| Allow Rules Only | Security Group |
| Explicit Deny | NACL |
| ALB → EC2 | Security Group Reference |
| App → Database | Security Group Reference |
| Return Traffic | Automatically Allowed |
| Rule Order | None |
| Multiple SGs | Union of Allow Rules |
| Subnet Firewall | NACL |
| SQL Injection | WAF |
| Advanced VPC Inspection | Network Firewall |

---

# Security Group Decision Map

Need:

**Allow traffic to EC2**

→ Security Group

Need:

**Only ALB can reach EC2**

→ Reference ALB Security Group

Need:

**Only App can reach DB**

→ Reference App Security Group

Need:

**Explicit deny**

→ NACL

Need:

**HTTP attack inspection**

→ WAF

Need:

**Advanced network inspection**

→ Network Firewall

---

# Three-Tier Security Map

> **INTERNET**
> ↓
> **ALB SECURITY GROUP**
> → Allow 443 from Internet
> ↓
> **APP SECURITY GROUP**
> → Allow app port from ALB SG
> ↓
> **DB SECURITY GROUP**
> → Allow DB port from App SG

### Master Rule

> **Each tier trusts only the tier that needs to talk to it**

---

# Final Exam Rapid-Fire

> **RESOURCE FIREWALL**
> → SECURITY GROUP
>
> **STATEFUL**
> → SECURITY GROUP
>
> **ALLOW ONLY**
> → SECURITY GROUP
>
> **EXPLICIT DENY**
> → NACL
>
> **ALB → EC2**
> → SG REFERENCE
>
> **APP → DB**
> → SG REFERENCE
>
> **RETURN TRAFFIC**
> → AUTOMATICALLY ALLOWED
>
> **RULE PRIORITY**
> → NONE
>
> **MULTIPLE SECURITY GROUPS**
> → UNION OF ALLOW RULES
>
> **SUBNET FIREWALL**
> → NACL
>
> **WEB ATTACK**
> → WAF
>
> **ADVANCED VPC INSPECTION**
> → NETWORK FIREWALL

---

## Master Memory Trick

> [!tip] Security Groups Master Memory Trick
> Imagine every AWS resource has:
>
> **A PERSONAL SECURITY GUARD**
>
> The guard has a list saying:
>
> **WHO IS ALLOWED IN**
>
> and:
>
> **WHERE THE RESOURCE MAY GO**
>
> The guard can say:
>
> **YES**
>
> but does not have:
>
> **DENY RULES**
>
> Once the guard lets someone inside:
>
> it remembers the conversation.
>
> Return traffic is:
>
> **AUTOMATICALLY ALLOWED**
>
> That's why the guard is:
>
> **STATEFUL**
>
> And instead of saying:
>
> **"Allow IP 10.0.1.15"**
>
> you can say:
>
> **"Allow anyone wearing the ALB SECURITY GROUP badge."**

So remember:

> **SECURITY GROUP**
> → RESOURCE FIREWALL
>
> **STATEFUL**
> → REMEMBERS
>
> **ALLOW ONLY**
> → NO DENY
>
> **REFERENCE SG**
> → TRUST THE TIER
>
> **NACL**
> → SUBNET + STATELESS + DENY

And the killer SAA question:

> **"Does the requirement involve stateful, resource-level control of allowed network traffic?"**
>
> YES
>
> → **Security Group**

---

## Related Notes

- [[VPC]]
- [[NACL]]
- [[Application Load Balancer]]
- [[RDS]]
- [[Systems Manager]]
- [[WAF]]
- [[20-SAA/15-Security/Network Firewall]]
- [[Shield]]