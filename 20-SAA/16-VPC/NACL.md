## What Problem Does It Solve?

[[NACL]] provides:

**Stateless network filtering at the subnet level**

It controls traffic entering and leaving:

**A subnet**

based on:

- Source IP
- Destination IP
- Port
- Protocol
- Allow rules
- Deny rules

Architecture:

Traffic  
↓  
Subnet Boundary  
↓  
NACL Rules  
↓  
ALLOW / DENY  
↓  
Resources

> [!tip] Memory Trick
> **NACL = Stateless Subnet Firewall**

---

## Core Concept

A Network ACL applies to:

**Subnets**

not directly to:

**Individual resources**

It is:

**Stateless**

and supports:

- Allow rules
- Deny rules

### Killer Exam Clue

> **Need an explicit deny rule for traffic entering or leaving a subnet**
>
> → **NACL**

---

# Subnet-Level Control

A NACL is associated with:

**One or more subnets**

Resources inside those subnets are subject to:

**The NACL rules**

### Memory Trick

**Security Group = Resource**

**NACL = Subnet**

---

# Stateless

NACLs are:

**Stateless**

This means:

If inbound traffic is allowed:

**Return traffic is NOT automatically allowed**

You must also permit the corresponding:

**Outbound traffic**

### Killer Exam Clue

> **Traffic enters successfully but return traffic is blocked**
>
> → Check the **NACL outbound rules**

### Memory Trick

**Stateless = Forgets the Connection**

---

# Inbound Rules

Inbound rules control:

**Traffic entering the subnet**

Example:

Allow:

TCP 443  
From:

`0.0.0.0/0`

---

# Outbound Rules

Outbound rules control:

**Traffic leaving the subnet**

For a stateless NACL:

You often need to explicitly allow:

**Return traffic**

### Exam Principle

> **Always think about both directions with NACLs**

---

# Allow and Deny Rules

Unlike Security Groups, NACLs support:

- ALLOW
- DENY

### Killer Exam Clue

> **Block one known malicious IP range at the subnet boundary**
>
> → **NACL Deny Rule**

---

# Rule Numbers

NACL rules have:

**Rule numbers**

Rules are evaluated:

**From the lowest number to the highest**

The first matching rule:

**Wins**

Example:

Rule 100  
→ DENY `203.0.113.0/24`

Rule 200  
→ ALLOW `0.0.0.0/0`

Traffic from:

`203.0.113.25`

matches:

**Rule 100 first**

and is:

**Denied**

### Memory Trick

**Lowest Number Wins**

---

# First Match Wins

NACLs do NOT combine rules together the same way Security Groups do.

Processing:

Rule 100  
↓  
Match?

YES  
→ Stop

NO  
↓  
Rule 200

### Killer Exam Trap

> **NACL rule order matters**

---

# Default NACL

Every VPC has a:

**Default NACL**

By default, it generally allows:

**Inbound and outbound traffic**

for associated subnets.

### Exam Principle

> **Default NACL is permissive**

---

# Custom NACL

A newly created:

**Custom NACL**

starts much more restrictive.

You must explicitly configure:

**Allow rules**

### Memory Trick

**Default NACL = Open**

**Custom NACL = Start Closed**

---

# Implicit Deny

At the end of a NACL rule list is an:

**Implicit deny**

If no rule matches:

**Traffic is denied**

### Killer Exam Concept

> **Traffic must match an allow rule before reaching the final deny**

---

# Security Group vs NACL

This comparison is critical.

## [[Security Groups]]

Think:

- Resource/ENI level
- Stateful
- Allow only
- No numbered priority
- Return traffic automatic

## NACL

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

# Comparison Table

| Feature | Security Group | NACL |
|---|---|---|
| Scope | Resource / ENI | Subnet |
| Stateful | ✅ | ❌ |
| Allow Rules | ✅ | ✅ |
| Deny Rules | ❌ | ✅ |
| Rule Order | No | ✅ |
| Return Traffic | Automatic | Explicit |
| Association | Resource | Subnet |

---

# Ephemeral Ports

One of the most important NACL concepts is:

**Ephemeral ports**

Clients use temporary high-numbered ports for:

**Return traffic**

Example:

Client  
↓  
Server:443

Server responds to:

Client Ephemeral Port

Because NACLs are stateless:

You may need outbound rules allowing:

**The relevant ephemeral port range**

### Killer Exam Clue

> **HTTPS request reaches server but response never returns**
>
> → Check NACL ephemeral-port rules.

---

# Why Ephemeral Ports Matter

Suppose a client connects to:

Server port:

**443**

The client itself may use:

**A temporary source port**

such as:

`49152`

Return traffic goes:

Server:443  
↓  
Client:49152

The NACL must allow:

**That return path**

---

# Ephemeral Port Ranges

Exact ephemeral-port ranges can vary by:

**Operating system/client**

For SAA, the important concept is:

> **Stateless NACLs may need broad ephemeral-port ranges for return traffic**

Do not over-focus on memorizing one universal range.

---

# Example — Public Web Subnet

Inbound NACL:

Allow:

TCP 443  
From Internet

Outbound NACL:

Allow:

Ephemeral return ports  
To Internet

Because the NACL is:

**Stateless**

---

# Example — Block Malicious IP

Requirement:

Block:

`198.51.100.0/24`

but allow other HTTPS traffic.

Rules:

100  
→ DENY `198.51.100.0/24`

200  
→ ALLOW TCP 443 from `0.0.0.0/0`

### Killer Exam Pattern

> **Specific deny before broad allow**

---

# NACL and Multiple Subnets

A NACL can be associated with:

**Multiple subnets**

But each subnet can be associated with:

**Only one NACL at a time**

### Memory Trick

**One Subnet → One NACL**

---

# Replacing NACL Association

If you associate a subnet with a:

**Different NACL**

the previous association is:

**Replaced**

---

# NACL + Public Subnet

A public subnet can use a NACL to control:

- Inbound Internet traffic
- Outbound Internet traffic

But the subnet also still needs:

- Route table
- Internet Gateway
- Resource Security Groups

### Exam Principle

> **NACL is only one layer of VPC security**

---

# Layered Security

A common architecture:

Internet  
↓  
NACL  
↓  
Security Group  
↓  
EC2

Both controls must allow:

**The required traffic**

### Memory Trick

**NACL = Subnet Gate**

**Security Group = Resource Guard**

---

# NACL vs WAF

## [[WAF]]

Think:

**HTTP application-layer inspection**

## NACL

Think:

**IP/port/protocol subnet filtering**

### Killer Shortcut

SQL injection  
→ WAF

Block IP CIDR at subnet boundary  
→ NACL

---

# NACL vs Network Firewall

## [[20-SAA/15-Security/Network Firewall]]

Think:

**Advanced stateful network inspection**

## NACL

Think:

**Basic stateless subnet filter**

### Killer Shortcut

Simple CIDR deny  
→ NACL

Intrusion prevention / Suricata  
→ Network Firewall

---

# NACL vs Route Table

## Route Table

Determines:

**Where traffic goes**

## NACL

Determines:

**Whether traffic is allowed**

### Memory Trick

**Route Table = Direction**

**NACL = Permission**

---

# NACL vs Security Group Reference

NACL rules use:

**IP-based criteria**

They do NOT support:

**Security Group references**

### Exam Trap

Need:

**Allow app tier based on another Security Group**

→ Use Security Group

not NACL.

---

# Architecture Thinking

## Scenario 1 — Explicit Deny

Need to block:

**One malicious external CIDR**

for an entire subnet.

Choose:

**NACL**

---

## Scenario 2 — App Tier Access

Need application EC2 instances to accept traffic only from:

**ALB Security Group**

Choose:

**Security Group**

not NACL.

---

## Scenario 3 — Return Traffic Failure

Inbound request works.

Response does not.

Security Group looks correct.

Check:

**NACL outbound ephemeral ports**

---

## Scenario 4 — Subnet-Level Policy

Need one control that applies to:

**Every resource in the subnet**

Choose:

**NACL**

---

## Scenario 5 — SQL Injection

Need to block malicious SQL payloads.

Choose:

**WAF**

not NACL.

---

## Scenario 6 — Intrusion Prevention

Need:

**Stateful traffic inspection and attack signatures**

Choose:

**Network Firewall**

---

# Scenario Recognition

Immediately think:

**NACL**

when you see:

- Subnet firewall
- Stateless
- Explicit deny
- Rule numbers
- First match
- Ephemeral ports
- Allow + deny
- Subnet boundary filtering

---

## Think Security Group When You See

- Resource-level
- Stateful
- Allow only
- Security Group reference
- ALB to EC2
- App to DB

---

## Think Network Firewall When You See

- Advanced inspection
- Stateful network firewall
- Suricata
- Intrusion prevention

---

# Exam Traps

## Trap 1 — NACL Is Stateful

❌

It is:

**Stateless**

---

## Trap 2 — NACL Supports Security Group References

❌

It uses:

**IP / protocol / port-based rules**

---

## Trap 3 — Highest Rule Number Wins

❌

The:

**Lowest matching rule number**

wins.

---

## Trap 4 — Return Traffic Is Automatically Allowed

❌

That is true for:

**Security Groups**

not NACLs.

---

## Trap 5 — NACL Cannot Deny Traffic

❌

NACL supports:

**Explicit deny**

---

## Trap 6 — Custom NACL Allows Everything by Default

❌

Custom NACL starts:

**Restrictive**

---

## Trap 7 — NACL Alone Determines Internet Connectivity

❌

You also need:

- Routing
- IGW/NAT as applicable
- Security Groups
- IP addressing

---

# Quick Cheat Sheet

| Exam Clue | Answer |
|---|---|
| Subnet Firewall | NACL |
| Stateless | NACL |
| Explicit Deny | NACL |
| Allow + Deny | NACL |
| Rule Priority | Lowest Number First |
| First Match Wins | NACL |
| Return Traffic | Explicitly Allow |
| Ephemeral Ports | Important for NACL |
| Resource Firewall | Security Group |
| Advanced VPC Inspection | Network Firewall |
| Web Attack Filtering | WAF |

---

# NACL Decision Map

Need:

**Explicit deny**

→ NACL

Need:

**Subnet-wide rule**

→ NACL

Need:

**Stateful resource firewall**

→ Security Group

Need:

**Security Group reference**

→ Security Group

Need:

**Advanced intrusion prevention**

→ Network Firewall

Need:

**HTTP attack filtering**

→ WAF

---

# Final Exam Rapid-Fire

> **SUBNET FIREWALL**
> → NACL
>
> **STATELESS**
> → NACL
>
> **ALLOW + DENY**
> → NACL
>
> **EXPLICIT DENY**
> → NACL
>
> **LOWEST RULE NUMBER**
> → FIRST EVALUATED
>
> **FIRST MATCH**
> → WINS
>
> **RETURN TRAFFIC**
> → MUST BE ALLOWED
>
> **EPHEMERAL PORTS**
> → THINK NACL
>
> **RESOURCE FIREWALL**
> → SECURITY GROUP
>
> **ADVANCED INSPECTION**
> → NETWORK FIREWALL
>
> **SQL INJECTION**
> → WAF

---

## Master Memory Trick

> [!tip] NACL Master Memory Trick
> Imagine a subnet is:
>
> **A gated neighborhood**
>
> The NACL is:
>
> **THE CHECKPOINT AT THE ENTRANCE**
>
> The guard reads rules:
>
> **FROM THE LOWEST NUMBER UP**
>
> The first matching rule says:
>
> **ALLOW**
>
> or:
>
> **DENY**
>
> Then the guard immediately stops reading.
>
> But the guard has:
>
> **NO MEMORY**
>
> If someone enters:
>
> they must still pass the rules again when:
>
> **Traffic leaves**
>
> That's why NACL is:
>
> **STATELESS**

So remember:

> **NACL**
> → SUBNET
>
> **STATELESS**
> → NO MEMORY
>
> **ALLOW + DENY**
> → BOTH
>
> **LOWEST NUMBER**
> → FIRST
>
> **FIRST MATCH**
> → WINS
>
> **EPHEMERAL PORTS**
> → RETURN TRAFFIC
>
> **SECURITY GROUP**
> → RESOURCE + STATEFUL

And the killer SAA question:

> **"Does the requirement involve subnet-level stateless filtering, explicit deny rules, or numbered rule evaluation?"**
>
> YES
>
> → **NACL**

---

## Related Notes

- [[VPC]]
- [[Security Groups]]
- [[20-SAA/15-Security/Network Firewall]]
- [[WAF]]
- [[05-Networking/VPC Flow Logs]]