See also: [WAF](06-Security/WAF.md)

## What Problem Does It Solve?

Protects AWS applications against Distributed Denial of Service (DDoS) attacks.

A DDoS attack attempts to overwhelm an application with large amounts of malicious traffic, making the application unavailable to legitimate users.

### Memory Trick

Shield = DDoS Protection

---

## Type

DDoS Protection

---

## What Is AWS Shield?

AWS Shield protects applications running on AWS against:

Distributed Denial of Service (DDoS) attacks

Your course divides Shield into two levels:

1. Shield Standard
2. Shield Advanced

### Memory Trick

Shield = Protect Against Traffic Floods

---

## Shield Standard

AWS Shield Standard provides basic DDoS protection.

Your course emphasizes that Shield Standard is:

FREE

and

Automatically Activated for Every AWS Customer

You do not need to purchase Shield Standard separately.

### Memory Trick

Shield Standard = Free + Automatic

---

## What Does Shield Standard Protect Against?

Your course gives examples including:

- SYN floods
- UDP floods
- Reflection attacks
- Other Layer 3 attacks
- Other Layer 4 attacks

The important exam concept is:

Shield Standard protects against common network and transport-layer DDoS attacks.

### Memory Trick

Standard = Basic DDoS Protection

---

## Shield Advanced

AWS Shield Advanced provides additional protection against more sophisticated DDoS attacks.

Unlike Shield Standard:

Shield Advanced is optional and paid.

Your course lists the price as:

$3,000 per month per organization

For exam purposes, the more important concept is:

Shield Advanced = Paid Advanced DDoS Protection

---

## Resources Protected by Shield Advanced

Your course identifies protection for resources such as:

- Amazon EC2
- Elastic Load Balancing (ELB)
- Amazon CloudFront
- AWS Global Accelerator
- Amazon Route 53

### Memory Trick

Advanced = Protect Important Internet-Facing AWS Resources

---

## DDoS Response Team

Shield Advanced provides:

24/7 access to the AWS DDoS Response Team

Your course refers to this as:

DRP

This provides additional support during DDoS attacks.

### Memory Trick

Shield Advanced = 24/7 DDoS Help

---

## Cost Protection

A DDoS attack can cause resource usage to increase significantly.

Your course notes that Shield Advanced provides protection against higher AWS fees resulting from usage spikes caused by DDoS attacks.

### Memory Trick

Shield Advanced = DDoS Cost Protection

---

## Shield Standard vs Shield Advanced

| Shield Standard | Shield Advanced |
|---|---|
| Free | Paid |
| Automatically enabled | Optional |
| Basic DDoS protection | Advanced DDoS protection |
| Common Layer 3 / Layer 4 attacks | More sophisticated attacks |
| Basic protection | 24/7 DDoS response support |
| — | DDoS cost protection |

### Memory Trick

Standard = Free Protection

Advanced = More Protection + Support

---

## Shield vs WAF

This is an important distinction.

### AWS Shield

Protects against:

DDoS Attacks

Think:

Traffic Flood

### AWS WAF

Filters:

Web Requests

Think:

Malicious HTTP Requests

| Shield | WAF |
|---|---|
| DDoS protection | Web application firewall |
| Protects availability | Filters web traffic |
| Traffic floods | HTTP request rules |
| Layer 3 / 4 protection emphasized by Shield Standard | Layer 7 protection |

### Memory Trick

Shield = Stop the Flood

WAF = Filter the Requests

See:

[WAF](06-Security/WAF.md)

---

## Common Use Cases

- DDoS protection
- Protecting web applications
- Protecting internet-facing AWS resources
- Advanced DDoS mitigation
- Protecting against DDoS-related cost increases

---

## Scenario Questions

A company wants basic DDoS protection at no additional cost.

→ Shield Standard

---

A company wants automatic DDoS protection for its AWS environment.

→ Shield Standard

---

A company needs advanced protection against sophisticated DDoS attacks.

→ Shield Advanced

---

A company wants 24/7 access to an AWS DDoS response team.

→ Shield Advanced

---

A company wants protection against higher AWS charges caused by a DDoS attack.

→ Shield Advanced

---

A company wants to filter malicious HTTP requests based on rules.

→ AWS WAF

NOT Shield

---

## Don't Confuse These

Shield = DDoS Protection

Shield Standard = Free + Automatic

Shield Advanced = Paid + Advanced Protection

WAF = Web Traffic Filtering

### Memory Trick

Shield = DDoS

WAF = Web Firewall

---

## Exam Keywords

AWS Shield

DDoS

Shield Standard

Shield Advanced

SYN Flood

UDP Flood

Reflection Attack

Layer 3

Layer 4

DDoS Response Team

Cost Protection

---

## Quick Cheat Sheet

Shield = DDoS Protection

Shield Standard = Free

Shield Standard = Automatically Enabled

Shield Standard = Layer 3 / Layer 4 DDoS Protection

Shield Advanced = Paid

Shield Advanced = Advanced DDoS Protection

Shield Advanced = 24/7 DDoS Support

Shield Advanced = DDoS Cost Protection

WAF = Filter Web Requests