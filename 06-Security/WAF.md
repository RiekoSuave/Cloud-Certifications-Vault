See also: [Shield](06-Security/Shield.md)

## What Problem Does It Solve?

Protects web applications from common web exploits and malicious web traffic.

AWS WAF stands for:

Web Application Firewall

WAF operates at:

Layer 7

Layer 7 is associated with:

HTTP

### Memory Trick

WAF = Web Firewall

---

## Type

Web Security

---

## What Is AWS WAF?

AWS WAF protects web applications by inspecting incoming web requests and applying rules that determine which traffic should be allowed or blocked.

Think:

Internet Traffic

↓

AWS WAF

↓

Inspect Web Requests

↓

Allow / Block

↓

Web Application

### Memory Trick

WAF = Filter Web Requests

---

## Layer 7 Protection

Your course emphasizes that WAF operates at:

Layer 7

This is the application layer where:

HTTP

traffic operates.

Your course contrasts this with:

Layer 4 = TCP

### Memory Trick

WAF = Layer 7 = HTTP

---

## Where Can WAF Be Deployed?

Your course identifies three important AWS services:

- Application Load Balancer (ALB)
- Amazon API Gateway
- Amazon CloudFront

### Memory Trick

WAF Protects:

ALB + API Gateway + CloudFront

---

## Web ACL

AWS WAF uses:

Web ACL

which stands for:

Web Access Control List

A Web ACL contains rules that determine how incoming web requests should be handled.

Think:

Web Request

↓

Web ACL Rules

↓

Allow / Block

### Memory Trick

Web ACL = WAF Rules

---

## WAF Rules

Your course identifies several things WAF rules can inspect.

Rules can include:

- IP address
- HTTP headers
- HTTP body
- URI strings

This allows WAF to filter requests based on characteristics of incoming web traffic.

### Memory Trick

WAF Rules = Inspect the Web Request

---

## SQL Injection

AWS WAF can help protect web applications from:

SQL Injection

This is one of the common web attacks specifically identified in your course.

### Memory Trick

SQL Injection?

→ WAF

---

## Cross-Site Scripting (XSS)

AWS WAF can also help protect against:

Cross-Site Scripting

or:

XSS

This is another common Layer 7 web exploit identified in your course.

### Memory Trick

XSS?

→ WAF

---

## Geo-Match

WAF supports:

Geo-Match

This allows rules to filter traffic based on geographic location.

Your course gives the example of:

Blocking Countries

### Memory Trick

Block Traffic by Country

→ WAF Geo-Match

---

## Size Constraints

WAF rules can also use:

Size Constraints

This allows WAF to evaluate web requests based on their size.

---

## Rate-Based Rules

AWS WAF supports:

Rate-Based Rules

These rules can count occurrences of events and help respond when too many requests are coming from a source.

Your course associates rate-based rules with:

DDoS Protection

### Memory Trick

Too Many Web Requests?

→ WAF Rate-Based Rule

---

## WAF vs Shield

This is an important distinction.

### AWS WAF

Protects against:

Malicious Web Requests

Think:

Layer 7 / HTTP

### AWS Shield

Protects against:

DDoS Attacks

Think:

Traffic Floods

| WAF | Shield |
|---|---|
| Web Application Firewall | DDoS Protection |
| Layer 7 | Layer 3 / Layer 4 emphasized for Shield Standard |
| HTTP traffic | Traffic floods |
| Rule-based filtering | DDoS mitigation |
| SQL Injection / XSS | SYN / UDP floods |

### Memory Trick

WAF = Filter the Requests

Shield = Stop the Flood

See:

[Shield](06-Security/Shield.md)

---

## Common Use Cases

- Protecting web applications
- Protecting APIs
- Filtering malicious web requests
- Blocking IP addresses
- Blocking traffic by country
- Protecting against SQL injection
- Protecting against XSS
- Rate-based web traffic filtering

---

## Scenario Questions

A company wants to protect a web application from SQL injection attacks.

→ AWS WAF

---

A company wants to protect a web application from cross-site scripting (XSS).

→ AWS WAF

---

A company wants to filter incoming HTTP requests based on IP address.

→ AWS WAF

---

A company wants to block web traffic from specific countries.

→ AWS WAF Geo-Match

---

A company wants to apply web security rules to an Application Load Balancer.

→ AWS WAF

---

A company wants to protect an API Gateway API from malicious web requests.

→ AWS WAF

---

A company wants to protect CloudFront from malicious web requests.

→ AWS WAF

---

A company wants protection against DDoS traffic floods.

→ AWS Shield

---

## Don't Confuse These

WAF = Web Application Firewall

Web ACL = WAF Rules

WAF = Layer 7

Layer 7 = HTTP

Shield = DDoS Protection

### Memory Trick

WAF = Web Requests

Shield = DDoS

---

## Exam Keywords

AWS WAF

Web Application Firewall

Layer 7

HTTP

Web ACL

SQL Injection

Cross-Site Scripting

XSS

Geo-Match

Rate-Based Rules

IP Address

HTTP Headers

HTTP Body

URI Strings

---

## Quick Cheat Sheet

WAF = Web Firewall

WAF = Layer 7

Layer 7 = HTTP

Web ACL = WAF Rules

WAF → ALB

WAF → API Gateway

WAF → CloudFront

SQL Injection = WAF

XSS = WAF

Block Countries = Geo-Match

Rate-Based Rules = Count Requests

Shield = DDoS Protection