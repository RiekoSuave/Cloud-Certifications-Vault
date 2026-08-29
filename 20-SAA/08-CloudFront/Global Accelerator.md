## What Problem Does It Solve?

[[Global Accelerator]] improves application performance for global users by routing traffic onto the:

**AWS Global Network**

as quickly as possible.

It solves the problem of:

> **"How can global users reach my application with lower latency and more consistent network performance?"**

Without Global Accelerator:

Global User  
↓  
Public Internet  
↓  
Many Network Hops  
↓  
AWS Application

With Global Accelerator:

Global User  
↓  
Nearest AWS Edge Location  
↓  
AWS Global Network  
↓  
Application

> [!tip] Memory Trick
> **Global Accelerator = Get onto AWS's highway sooner**

---

## Why Global Accelerator Exists

Imagine an application behind a:

[[Application Load Balancer]]

in one AWS Region.

Users are located in:

- North America
- Europe
- India
- Australia

Without Global Accelerator:

Users  
↓  
Public Internet  
↓  
Multiple Network Hops  
↓  
Application

More public internet hops can mean:

- Higher latency
- Less consistent performance
- More unpredictable routing

Global Accelerator moves traffic onto:

**AWS's private global network**

earlier in the request path.

---

# Core Architecture

Architecture:

Global Users  
↓  
Global Accelerator  
↓  
Nearest Edge Location  
↓  
AWS Global Network  
↓  
Regional Application

The Maarek slides emphasize:

**AWS internal network**

as the primary performance advantage.

### Memory Trick

**Public Internet = Variable Road**

**AWS Network = Express Lane**

---

# Anycast IP Addresses

Global Accelerator creates:

**2 static Anycast IP addresses**

for your application.

These IP addresses remain associated with the accelerator.

Architecture:

Users Worldwide  
↓  
Same Anycast IPs  
↓  
Nearest AWS Edge Location  
↓  
Application

> [!tip] Exam Number
> **Global Accelerator = 2 Anycast IPs**

---

# What Is Anycast?

Anycast means:

**Multiple locations advertise the same IP address**

and users are routed toward the:

**Nearest appropriate location**

Conceptually:

Edge Location A  
→ `12.34.56.78`

Edge Location B  
→ `12.34.56.78`

Edge Location C  
→ `12.34.56.78`

User connects to:

`12.34.56.78`

and network routing directs the user toward a nearby Edge Location.

---

# Anycast vs Unicast

## Unicast

One IP address identifies:

**One endpoint/location**

Example:

Server A  
→ IP A

Server B  
→ IP B

---

## Anycast

Multiple locations advertise:

**The same IP**

The user is routed toward:

**The nearest location**

### Memory Trick

**UNI = One**

**ANY = Same IP from many places**

---

# Global Accelerator Request Flow

Example:

User in Australia  
↓  
Global Accelerator Anycast IP  
↓  
Nearby AWS Edge Location  
↓  
AWS Global Network  
↓  
ALB in U.S.

Instead of:

Australia  
↓  
Public Internet across the entire distance  
↓  
U.S. ALB

This reduces dependency on long-distance public internet routing.

---

# Supported Endpoints

Global Accelerator works with several AWS endpoints.

The Maarek slides highlight:

- Elastic IP
- [[EC2]]
- [[Application Load Balancer]]
- [[Network Load Balancer]]

These endpoints can be:

**Public or private**

depending on the supported architecture.

---

# Application Load Balancer

Architecture:

Global User  
↓  
Global Accelerator  
↓  
AWS Edge Location  
↓  
[[Application Load Balancer]]  
↓  
Application

Use when:

The application is HTTP/S-based but needs:

- Static IP addresses
- Fast regional failover
- Consistent global network performance

---

# Network Load Balancer

Architecture:

Global User  
↓  
Global Accelerator  
↓  
AWS Edge  
↓  
[[Network Load Balancer]]  
↓  
Application

This is especially relevant when the application uses:

**TCP or UDP**

---

# EC2

Global Accelerator can also target:

[[EC2]]

instances.

Architecture:

User  
↓  
Global Accelerator  
↓  
AWS Network  
↓  
EC2

---

# Elastic IP

Global Accelerator also supports endpoints using:

**Elastic IP addresses**

This can be useful when applications already expose resources through static AWS IP addresses.

---

# Consistent Performance

One of the key benefits of Global Accelerator is:

**Consistent Performance**

Why?

Traffic enters:

**AWS's network**

near the user rather than spending most of its journey across the public internet.

Architecture:

User  
↓  
Nearest Edge  
↓  
AWS Backbone  
↓  
Application

This provides a more predictable network path.

---

# Intelligent Routing

Global Accelerator intelligently routes users toward:

**The lowest-latency healthy endpoint**

Architecture:

User  
↓  
Global Accelerator  
↓  
Evaluate Endpoints  
↓  
Lowest-Latency Healthy Endpoint

This provides both:

**Performance**

and:

**Availability**

---

# Health Checks

Global Accelerator performs:

**Health Checks**

against application endpoints.

If an endpoint becomes unhealthy:

Global Accelerator can redirect traffic toward:

**A healthy endpoint**

Architecture:

Region A  
↓  
Unhealthy ❌

Region B  
↓  
Healthy ✅

Global Accelerator  
↓  
Route Users to Region B

> [!tip] Memory Trick
> **Global Accelerator = Speed + Health-Aware Routing**

---

# Fast Regional Failover

Because Global Accelerator performs health checks:

It can provide:

**Fast regional failover**

The Maarek slides indicate failover for unhealthy applications can happen in:

**Less than 1 minute**

This makes Global Accelerator useful for:

**Disaster Recovery**

---

# Global Accelerator for Disaster Recovery

Example:

Primary Region  
↓  
ALB

Secondary Region  
↓  
ALB

Global Accelerator  
↓  
Health Checks Both Regions

Primary Healthy  
↓  
Traffic → Primary

Primary Fails  
↓  
Traffic → Secondary

### Architecture Thinking

If the requirement says:

> **"Global application requires fast deterministic regional failover."**

Think:

[[Global Accelerator]]

---

# Static IP Addresses

Another major benefit:

Global Accelerator provides:

**2 static Anycast IP addresses**

These remain stable even when the backend architecture changes.

That means clients do not need to track changing:

- Load Balancer addresses
- Regional endpoints
- DNS responses

### Memory Trick

**Backend changes**

but:

**Global Accelerator IPs stay the same**

---

# Why Static IPs Matter

Some applications or enterprise networks require:

**IP allowlisting**

Example:

Corporate Firewall  
↓  
Allow Only Known Destination IPs

Global Accelerator provides:

**Two stable external IP addresses**

So the organization only needs to whitelist those two addresses.

> [!tip] Exam Pattern
> **Global application + static IP requirement**
>
> → **Global Accelerator**

---

# Client DNS Cache Problem

DNS-based failover can sometimes be affected by:

**Client DNS caching**

Suppose DNS changes:

Old Endpoint  
↓  
New Endpoint

But client still has:

**Old DNS result cached**

Traffic may continue going to the wrong endpoint temporarily.

Global Accelerator avoids this issue because:

**The IP address does not change**

The routing behind that IP changes instead.

### Memory Trick

**DNS changes destination**

**Global Accelerator keeps IP, changes route**

---

# DDoS Protection

Global Accelerator integrates with:

[[06-Security/Shield]]

for:

**DDoS protection**

Architecture:

Attack Traffic  
↓  
Global Accelerator  
↓  
Shield  
↓  
Application

CloudFront also integrates with Shield.

This similarity becomes important when comparing:

[[Global Accelerator]]

with:

[[CloudFront]]

---

# Global Accelerator vs CloudFront

This is one of the biggest exam comparisons in this section.

Both:

- Use AWS global network
- Use Edge Locations
- Improve global performance
- Integrate with [[06-Security/Shield]]

But:

**They solve different problems**

---

# CloudFront

[[CloudFront]] focuses on:

**Content Delivery**

Works especially well for:

- Images
- Videos
- Static files
- Websites
- APIs
- Dynamic HTTP content

CloudFront can:

**Cache content at the edge**

Architecture:

User  
↓  
CloudFront Edge  
↓  
Cached Content

---

# Global Accelerator

Global Accelerator focuses on:

**Network acceleration**

for:

- TCP
- UDP
- HTTP/S
- Applications requiring static IPs

Global Accelerator:

**Does NOT primarily cache content**

Instead:

Edge Location  
↓  
Proxies network traffic  
↓  
Application in AWS Region

> [!tip] Master Difference
> **CloudFront = CONTENT**
>
> **Global Accelerator = CONNECTION**

---

# TCP and UDP

Global Accelerator supports:

**TCP and UDP**

This makes it useful for applications CloudFront is not designed to serve as a CDN.

Examples:

- Online gaming
- IoT
- Voice over IP
- Other non-HTTP applications

### Exam Pattern

> **UDP application + global users**
>
> → **Global Accelerator**

---

# Gaming

Gaming applications often require:

- Low latency
- UDP
- Consistent network paths

Architecture:

Player  
↓  
Global Accelerator  
↓  
Nearest Edge  
↓  
AWS Global Network  
↓  
Game Server

This is a strong Global Accelerator exam scenario.

---

# IoT

The Maarek slides highlight:

**MQTT**

as an example of a non-HTTP protocol where Global Accelerator may fit.

Architecture:

IoT Device  
↓  
TCP Connection  
↓  
Global Accelerator  
↓  
AWS Application

---

# Voice over IP

VoIP applications require:

- Low latency
- Stable network performance
- Often UDP

Think:

[[Global Accelerator]]

rather than CloudFront.

---

# Global Accelerator vs CloudFront Decision

## Choose CloudFront When You Need

- CDN
- Content caching
- Images/videos
- Static content
- Dynamic HTTP delivery
- API acceleration
- Edge content delivery

---

## Choose Global Accelerator When You Need

- TCP
- UDP
- Static Anycast IPs
- Gaming
- IoT
- VoIP
- Fast regional failover
- Deterministic global network performance

---

# Architecture Thinking

## Scenario 1 — Global UDP Game

A multiplayer gaming application runs in AWS.

Users worldwide require:

- Low latency
- UDP support
- Fast routing to the application

**Choose → Global Accelerator**

---

## Scenario 2 — Static Website Images

A company serves static images from S3 to global users.

The content is highly cacheable.

**Do NOT choose Global Accelerator as the primary answer**

Choose:

[[CloudFront]]

---

## Scenario 3 — Static IP Requirement

Enterprise clients must whitelist the public IP addresses used by an application.

The application runs behind multiple regional load balancers.

**Choose → Global Accelerator**

Why?

It provides:

**2 static Anycast IPs**

---

## Scenario 4 — Fast Regional Failover

A global application runs in two AWS Regions.

If the primary becomes unhealthy, traffic should quickly move to the secondary Region.

**Choose → Global Accelerator**

Why?

It performs:

**Health Checks + Fast Regional Failover**

---

## Scenario 5 — Global Video Delivery

A company distributes video files worldwide.

The videos should be cached close to users.

**Choose → CloudFront**

Why?

The requirement is:

**Content caching**

---

## Scenario 6 — VoIP Application

A voice application requires:

- UDP
- Global performance
- Low latency

**Choose → Global Accelerator**

---

## Scenario 7 — API with Static IP Requirement

A global HTTP API requires:

**Static public IP addresses**

Clients use strict firewall allowlists.

**Choose → Global Accelerator**

Even though HTTP is supported by CloudFront, the key requirement is:

**Static IP**

---

# Global Accelerator vs Route 53

Both can route users between application endpoints.

But they work differently.

## [[Route 53]]

Uses:

**DNS**

Architecture:

DNS Query  
↓  
Route 53  
↓  
Endpoint Address

Routing decisions may depend on:

- Latency
- Geography
- Health
- Weighted policies

---

## Global Accelerator

Uses:

**Static Anycast IPs**

Architecture:

Client  
↓  
Static Anycast IP  
↓  
Nearest Edge  
↓  
Healthy Application Endpoint

### Memory Trick

**Route 53 = DNS Routing**

**Global Accelerator = Network Routing**

---

# Global Accelerator vs Route 53 Failover

Route 53 failover may require clients to:

**Resolve DNS changes**

Global Accelerator keeps:

**The same IP addresses**

and changes:

**Where traffic is routed**

This can provide faster and more deterministic failover for certain workloads.

---

# Global Accelerator vs CloudFront vs Route 53

| Requirement | CloudFront | Global Accelerator | Route 53 |
|---|---:|---:|---:|
| CDN | ✅ | ❌ | ❌ |
| Cache Content | ✅ | ❌ | ❌ |
| TCP / UDP Acceleration | ❌ | ✅ | ❌ |
| Static Anycast IPs | ❌ | ✅ | ❌ |
| DNS | ❌ | ❌ | ✅ |
| Edge Locations | ✅ | ✅ | ❌ as CDN |
| HTTP/S | ✅ | ✅ | DNS only |
| Fast Regional Failover | Possible architectures | ✅ Strong Fit | ✅ |
| Gaming / UDP | ❌ | ✅ | Routing only |
| Static Images / Video | ✅ | ❌ | Routing only |

---

# Scenario Recognition

## Immediately Think Global Accelerator When You See

- Static Anycast IP
- Two static IP addresses
- TCP
- UDP
- Gaming
- VoIP
- MQTT
- Fast regional failover
- Global application
- AWS global network
- Health checks
- Deterministic routing
- Client IP allowlisting
- Avoid DNS cache issues

### Strongest Exam Patterns

> **"Global TCP/UDP application needs lower latency."**
>
> → **Global Accelerator**

> **"Global application requires static IP addresses."**
>
> → **Global Accelerator**

---

# Exam Traps

## Trap 1 — Global Accelerator Caches Content

False.

That is primarily:

[[CloudFront]]

Global Accelerator:

**Proxies network traffic**

---

## Trap 2 — CloudFront and Global Accelerator Are Identical

False.

CloudFront:

**Content delivery**

Global Accelerator:

**Network acceleration**

---

## Trap 3 — Global Accelerator Only Supports HTTP

False.

It supports:

**TCP + UDP**

---

## Trap 4 — Global Accelerator Uses Changing IP Addresses

False.

It provides:

**2 static Anycast IPs**

---

## Trap 5 — Global Accelerator Uses Only the Public Internet

False.

One of its major benefits is:

**AWS internal global network**

---

## Trap 6 — Anycast Means Every Server Has a Different IP

False.

Anycast means:

**Multiple locations advertise the same IP**

---

## Trap 7 — Global Accelerator Has No Health Checks

False.

Health checks are central to:

**Fast failover**

---

## Trap 8 — CloudFront Is Better for UDP Gaming

False.

Think:

[[Global Accelerator]]

---

# Quick Cheat Sheet

| Requirement | Best Choice |
|---|---|
| Global Network Acceleration | Global Accelerator |
| Static Anycast IPs | Global Accelerator |
| Number of Static IPs | 2 |
| TCP | ✅ |
| UDP | ✅ |
| Gaming | Global Accelerator |
| IoT / MQTT | Global Accelerator |
| VoIP | Global Accelerator |
| Health Checks | ✅ |
| Fast Regional Failover | ✅ |
| AWS Global Network | ✅ |
| Shield Integration | ✅ |
| Content Caching | CloudFront |
| Static Images / Videos | CloudFront |
| DNS Routing | Route 53 |

---

## Master Memory Trick

> [!tip] Master Memory Trick
> **Global Accelerator = Two permanent entrances to AWS's global highway**
>
> **TWO ANYCAST IPs**
>
> → Users always know where to connect
>
> **EDGE LOCATION**
>
> → Get onto AWS network quickly
>
> **AWS GLOBAL NETWORK**
>
> → Fast predictable travel
>
> **HEALTH CHECKS**
>
> → Avoid broken destinations
>
> **FAILOVER**
>
> → Route toward healthy Region

Remember:

> **CloudFront = CACHE the content**
>
> **Global Accelerator = CARRY the connection**
>
> **Route 53 = CHOOSE through DNS**

And the killer clues:

**TCP / UDP**
→ Global Accelerator

**Static IP**
→ Global Accelerator

**Gaming / VoIP**
→ Global Accelerator

**Cached images/videos**
→ CloudFront

---

## Related Notes

- [[CloudFront]]
- [[CloudFront Caching]]
- [[Application Load Balancer]]
- [[Network Load Balancer]]
- [[EC2]]
- [[Route 53]]
- [[Route 53 Latency-Based Routing]]
- [[Route 53 Failover Routing]]
- [[06-Security/Shield]]
- [[S3]]