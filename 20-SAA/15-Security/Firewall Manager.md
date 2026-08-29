## What Problem Does It Solve?

[[Firewall Manager]] provides:

**Centralized security policy management across multiple AWS accounts and resources**

It helps organizations consistently manage protections such as:

- WAF policies
- Shield Advanced protections
- Security group policies
- Network Firewall policies
- DNS Firewall policies

Architecture:

AWS Organizations  
↓  
Firewall Manager  
↓  
Central Security Policies  
↓  
Multiple Accounts / Resources

> [!tip] Memory Trick
> **Firewall Manager = Manage Security Rules Everywhere**

---

## Core Concept

Firewall Manager is especially useful when an organization has:

**Many AWS accounts**

and wants to enforce:

**Consistent network and application security policies**

from one place.

### Killer Exam Clue

> **Need centralized firewall/security policy enforcement across an AWS Organization**
>
> → **Firewall Manager**

---

# AWS Organizations Integration

Firewall Manager is designed to work with:

**AWS Organizations**

Architecture:

AWS Organization  
↓  
Security Administrator Account  
↓  
Firewall Manager  
↓  
Member Accounts

This allows a central security team to manage policies across:

**Many accounts**

### Memory Trick

**Organizations = Accounts**

**Firewall Manager = Security Policy Across Accounts**

---

# Delegated Administrator

A dedicated security account can be configured as:

**Firewall Manager administrator**

This lets the security team centrally manage:

**Firewall policies**

without doing everything from the:

**Management account**

### Killer Exam Clue

> **Need a dedicated security account to centrally enforce firewall policies**
>
> → **Firewall Manager administrator**

---

# Policy-Based Management

Firewall Manager uses:

**Security policies**

to define:

**What protections should be applied**

and:

**Where they should apply**

Example:

Security Policy  
↓  
Apply WAF Rules  
↓  
All Internet-Facing ALBs  
↓  
Across All Member Accounts

### Memory Trick

**Policy = Security Rule Blueprint**

---

# Scope

Policies can target resources based on factors such as:

- AWS account
- Resource type
- Tags
- Organizational units
- Inclusion/exclusion rules

This allows centralized security without applying every policy to:

**Every single resource**

---

# Firewall Manager + WAF

One of the most important integrations:

[[WAF]]  
↓  
Firewall Manager  
↓  
Centralized Web ACL Policies

Use when you need to apply:

**Consistent WAF protections**

across many:

- ALBs
- CloudFront distributions
- API endpoints

### Killer Exam Clue

> **Apply the same WAF rules to web applications across multiple AWS accounts**
>
> → **Firewall Manager**

---

# Example — Central WAF Policy

Security team creates:

**Corporate WAF Policy**

Rules include:

- Block SQL injection
- Block XSS
- Block malicious IPs

Firewall Manager applies the policy to:

**All qualifying web resources**

across:

**Member accounts**

### Memory Trick

**WAF Protects One Web Resource**

**Firewall Manager Scales the Policy**

---

# Firewall Manager + Shield Advanced

Firewall Manager can centrally manage:

[[Shield]]

Advanced protections across:

**Multiple accounts**

### Killer Exam Clue

> **Centrally apply Shield Advanced protection to resources across an AWS Organization**
>
> → **Firewall Manager**

---

# Firewall Manager + Security Groups

Firewall Manager can help enforce:

**Security group policies**

Examples:

- Require approved security groups
- Audit security group usage
- Detect overly permissive rules
- Standardize security group controls

### Killer Exam Clue

> **Centrally enforce security group standards across many accounts**
>
> → **Firewall Manager**

---

# Common Security Group Policies

Firewall Manager can help with policies that:

- Audit security groups
- Enforce required groups
- Remove unwanted rules where supported
- Standardize controls

### Memory Trick

**Security Group Policy = Keep Network Access Consistent**

---

# Firewall Manager + Network Firewall

Firewall Manager can centrally deploy and manage:

[[20-SAA/15-Security/Network Firewall]]

policies across:

**Multiple VPCs and accounts**

Architecture:

Firewall Manager  
↓  
Network Firewall Policy  
↓  
Multiple VPCs  
↓  
Centralized Inspection

### Killer Exam Clue

> **Deploy consistent Network Firewall policies across many VPCs**
>
> → **Firewall Manager**

---

# Firewall Manager + DNS Firewall

Firewall Manager can centrally manage supported:

**Route 53 Resolver DNS Firewall**

policies.

Use when you need to control:

**DNS query filtering**

across:

**Multiple VPCs/accounts**

### Killer Exam Clue

> **Apply centralized DNS filtering rules across an organization**
>
> → **Firewall Manager**

---

# Firewall Manager vs WAF

This distinction is critical.

## [[WAF]]

Actually:

**Inspects and filters HTTP(S) requests**

## Firewall Manager

Centrally:

**Deploys and manages WAF policies**

### Memory Trick

**WAF = Protection**

**Firewall Manager = Management**

---

# Firewall Manager vs Network Firewall

## [[20-SAA/15-Security/Network Firewall]]

Actually:

**Inspects VPC network traffic**

## Firewall Manager

Centrally:

**Manages Network Firewall policies**

### Killer Shortcut

**Need packet/session inspection**
→ Network Firewall

**Need centralized policy deployment across accounts**
→ Firewall Manager

---

# Firewall Manager vs Shield

## [[Shield]]

Provides:

**DDoS protection**

## Firewall Manager

Helps centrally manage:

**Shield Advanced protections**

### Memory Trick

**Shield = Defend**

**Firewall Manager = Coordinate**

---

# Firewall Manager vs Security Hub

These are easy to confuse.

## [[Security Hub]]

Think:

**Centralized security findings and posture**

## Firewall Manager

Think:

**Centralized security policy enforcement**

### Killer Shortcut

**See findings**
→ Security Hub

**Push firewall policies**
→ Firewall Manager

---

# Firewall Manager vs Config

## [[Config]]

Think:

**Detect configuration compliance**

## Firewall Manager

Think:

**Enforce centralized firewall/security policies**

Example:

Need to detect that SG allows `0.0.0.0/0`

→ Config

Need centralized organization-wide SG policy

→ Firewall Manager

---

# Firewall Manager vs Organizations SCPs

## SCP

Controls:

**What API actions accounts can perform**

## Firewall Manager

Controls:

**Firewall/security policy deployment**

### Memory Trick

**SCP = Permission Boundary**

**Firewall Manager = Network/Web Security Policy**

---

# Automatic Policy Application

One of Firewall Manager's strengths is:

**Automatically applying policies to new qualifying resources**

Example:

Developer creates:

New Internet-Facing ALB  
↓  
Firewall Manager detects resource  
↓  
Corporate WAF policy applies

### Killer Exam Clue

> **New resources must automatically receive the organization's standard firewall protections**
>
> → **Firewall Manager**

---

# Policy Compliance

Firewall Manager can identify resources that are:

**Noncompliant with centralized policies**

This helps security teams:

- Detect gaps
- Correct drift
- Enforce consistency

### Memory Trick

**Policy Exists → Resource Must Match**

---

# Remediation

Depending on the policy type, Firewall Manager can support:

**Automatic remediation**

to bring noncompliant resources back into:

**Policy compliance**

### Killer Exam Clue

> **Automatically remediate resources that drift from centralized firewall policy**
>
> → **Firewall Manager**

---

# Resource Tags

Firewall Manager policies can often use:

**Tags**

to determine:

**Which resources should receive protection**

Example:

`Environment = Production`

→ Apply stricter WAF policy

### Exam Principle

> **Tags can help scope centralized security enforcement**

---

# Organizational Units

Policies can be scoped to:

**Organizational Units — OUs**

Example:

Production OU  
→ Strict Network Firewall policy

Development OU  
→ Less restrictive policy

### Killer Exam Clue

> **Apply different firewall policies to different groups of AWS accounts**
>
> → **Firewall Manager + OUs**

---

# Architecture Thinking

## Scenario 1 — Same WAF Rules Everywhere

Company has:

50 AWS accounts.

Every public ALB must use:

**The same WAF rule set**

Choose:

**Firewall Manager**

---

## Scenario 2 — Single Web Application

One ALB needs:

**SQL injection protection**

Choose:

**WAF**

Firewall Manager is unnecessary if there is no:

**Central multi-account policy requirement**

---

## Scenario 3 — Multiple VPC Firewalls

Enterprise wants:

**Consistent Network Firewall policies**

across:

100 VPCs.

Choose:

**Firewall Manager + Network Firewall**

---

## Scenario 4 — DDoS Across Organization

Company subscribes to:

**Shield Advanced**

and needs centralized protection management.

Choose:

**Firewall Manager**

---

## Scenario 5 — Central Security Findings

Security team wants one dashboard containing:

- GuardDuty
- Inspector
- Macie findings

Choose:

**Security Hub**

not Firewall Manager.

---

## Scenario 6 — Security Group Standardization

All production accounts must enforce:

**Approved security group rules**

Choose:

**Firewall Manager security group policies**

---

## Scenario 7 — New Resources

Developers continually create:

**New CloudFront distributions**

They should automatically receive:

**Corporate WAF protections**

Choose:

**Firewall Manager**

---

# Scenario Recognition

Immediately think:

**Firewall Manager**

when you see:

- Centralized firewall policies
- AWS Organizations
- Multi-account WAF
- Multi-account Shield Advanced
- Security group policy enforcement
- Central Network Firewall deployment
- Organization-wide security policies

---

## Think WAF When You See

- SQL injection
- XSS
- HTTP request filtering

---

## Think Network Firewall When You See

- VPC traffic inspection
- Stateful firewall
- Suricata

---

## Think Shield When You See

- DDoS protection

---

## Think Security Hub When You See

- Central security findings
- Security posture
- Findings aggregation

---

# Exam Traps

## Trap 1 — Firewall Manager Inspects Packets Itself

❌

Services such as:

- WAF
- Network Firewall

perform the actual inspection.

Firewall Manager:

**Centralizes policy management**

---

## Trap 2 — Firewall Manager Is the Same as Security Hub

❌

Firewall Manager:

**Policy enforcement**

Security Hub:

**Finding aggregation**

---

## Trap 3 — Firewall Manager Is Only for WAF

❌

It can centrally manage multiple supported security policy types.

---

## Trap 4 — Firewall Manager Is Mainly a DDoS Protection Service

❌

Think:

**Shield**

Firewall Manager can centrally manage:

**Shield Advanced**

---

## Trap 5 — Firewall Manager Is Useful Only for One Resource

❌

Its strongest use case is:

**Centralized security across many resources/accounts**

---

## Trap 6 — SCP and Firewall Manager Are the Same

❌

SCP:

**API permission guardrail**

Firewall Manager:

**Firewall/security policy management**

---

# Quick Cheat Sheet

| Exam Clue | Answer |
|---|---|
| Central Firewall Policies | Firewall Manager |
| Multi-Account WAF | Firewall Manager |
| Multi-Account Shield Advanced | Firewall Manager |
| Security Group Policy | Firewall Manager |
| Multi-VPC Network Firewall Policy | Firewall Manager |
| Central DNS Firewall Policy | Firewall Manager |
| Automatically Protect New Resources | Firewall Manager |
| HTTP Attack Filtering | WAF |
| VPC Traffic Inspection | Network Firewall |
| DDoS Protection | Shield |
| Central Security Findings | Security Hub |

---

# Security Management Decision Map

Need:

**Filter malicious HTTP requests**

→ WAF

Need:

**Inspect VPC traffic**

→ Network Firewall

Need:

**DDoS protection**

→ Shield

Need:

**Manage these protections across many accounts**

→ Firewall Manager

Need:

**Aggregate findings**

→ Security Hub

---

# Firewall Manager vs Security Hub

| Requirement | Firewall Manager | Security Hub |
|---|---:|---:|
| Central Policy Enforcement | ✅ | ❌ |
| Aggregate Findings | ❌ Primary | ✅ |
| Multi-Account WAF Management | ✅ | ❌ |
| Multi-Account Network Firewall | ✅ | ❌ |
| Security Posture Dashboard | Limited Different Role | ✅ |
| Automatic Policy Application | ✅ | ❌ Primary |

---

# Final Exam Rapid-Fire

> **CENTRAL FIREWALL MANAGEMENT**
> → FIREWALL MANAGER
>
> **MULTI-ACCOUNT WAF**
> → FIREWALL MANAGER
>
> **MULTI-ACCOUNT SHIELD ADVANCED**
> → FIREWALL MANAGER
>
> **SECURITY GROUP POLICY**
> → FIREWALL MANAGER
>
> **MULTI-VPC NETWORK FIREWALL**
> → FIREWALL MANAGER
>
> **AUTO-PROTECT NEW RESOURCES**
> → FIREWALL MANAGER
>
> **WEB FILTERING**
> → WAF
>
> **VPC INSPECTION**
> → NETWORK FIREWALL
>
> **DDoS**
> → SHIELD
>
> **CENTRAL FINDINGS**
> → SECURITY HUB

---

## Master Memory Trick

> [!tip] Firewall Manager Master Memory Trick
> Imagine a company has:
>
> **100 AWS ACCOUNTS**
>
> Each account has:
>
> - WAF rules
> - Security groups
> - Firewalls
> - DDoS protections
>
> Managing each one individually would be:
>
> **A nightmare**
>
> So the security team creates:
>
> **ONE CENTRAL RULEBOOK**
>
> and tells every account:
>
> **"FOLLOW THESE SECURITY POLICIES."**
>
> That's:
>
> **FIREWALL MANAGER**
>
> WAF still filters:
>
> **WEB TRAFFIC**
>
> Network Firewall still inspects:
>
> **VPC TRAFFIC**
>
> Shield still protects from:
>
> **DDoS**
>
> Firewall Manager simply makes sure:
>
> **EVERYONE USES THE RIGHT POLICIES**

So remember:

> **WAF**
> → WEB PROTECTION
>
> **NETWORK FIREWALL**
> → NETWORK INSPECTION
>
> **SHIELD**
> → DDoS
>
> **FIREWALL MANAGER**
> → MANAGE THEM AT SCALE
>
> **SECURITY HUB**
> → CENTRALIZE FINDINGS

And the killer SAA question:

> **"Does the company need to centrally enforce firewall or security policies across multiple AWS accounts and resources?"**
>
> YES
>
> → **Firewall Manager**

---

## Related Notes

- [[WAF]]
- [[Shield]]
- [[20-SAA/15-Security/Network Firewall]]
- [[Security Hub]]
- [[Config]]
- [[AWS Organizations]]
- [[CloudFront]]
- [[Application Load Balancer]]
- [[05-Networking/Transit Gateway]]