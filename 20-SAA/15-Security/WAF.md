## What Problem Does It Solve?

[[WAF]] protects web applications from:

**Common web exploits and unwanted HTTP(S) traffic**

It can inspect requests and allow or block traffic based on rules.

Common protections include:

- SQL injection
- Cross-site scripting
- Malicious IP addresses
- Suspicious request patterns
- Bot traffic
- Excessive request rates

Architecture:

Internet  
↓  
WAF  
↓  
Protected AWS Resource  
↓  
Application

> [!tip] Memory Trick
> **WAF = Web Request Filter**

---

## Core Concept

WAF operates at:

**Layer 7 — Application Layer**

It examines:

**HTTP and HTTPS requests**

and decides whether to:

- Allow
- Block
- Count
- Challenge/CAPTCHA where supported

### Killer Exam Clue

> **Need to protect a web application from SQL injection or XSS**
>
> → **WAF**

---

# Supported Resources

WAF can protect supported resources such as:

- [[CloudFront]]
- [[Application Load Balancer]]
- [[API Gateway]]
- Other supported AWS web endpoints

### Exam Shortcut

**Web request filtering**
→ WAF

---

# Web ACL

The main WAF resource is a:

**Web ACL — Web Access Control List**

A Web ACL contains:

**Rules**

that inspect incoming requests.

Architecture:

Request  
↓  
Web ACL  
↓  
Rules  
↓  
Allow / Block

### Memory Trick

**Web ACL = Rule Container**

---

# WAF Rules

Rules define:

**What traffic should match**

Examples:

- IP address
- Country
- Request path
- Header
- Query string
- Request body
- SQL injection pattern
- XSS pattern
- Request rate

---

# Rule Actions

A matching WAF rule can take actions such as:

- Allow
- Block
- Count

Additional supported actions can include:

- CAPTCHA
- Challenge

### Memory Trick

**Match Traffic → Take Action**

---

# Managed Rule Groups

WAF supports:

**Managed Rule Groups**

These provide prebuilt protections for:

- Common vulnerabilities
- Known attack patterns
- OWASP-style threats
- Malicious requests

### Killer Exam Clue

> **Need common web exploit protection without writing every rule manually**
>
> → **WAF Managed Rules**

---

# SQL Injection Protection

SQL injection attempts try to manipulate:

**Database queries**

through malicious input.

WAF can inspect request content for:

**SQL injection patterns**

### Killer Exam Clue

> **Protect public application from SQL injection**
>
> → **WAF**

---

# Cross-Site Scripting

Cross-site scripting:

**XSS**

attempts to inject malicious scripts into:

**Web content or requests**

WAF can detect:

**XSS patterns**

### Memory Trick

**SQLi + XSS = WAF**

---

# IP Set

An:

**IP Set**

contains IP addresses or CIDR ranges.

You can use it to:

- Allow trusted IPs
- Block malicious IPs
- Restrict access by source

### Killer Exam Clue

> **Block known malicious IP ranges**
>
> → **WAF IP Set**

---

# Geographic Match

WAF can filter traffic based on:

**Country of origin**

This can be useful when an application should:

- Block specific countries
- Allow traffic only from certain regions

### Killer Exam Clue

> **Block web requests originating from certain countries**
>
> → **WAF Geographic Match**

---

# Rate-Based Rules

A:

**Rate-Based Rule**

tracks request rates from sources such as:

**Client IP addresses**

and can take action when the request rate exceeds:

**A configured threshold**

### Killer Exam Clue

> **Block a client sending an excessive number of requests**
>
> → **WAF Rate-Based Rule**

### Memory Trick

**Too Many Requests From One Source = Rate-Based Rule**

---

# Rate-Based Rule vs API Gateway Throttling

## WAF Rate-Based Rule

Think:

**Security-oriented source filtering**

Useful for:

- Abusive clients
- Bots
- Request floods

## API Gateway Throttling

Think:

**API traffic management**

Useful for:

- Request-rate limits
- Protecting backend capacity
- Usage plans

### Killer Shortcut

**Malicious source**
→ WAF

**API capacity control**
→ API Gateway throttling

---

# WAF vs Shield

This is one of the most important security comparisons.

## WAF

Protects against:

**Layer 7 web attacks**

Examples:

- SQL injection
- XSS
- Malicious HTTP requests

## [[06-Security/Shield]]

Protects against:

**DDoS attacks**

### Memory Trick

**WAF = Web Exploits**

**Shield = DDoS**

---

# WAF + Shield

They are often used:

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

Think:

Shield  
→ Absorb DDoS

WAF  
→ Filter malicious web requests

---

# WAF + CloudFront

A common architecture:

Internet  
↓  
WAF  
↓  
[[CloudFront]]  
↓  
Origin

Benefits include:

- Block malicious traffic at the edge
- Reduce unwanted origin requests
- Protect global web applications

### Killer Exam Clue

> **Protect a globally distributed web application from malicious HTTP requests**
>
> → **CloudFront + WAF**

---

# WAF + ALB

Architecture:

Internet  
↓  
WAF  
↓  
[[Application Load Balancer]]  
↓  
EC2 / ECS

Use when:

**Application traffic reaches an ALB**

and needs:

**Layer 7 filtering**

---

# WAF + API Gateway

Architecture:

Internet  
↓  
WAF  
↓  
[[API Gateway]]  
↓  
Backend

Use when:

**Public APIs**

need protection against:

- SQL injection
- XSS
- Malicious IPs
- Abusive request patterns

---

# WAF vs Security Groups

## Security Groups

Operate mainly at:

**Network/transport level**

Think:

- IP
- Port
- Protocol

## WAF

Operates at:

**HTTP application layer**

Think:

- URL
- Header
- Body
- Query string
- Web attack signatures

### Killer Shortcut

**Port 443 allowed?**
→ Security Group

**SQL injection in request body?**
→ WAF

---

# WAF vs NACL

## NACL

Think:

**Subnet-level network filtering**

## WAF

Think:

**Application-layer HTTP filtering**

### Memory Trick

**NACL = Network**

**WAF = Web**

---

# WAF vs Network Firewall

AWS Network Firewall focuses on:

**Network traffic inspection and filtering**

WAF focuses on:

**HTTP(S) web requests**

### Killer Shortcut

**VPC network traffic**
→ Network Firewall

**Web request**
→ WAF

---

# Custom Rules

You can create:

**Custom WAF rules**

when managed rules do not fully match:

**Application-specific requirements**

Examples:

- Block `/admin` except trusted IPs
- Require specific header
- Block suspicious query patterns

---

# Rule Priority

Rules in a Web ACL have:

**Priority**

WAF evaluates rules according to:

**Their configured order**

### Exam Principle

> **Rule ordering matters when multiple rules could match the same request**

---

# Default Action

If no WAF rule matches:

The Web ACL uses its:

**Default Action**

Typically:

- Allow
- Block

### Memory Trick

**No Rule Match → Default Action**

---

# Count Mode

A rule can use:

**Count**

instead of immediately blocking traffic.

This is useful for:

- Testing
- Tuning
- Observing impact
- Avoiding accidental blocking

### Killer Exam Clue

> **Evaluate a new WAF rule before enforcing it**
>
> → **Count Mode**

---

# False Positives

Security rules can sometimes block:

**Legitimate traffic**

These are:

**False positives**

Using:

- Count mode
- Rule tuning
- Scope-down logic

can help reduce:

**Unwanted blocking**

---

# WAF Logging

WAF can send logs to supported destinations for:

- Security analysis
- Troubleshooting
- Rule tuning
- Incident investigation

### Exam Principle

> **Use WAF logging to understand why requests were allowed or blocked**

---

# CloudWatch Metrics

WAF publishes:

**CloudWatch metrics**

for:

- Allowed requests
- Blocked requests
- Rule matches

This helps monitor:

**Web security activity**

---

# WAF + CloudWatch

Architecture:

WAF  
↓  
CloudWatch Metrics  
↓  
Alarm / Dashboard

Use this to monitor:

- Attack patterns
- Blocked-request spikes
- Rule activity

---

# Bot Control

WAF supports capabilities designed to help identify and manage:

**Bot traffic**

This can help distinguish:

- Legitimate automation
- Scrapers
- Malicious bots
- Automated abuse

### Killer Exam Clue

> **Need advanced protection against unwanted bot traffic**
>
> → **WAF Bot Control**

---

# CAPTCHA / Challenge

Supported WAF configurations can require suspicious clients to:

**Complete a challenge**

instead of immediately:

**Blocking**

This can help reduce automated abuse while allowing:

**Legitimate human traffic**

---

# Scope-Down Statements

A rule can sometimes be narrowed so that it applies only to:

**A subset of requests**

Example:

Rate-limit only:

`/login`

instead of:

**The entire application**

### Exam Concept

> **Apply security controls selectively when only certain paths are sensitive**

---

# WAF vs Authentication

WAF does NOT determine:

**Who an application user is**

Authentication belongs to services such as:

- [[Cognito]]
- IAM
- Lambda Authorizer

### Exam Trap

> **WAF protects requests**
>
> It does not replace:
>
> **Authentication**

---

# WAF vs Encryption

WAF does NOT provide:

**TLS encryption**

For HTTPS certificates:

Think:

[[ACM]]

WAF inspects and filters:

**Web traffic**

---

# WAF vs Secrets Manager

WAF does not:

**Store credentials**

Think:

[[Secrets Manager]]

---

# Architecture Thinking

## Scenario 1 — SQL Injection

Public web application receives:

**SQL injection attacks**

Choose:

**WAF**

---

## Scenario 2 — XSS

Application receives malicious:

**JavaScript payloads**

Choose:

**WAF**

---

## Scenario 3 — Known Malicious IPs

Security team has a list of:

**Bad IP ranges**

Choose:

**WAF IP Set**

---

## Scenario 4 — Country Blocking

Business only operates in:

United States and Canada.

Need to block web traffic from:

Certain countries.

Choose:

**WAF Geographic Match**

---

## Scenario 5 — Request Flood From One IP

Single IP sends:

Thousands of HTTP requests per minute.

Choose:

**WAF Rate-Based Rule**

---

## Scenario 6 — Massive DDoS Attack

Application experiences:

**Large-scale DDoS**

Think:

**Shield**

and potentially WAF for:

**Layer 7 filtering**

---

## Scenario 7 — Port 22 Should Be Blocked

Need to stop:

**SSH traffic**

Do NOT choose WAF.

Think:

**Security Group / NACL**

---

## Scenario 8 — Public API Attack

API Gateway API receives:

**Malicious web payloads**

Choose:

**WAF + API Gateway**

---

## Scenario 9 — Test New Rule

Security team wants to see:

**Which requests would match**

without blocking them.

Choose:

**Count Mode**

---

# Scenario Recognition

Immediately think:

**WAF**

when you see:

- SQL injection
- XSS
- Web exploit
- Malicious HTTP request
- IP blocking
- Geographic blocking
- Rate-based web protection
- Bot traffic
- Web ACL

---

## Think Shield When You See

- DDoS
- Volumetric attack
- Infrastructure-level attack
- Advanced DDoS protection

---

## Think Security Groups When You See

- Ports
- Protocols
- EC2 network access

---

## Think Network Firewall When You See

- VPC network filtering
- Stateful network inspection
- Network traffic rules

---

# Exam Traps

## Trap 1 — WAF Protects Against Every DDoS Attack by Itself

❌

Think:

**Shield**

for DDoS protection.

---

## Trap 2 — WAF Controls EC2 SSH Access

❌

Think:

**Security Groups**

---

## Trap 3 — WAF Is an Authentication Service

❌

Think:

Cognito / IAM / Authorizer

---

## Trap 4 — WAF Provides HTTPS Certificates

❌

Think:

**ACM**

---

## Trap 5 — WAF Operates at the Subnet Layer

❌

Think:

**NACL**

WAF operates at:

**Application Layer**

---

## Trap 6 — Rate-Based Rule and API Throttling Are Identical

❌

WAF:

**Security filtering**

API throttling:

**Traffic/capacity control**

---

## Trap 7 — New Rules Must Immediately Block Traffic

❌

Use:

**Count Mode**

to test first.

---

# Quick Cheat Sheet

| Exam Clue | Answer |
|---|---|
| Web Application Firewall | WAF |
| SQL Injection | WAF |
| XSS | WAF |
| Malicious IP Blocking | IP Set |
| Country Blocking | Geographic Match |
| Excessive Requests From Source | Rate-Based Rule |
| Prebuilt Web Attack Rules | Managed Rule Groups |
| Test Rule Without Blocking | Count |
| DDoS | Shield |
| Port/Protocol Filtering | Security Group / NACL |
| VPC Network Inspection | Network Firewall |
| HTTPS Certificate | ACM |
| User Authentication | Cognito / IAM |

---

# Security Decision Map

Need:

**SQL injection / XSS protection**

→ WAF

Need:

**DDoS protection**

→ Shield

Need:

**Port-level EC2 access control**

→ Security Group

Need:

**Subnet-level filtering**

→ NACL

Need:

**VPC network inspection**

→ Network Firewall

Need:

**HTTPS certificate**

→ ACM

Need:

**User authentication**

→ Cognito / IAM

---

# WAF vs Shield

| Requirement | WAF | Shield |
|---|---:|---:|
| SQL Injection | ✅ | ❌ |
| XSS | ✅ | ❌ |
| HTTP Rule Filtering | ✅ | ❌ |
| IP Blocking | ✅ | Limited Different Purpose |
| DDoS Protection | Limited Layer 7 Assistance | ✅ |
| Web ACL | ✅ | ❌ |
| Rate-Based Web Rules | ✅ | ❌ |

---

# Final Exam Rapid-Fire

> **SQL INJECTION**
> → WAF
>
> **XSS**
> → WAF
>
> **WEB ACL**
> → WAF
>
> **BAD IP**
> → IP SET
>
> **COUNTRY BLOCK**
> → GEO MATCH
>
> **TOO MANY REQUESTS FROM ONE IP**
> → RATE-BASED RULE
>
> **PREBUILT PROTECTION**
> → MANAGED RULE GROUP
>
> **TEST RULE**
> → COUNT MODE
>
> **BOT TRAFFIC**
> → WAF BOT CONTROL
>
> **DDoS**
> → SHIELD
>
> **PORT FILTERING**
> → SECURITY GROUP / NACL
>
> **HTTPS**
> → ACM
>
> **AUTHENTICATION**
> → COGNITO / IAM

---

## Master Memory Trick

> [!tip] WAF Master Memory Trick
> Imagine your application is:
>
> **A nightclub**
>
> The Internet sends people to the door.
>
> WAF is:
>
> **THE SECURITY GUARD**
>
> Someone brings:
>
> **SQL INJECTION**
>
> → Block
>
> Someone brings:
>
> **XSS**
>
> → Block
>
> Known troublemaker IP?
>
> → Block
>
> Someone keeps rushing the door thousands of times?
>
> → Rate-Based Rule
>
> But suddenly:
>
> **A giant mob tries to overwhelm the entire building**
>
> That's:
>
> **DDoS**
>
> Call:
>
> **SHIELD**

So remember:

> **WAF**
> → FILTER WEB REQUESTS
>
> **WEB ACL**
> → RULE CONTAINER
>
> **MANAGED RULE**
> → PREBUILT PROTECTION
>
> **IP SET**
> → BLOCK/ALLOW IPS
>
> **RATE RULE**
> → ABUSIVE REQUEST RATE
>
> **SHIELD**
> → DDoS
>
> **SECURITY GROUP**
> → PORTS
>
> **ACM**
> → CERTIFICATE

And the killer SAA question:

> **"Does the requirement involve inspecting HTTP(S) requests for malicious patterns such as SQL injection, XSS, abusive IPs, or bots?"**
>
> YES
>
> → **WAF**

---

## Related Notes

- [[06-Security/Shield]]
- [[CloudFront]]
- [[Application Load Balancer]]
- [[API Gateway]]
- [[ACM]]
- [[Cognito]]
- [[CloudWatch]]
- [[20-SAA/15-Security/Network Firewall]]