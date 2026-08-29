## What Problem Does It Solve?

[[Shield]] protects AWS applications against:

**Distributed Denial of Service — DDoS attacks**

It helps defend applications from attacks designed to:

**Overwhelm network or application resources with massive traffic**

Architecture:

Attack Traffic  
↓  
Shield  
↓  
Protected AWS Resource  
↓  
Application

> [!tip] Memory Trick
> **Shield = DDoS Protection**

---

## Core Concept

A DDoS attack attempts to make an application:

**Unavailable**

by overwhelming it with:

- Network traffic
- Protocol traffic
- Request floods

Shield provides:

**Managed DDoS protection**

### Killer Exam Clue

> **Protect AWS workloads against DDoS attacks**
>
> → **Shield**

---

# Shield Standard

**Shield Standard**

provides:

**Automatic baseline DDoS protection**

for AWS customers.

It helps protect against common:

- Network-layer attacks
- Transport-layer attacks

### Important Exam Fact

Shield Standard is:

**Automatically included**

for AWS customers.

### Memory Trick

**Standard = Automatic Basic DDoS Protection**

---

# Shield Advanced

**Shield Advanced**

provides:

**Enhanced DDoS protection**

for applications with:

- Higher security requirements
- Mission-critical workloads
- Greater attack risk

It adds capabilities beyond:

**Shield Standard**

### Killer Exam Clue

> **Mission-critical application needs advanced DDoS protection and specialized support**
>
> → **Shield Advanced**

---

# Standard vs Advanced

| Requirement | Shield Standard | Shield Advanced |
|---|---:|---:|
| Basic DDoS Protection | ✅ | ✅ |
| Automatically Included | ✅ | ❌ Paid |
| Advanced DDoS Detection | Limited | ✅ |
| Specialized DDoS Support | ❌ | ✅ |
| DDoS Cost Protection | ❌ | ✅ Supported Cases |
| Advanced Visibility | Limited | ✅ |

### Memory Trick

**Standard = Baseline**

**Advanced = Mission-Critical**

---

# Protected Resources

Shield protection commonly applies to supported resources such as:

- [[CloudFront]]
- Route 53
- [[Application Load Balancer]]
- Network Load Balancer
- Elastic IP addresses
- Other supported AWS edge/network resources

### Exam Principle

> **Shield works especially well with AWS edge and load-balancing services**

---

# Shield + CloudFront

A very common architecture:

Internet  
↓  
Shield  
↓  
[[CloudFront]]  
↓  
Origin

CloudFront provides:

- Global edge distribution
- Traffic absorption
- Origin protection

Shield provides:

**DDoS defense**

### Killer Exam Clue

> **Protect a globally distributed web application from DDoS attacks**
>
> → **CloudFront + Shield**

---

# Shield + Route 53

Route 53 is designed for:

**Highly available DNS**

and receives:

**Shield Standard protection**

This helps protect:

**DNS availability**

during attacks.

### Memory Trick

**Route 53 + Shield = Protect DNS Availability**

---

# Shield + Load Balancers

Shield can help protect:

- Application Load Balancers
- Network Load Balancers

from:

**DDoS-related traffic**

This provides protection before traffic reaches:

**Backend targets**

---

# DDoS Layers

DDoS attacks can target different layers.

## Layer 3

Think:

**Network**

Examples:

- Large traffic floods

## Layer 4

Think:

**Transport**

Examples:

- TCP/UDP attacks

## Layer 7

Think:

**Application / HTTP**

Examples:

- HTTP request floods

### SAA Principle

> **Shield focuses on DDoS protection**
>
> **WAF adds application-layer request filtering**

---

# Shield vs WAF

This comparison is extremely important.

## [[WAF]]

Think:

**Malicious HTTP requests**

Examples:

- SQL injection
- XSS
- Bad IPs
- Suspicious paths
- Bots

## Shield

Think:

**DDoS**

Examples:

- Volumetric attacks
- Protocol attacks
- Large-scale request floods

### Memory Trick

**WAF = BAD REQUEST**

**SHIELD = TOO MUCH TRAFFIC**

---

# Shield + WAF

These services are commonly used:

**Together**

Architecture:

Internet  
↓  
Shield  
↓  
WAF  
↓  
CloudFront / ALB  
↓  
Application

Shield:

**Absorbs DDoS attacks**

WAF:

**Filters malicious web requests**

### Killer Exam Clue

> **Need both DDoS protection and SQL injection protection**
>
> → **Shield + WAF**

---

# Shield Advanced DDoS Response Team

Shield Advanced customers can receive access to specialized AWS support for:

**DDoS events**

commonly associated with the:

**AWS Shield Response Team**

This can help during:

**Serious attacks**

### Killer Exam Clue

> **Need AWS specialists to help respond to DDoS attacks**
>
> → **Shield Advanced**

---

# DDoS Cost Protection

Large DDoS attacks can cause protected resources to:

**Scale significantly**

which may increase:

**AWS charges**

Shield Advanced provides:

**DDoS cost protection**

for eligible scaling charges associated with:

**Validated DDoS attacks**

### Killer Exam Clue

> **Need financial protection from scaling charges caused by DDoS attacks**
>
> → **Shield Advanced**

---

# Attack Visibility

Shield Advanced provides:

**Greater visibility**

into DDoS activity.

This helps security teams understand:

- Attack patterns
- Attack duration
- Protected resources
- Mitigation activity

---

# CloudWatch Integration

Shield metrics and events can integrate with:

[[CloudWatch]]

for:

- Monitoring
- Alarms
- Attack visibility

### Memory Trick

**Shield Protects**

**CloudWatch Monitors**

---

# Shield Advanced + WAF

Shield Advanced works closely with:

[[WAF]]

for:

**Application-layer DDoS mitigation**

This combination provides:

- DDoS defense
- HTTP filtering
- Rate-based rules
- Custom web controls

---

# Rate-Based WAF Rules

If a DDoS-like attack occurs specifically at:

**HTTP request level**

a WAF:

**Rate-Based Rule**

can help restrict:

**Abusive request sources**

### Killer Distinction

Large volumetric DDoS  
→ Shield

Repeated HTTP requests from sources  
→ WAF Rate-Based Rule

---

# CloudFront as DDoS Defense Layer

CloudFront can absorb traffic at:

**AWS edge locations**

This prevents every request from reaching:

**The origin**

Architecture:

Attack  
↓  
AWS Edge  
↓  
CloudFront + Shield  
↓  
Origin

### SAA Principle

> **Use AWS edge infrastructure to absorb attacks before they reach your application**

---

# Route 53 Resilience

Route 53 is built as a:

**Globally distributed DNS service**

This makes it an important component of:

**DDoS-resilient architectures**

---

# Auto Scaling and DDoS

Auto Scaling can help applications:

**Handle legitimate traffic spikes**

but it is NOT itself:

**A DDoS protection service**

### Exam Trap

> Do not choose Auto Scaling alone when the requirement says:
>
> **DDoS protection**

Think:

**Shield**

---

# Shield vs Auto Scaling

## Auto Scaling

Think:

**Add capacity**

## Shield

Think:

**Mitigate malicious traffic**

### Memory Trick

**Auto Scaling = Handle Demand**

**Shield = Handle Attack**

---

# Shield vs Network Firewall

## Shield

Think:

**DDoS protection**

## Network Firewall

Think:

**VPC network traffic inspection**

They solve:

**Different security problems**

---

# Shield vs Security Groups

## Security Groups

Think:

- Ports
- Protocols
- Source/destination access

## Shield

Think:

**DDoS mitigation**

### Killer Shortcut

**Block port 22**
→ Security Group

**Stop volumetric attack**
→ Shield

---

# Shield vs NACL

NACLs can block:

**Specific network traffic**

at the subnet level.

But they are not designed as:

**Managed DDoS mitigation platforms**

### Memory Trick

**NACL = Network Rule**

**Shield = DDoS Defense**

---

# Shield vs GuardDuty

## Shield

Protects against:

**DDoS**

## GuardDuty

Detects:

**Suspicious or malicious account/workload activity**

### Killer Shortcut

DDoS  
→ Shield

Suspicious AWS activity  
→ GuardDuty

---

# Architecture Thinking

## Scenario 1 — Public Website DDoS

Company operates:

A public e-commerce website.

Need basic DDoS protection.

Choose:

**Shield Standard**

---

## Scenario 2 — Mission-Critical Bank

Financial application requires:

- Advanced DDoS protection
- AWS expert response
- Financial protection from DDoS scaling charges

Choose:

**Shield Advanced**

---

## Scenario 3 — SQL Injection

Application receives:

**Malicious SQL payloads**

Do NOT choose Shield as the main answer.

Choose:

**WAF**

---

## Scenario 4 — DDoS + SQL Injection

Need:

- DDoS protection
- SQL injection protection

Choose:

Shield  
+  
WAF

---

## Scenario 5 — Global Web Application

Need strong DDoS resilience.

Architecture:

Route 53  
↓  
CloudFront  
↓  
Shield  
↓  
WAF  
↓  
ALB

---

## Scenario 6 — SSH Restriction

Need to prevent:

**Internet access to port 22**

Do NOT choose Shield.

Choose:

**Security Group**

---

## Scenario 7 — Sudden Legitimate Traffic

Marketing campaign causes:

**Huge legitimate traffic spike**

Need capacity.

Think:

**Auto Scaling**

not Shield.

---

## Scenario 8 — DDoS Scaling Charges

Massive attack caused:

**Protected resources to scale**

Need financial protection.

Choose:

**Shield Advanced**

---

# Scenario Recognition

Immediately think:

**Shield**

when you see:

- DDoS
- Distributed denial of service
- Volumetric attack
- Protocol attack
- AWS edge protection
- Shield Advanced
- DDoS Response Team
- DDoS cost protection

---

## Think Shield Standard When You See

- Basic DDoS protection
- Automatic protection
- No specialized support requirement

---

## Think Shield Advanced When You See

- Mission-critical workload
- Advanced DDoS protection
- DDoS response assistance
- DDoS cost protection
- Enhanced visibility

---

## Think WAF When You See

- SQL injection
- XSS
- Bad HTTP request
- Bot filtering
- URL/header inspection

---

# Exam Traps

## Trap 1 — WAF and Shield Are the Same Service

❌

WAF:

**Web request filtering**

Shield:

**DDoS protection**

---

## Trap 2 — Shield Standard Requires a Paid Subscription

❌

Shield Standard is:

**Automatically included**

---

## Trap 3 — Shield Advanced Is Required for Every AWS Application

❌

Use it when:

**Advanced DDoS protection requirements justify it**

---

## Trap 4 — Shield Prevents SQL Injection

❌

Think:

**WAF**

---

## Trap 5 — Auto Scaling Is a DDoS Protection Service

❌

It handles:

**Capacity**

Shield handles:

**DDoS attacks**

---

## Trap 6 — Security Groups Replace Shield

❌

Security Groups:

**Network access rules**

Shield:

**DDoS mitigation**

---

## Trap 7 — WAF Rate Limiting and Shield Solve Exactly the Same Problem

❌

WAF rate rules:

**Application-level abusive traffic**

Shield:

**Broader DDoS protection**

---

# Quick Cheat Sheet

| Exam Clue | Answer |
|---|---|
| DDoS Protection | Shield |
| Basic DDoS Protection | Shield Standard |
| Advanced DDoS Protection | Shield Advanced |
| Automatically Included | Shield Standard |
| Specialized DDoS Support | Shield Advanced |
| DDoS Cost Protection | Shield Advanced |
| SQL Injection | WAF |
| XSS | WAF |
| HTTP Rate Filtering | WAF |
| Global Edge Protection | CloudFront + Shield |
| Port Filtering | Security Group |
| Legitimate Traffic Scaling | Auto Scaling |

---

# Security Decision Map

Need:

**DDoS protection**

→ Shield

Need:

**Advanced DDoS support**

→ Shield Advanced

Need:

**SQL injection / XSS**

→ WAF

Need:

**Bot/rate-based HTTP filtering**

→ WAF

Need:

**Port filtering**

→ Security Group / NACL

Need:

**Application scaling**

→ Auto Scaling

---

# Shield vs WAF

| Requirement | Shield | WAF |
|---|---:|---:|
| DDoS | ✅ | Limited Supporting Role |
| Volumetric Attack | ✅ | ❌ Primary |
| SQL Injection | ❌ | ✅ |
| XSS | ❌ | ✅ |
| HTTP Request Inspection | ❌ Primary | ✅ |
| Rate-Based HTTP Rules | ❌ | ✅ |
| DDoS Specialist Support | Advanced | ❌ |

---

# Final Exam Rapid-Fire

> **DDoS**
> → SHIELD
>
> **BASIC DDoS**
> → SHIELD STANDARD
>
> **ADVANCED DDoS**
> → SHIELD ADVANCED
>
> **AUTOMATIC DDoS PROTECTION**
> → SHIELD STANDARD
>
> **AWS DDoS EXPERT HELP**
> → SHIELD ADVANCED
>
> **DDoS COST PROTECTION**
> → SHIELD ADVANCED
>
> **SQL INJECTION**
> → WAF
>
> **XSS**
> → WAF
>
> **BAD HTTP REQUEST**
> → WAF
>
> **PORT ACCESS**
> → SECURITY GROUP
>
> **LEGITIMATE TRAFFIC SPIKE**
> → AUTO SCALING

---

## Master Memory Trick

> [!tip] Shield Master Memory Trick
> Imagine your application is:
>
> **A castle**
>
> [[WAF]] is the guard at the front gate inspecting:
>
> **Each visitor**
>
> Shield is:
>
> **THE GIANT WALL AROUND THE CASTLE**
>
> When a massive army tries to overwhelm:
>
> **THE ENTIRE CASTLE**
>
> Shield absorbs:
>
> **THE ATTACK**
>
> Basic wall?
>
> **SHIELD STANDARD**
>
> Giant reinforced wall with AWS security specialists standing by?
>
> **SHIELD ADVANCED**

So remember:

> **SHIELD**
> → DDoS
>
> **STANDARD**
> → BASIC + AUTOMATIC
>
> **ADVANCED**
> → MORE PROTECTION + SUPPORT
>
> **WAF**
> → MALICIOUS WEB REQUESTS
>
> **CLOUDFRONT**
> → EDGE ABSORPTION
>
> **AUTO SCALING**
> → LEGITIMATE CAPACITY

And the killer SAA question:

> **"Is the application being overwhelmed by a distributed denial-of-service attack?"**
>
> YES
>
> → **Shield**
>
> Need advanced support and cost protection?
>
> → **Shield Advanced**

---

## Related Notes

- [[WAF]]
- [[CloudFront]]
- [[Application Load Balancer]]
- [[Network Load Balancer]]
- [[Route 53]]
- [[CloudWatch]]
- [[06-Security/GuardDuty]]
- [[20-SAA/15-Security/Network Firewall]]