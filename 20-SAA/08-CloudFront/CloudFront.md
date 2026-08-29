## What Problem Does It Solve?

[[CloudFront]] is AWS's global **Content Delivery Network (CDN)**.

It solves the problem of:

> **"How can I deliver content to users around the world with lower latency and better performance?"**

Instead of every user retrieving content directly from the origin:

User  
↓  
Public Internet  
↓  
Origin

CloudFront places cached content closer to users:

User  
↓  
Nearest CloudFront Edge Location  
↓  
Cached Content

If the content is not cached:

User  
↓  
Edge Location  
↓  
Origin  
↓  
Edge Cache  
↓  
User

> [!tip] Memory Trick
> **CloudFront = Bring the content closer to the user**

---

## Why CloudFront Exists

Imagine an application hosted in:

**United States**

Users are located in:

- United States
- Europe
- Asia
- Australia
- Africa

Without CloudFront:

Global User  
↓  
Long Network Distance  
↓  
Origin in U.S.  
↓  
Higher Latency

Every request may need to travel all the way back to the origin.

With CloudFront:

Global User  
↓  
Nearby Edge Location  
↓  
Cached Content

Result:

**Lower latency + faster reads + better user experience**

---

# CloudFront = CDN

CDN means:

**Content Delivery Network**

The main idea is:

Origin  
↓  
CloudFront  
↓  
Edge Locations Around the World  
↓  
Users

CloudFront has:

**Hundreds of Points of Presence globally**

These include:

- Edge Locations
- Caches

> [!tip] Memory Trick
> **CDN = Cache Data Nearby**

---

# CloudFront Improves Read Performance

CloudFront primarily improves:

**Read performance**

because content can be cached closer to users.

Architecture:

Origin  
↓  
Object / Content  
↓  
CloudFront Edge Cache  
↓  
User

Instead of repeatedly contacting the origin:

User 1  
↓  
Origin

User 2  
↓  
Origin

User 3  
↓  
Origin

CloudFront can serve:

User 1  
User 2  
User 3  
↓  
Nearby Edge Cache

This also reduces repeated requests reaching the origin.

---

# CloudFront Edge Locations

An:

**Edge Location**

is a CloudFront Point of Presence located closer to end users.

Think:

AWS Region  
↓  
Origin

versus:

User  
↓  
Nearby Edge Location  
↓  
AWS Network  
↓  
Origin

The Edge Location maintains a:

**Local Cache**

---

# CloudFront High-Level Architecture

The Maarek slides show the basic architecture as:

Client  
↓  
CloudFront Edge Location  
↓  
Local Cache

If requested content exists in cache:

Client  
↓  
Edge Location  
↓  
Cache Hit  
↓  
Content Returned

If it does not:

Client  
↓  
Edge Location  
↓  
Cache Miss  
↓  
Forward Request to Origin  
↓  
Origin Returns Content  
↓  
CloudFront Caches Content  
↓  
Content Returned to Client

---

# Cache Hit

A:

**Cache Hit**

means CloudFront already has the requested content stored at the Edge Location.

Architecture:

User  
↓  
CloudFront  
↓  
Local Cache  
↓  
Object Found ✅  
↓  
Return Object

The origin does not need to serve the object again.

### Result

- Faster response
- Lower latency
- Less origin traffic

---

# Cache Miss

A:

**Cache Miss**

means the requested content is not currently stored in the Edge Location cache.

Architecture:

User  
↓  
CloudFront Edge  
↓  
Object Missing  
↓  
Origin  
↓  
Retrieve Object  
↓  
Cache Object  
↓  
Return to User

Future users may then receive the cached copy.

> [!tip] Memory Trick
> **HIT = Edge has it**
>
> **MISS = Edge must fetch it**

---

# What Is an Origin?

The:

**Origin**

is the backend where CloudFront retrieves the original content.

CloudFront supports several origin types.

The Maarek slides highlight:

1. S3 Bucket
2. VPC Origin
3. Custom HTTP Origin

---

# S3 Bucket Origin

One of the most common architectures is:

[[S3]]  
↓  
[[CloudFront]]  
↓  
Global Users

CloudFront can use an S3 bucket to:

- Distribute files
- Cache files at Edge Locations
- Upload files to S3 through CloudFront

Example:

Private S3 Bucket  
↓  
Images / Videos / Static Files  
↓  
CloudFront  
↓  
Global Users

### Common Content

- Images
- Videos
- CSS
- JavaScript
- Documents
- Downloads

---

# S3 + CloudFront Architecture

Without CloudFront:

User  
↓  
S3 Bucket

Every user accesses the S3 origin directly.

With CloudFront:

User  
↓  
Nearest Edge Location  
↓  
Cached S3 Object

Only when necessary:

Edge Location  
↓  
S3 Origin

This is one of the most important SAA architectures.

> [!tip] Exam Pattern
> **S3 static content + global users + low latency**
>
> → **CloudFront**

---

# Origin Access Control

An S3 origin can be secured using:

[[CloudFront Origin Access Control]]

or:

**OAC**

Architecture:

User  
↓  
CloudFront  
↓  
OAC  
↓  
Private S3 Bucket

The bucket can be configured so that:

**Only the CloudFront distribution can access it**

This prevents users from bypassing CloudFront and directly accessing the private S3 bucket.

> [!tip] Memory Trick
> **OAC = CloudFront's private doorway into S3**

We'll cover OAC in detail in its own note.

---

# VPC Origins

CloudFront can also access applications hosted inside:

**VPC private subnets**

The Maarek slides call this:

**VPC Origin**

Supported private resources include:

- Private [[Application Load Balancer]]
- Private [[Network Load Balancer]]
- Private [[EC2]]

Architecture:

Global User  
↓  
CloudFront  
↓  
VPC Origin  
↓  
Private ALB / NLB / EC2

This allows the application backend to remain:

**Private**

while CloudFront provides the global entry point.

---

# Custom HTTP Origins

CloudFront can also use:

**Custom HTTP Origins**

Examples include:

- S3 static website
- Public [[Application Load Balancer]]
- Any public HTTP backend

Architecture:

User  
↓  
CloudFront  
↓  
Public HTTP Origin

---

# S3 Static Website as an Origin

An S3 bucket configured for:

[[S3 Static Website Hosting]]

can be used as a:

**Custom HTTP Origin**

Important distinction:

Normal S3 Bucket Origin  
↓  
Can use OAC

S3 Website Endpoint  
↓  
Treated as Custom HTTP Origin

> [!warning] Exam Trap
> **S3 website endpoint = Custom Origin**

---

# CloudFront and Dynamic Content

CloudFront is not limited to static files.

It can also improve performance for:

**Dynamic content**

Example:

User  
↓  
CloudFront  
↓  
[[Application Load Balancer]]  
↓  
Application

Not every response must necessarily be cached.

CloudFront can still provide:

- Global network optimization
- Edge processing
- Security integration

### Exam Trap

Do not assume:

> **CloudFront = static content only**

CloudFront supports:

**Static + Dynamic content**

---

# CloudFront Security Benefits

Because CloudFront is globally distributed, it also provides security benefits.

The Maarek slides highlight integration with:

- [[06-Security/Shield]]
- [[06-Security/WAF]]

Architecture:

Internet  
↓  
CloudFront  
↓  
[[06-Security/WAF]]  
↓  
Origin

and:

Internet Attack  
↓  
CloudFront  
↓  
[[06-Security/Shield]]  
↓  
DDoS Protection

---

# DDoS Protection

CloudFront provides protection against:

**Distributed Denial of Service attacks**

because it operates across a large globally distributed infrastructure.

It integrates with:

[[06-Security/Shield]]

for additional DDoS protection.

> [!tip] Exam Pattern
> **Global content delivery + DDoS protection**
>
> → CloudFront + Shield

---

# CloudFront + WAF

[[06-Security/WAF]] can be associated with CloudFront.

This allows filtering of malicious HTTP/S requests.

Example:

Attacker  
↓  
CloudFront  
↓  
[[06-Security/WAF]]  
↓  
Blocked ❌

Legitimate User  
↓  
CloudFront  
↓  
WAF  
↓  
Origin ✅

WAF can protect against application-layer attacks and unwanted web traffic.

---

# CloudFront Does Not Replace the Origin

CloudFront is:

**Not the permanent source of truth**

The origin remains the authoritative backend.

Think:

Origin  
↓  
Original Content

CloudFront  
↓  
Cached Copies

If cached content expires or is missing:

CloudFront returns to:

**The Origin**

---

# Architecture Thinking

## Scenario 1 — Global Static Website

A company stores website assets in S3.

Users around the world experience high latency downloading:

- Images
- CSS
- JavaScript

**Choose:**

[[S3]]  
↓  
[[CloudFront]]

Why?

CloudFront caches the content at Edge Locations near users.

---

## Scenario 2 — Private S3 Content

A company wants users to access content through CloudFront.

Users must not directly access the S3 bucket.

**Choose:**

CloudFront  
+  
[[CloudFront Origin Access Control]]

Architecture:

User  
↓  
CloudFront  
↓  
OAC  
↓  
Private S3 Bucket

---

## Scenario 3 — Global Dynamic Application

A web application runs behind an:

[[Application Load Balancer]]

Global users experience high latency.

The company wants global HTTP content delivery and acceleration.

**Choose → CloudFront**

Origin:

Public ALB

---

## Scenario 4 — Private Application Backend

An application runs behind a private ALB inside private VPC subnets.

The company wants CloudFront as the global entry point.

**Choose → CloudFront VPC Origin**

---

## Scenario 5 — DDoS-Protected Global Website

A website needs:

- Global content delivery
- DDoS protection
- Web request filtering

Architecture:

User  
↓  
CloudFront  
↓  
[[06-Security/WAF]]  
↓  
Origin

with:

[[06-Security/Shield]]

providing DDoS protection.

---

# CloudFront vs S3

## [[S3]]

Stores:

**Objects**

---

## CloudFront

Distributes:

**Content globally**

### Memory Trick

**S3 = STORE**

**CloudFront = DELIVER**

They are often used together:

S3  
↓  
CloudFront  
↓  
Users

---

# CloudFront vs Route 53

## [[Route 53]]

Provides:

**DNS**

It answers:

> **Where should the client go?**

---

## CloudFront

Provides:

**Content delivery + caching**

It answers:

> **How can I serve the content quickly once the client arrives?**

### Memory Trick

**Route 53 = Find it**

**CloudFront = Deliver it**

---

# CloudFront vs Global Accelerator

Both use:

- AWS global infrastructure
- Edge Locations
- AWS global network

But their primary use cases differ.

## CloudFront

Best for:

**HTTP/S content delivery**

Can cache content at the edge.

---

## [[05-Networking/Global Accelerator]]

Best for:

**TCP / UDP application acceleration**

and situations requiring:

**Static Anycast IP addresses**

We'll compare these in detail later.

> [!tip] Quick Memory
> **CloudFront = CONTENT**
>
> **Global Accelerator = CONNECTION**

---

# Scenario Recognition

## Immediately Think CloudFront When You See

- CDN
- Global users
- Edge Locations
- Cache content
- Reduce latency
- Improve read performance
- S3 static content
- Global website
- Origin
- Cache Hit / Cache Miss
- WAF integration
- Shield integration
- Global HTTP/S delivery

### Strongest Exam Pattern

> **"Global users need low-latency access to content."**
>
> → **CloudFront**

---

# Exam Traps

## Trap 1 — CloudFront Stores the Original Data

False.

The:

**Origin**

stores the authoritative content.

CloudFront stores:

**Cached copies**

---

## Trap 2 — CloudFront Only Works with S3

False.

Origins can include:

- S3
- VPC Origins
- S3 Websites
- Public ALBs
- Other HTTP backends

---

## Trap 3 — CloudFront Is Static Content Only

False.

CloudFront can accelerate:

**Static and dynamic content**

---

## Trap 4 — Edge Location Is an AWS Region

False.

Edge Locations are:

**Points of Presence**

used to deliver content closer to users.

---

## Trap 5 — CloudFront Must Contact Origin for Every Request

False.

If the content is already cached:

**Cache Hit**

CloudFront can return it directly.

---

## Trap 6 — S3 Website Endpoint Uses OAC

Be careful.

An:

**S3 website endpoint**

is treated as a:

**Custom HTTP Origin**

Normal private S3 bucket origins are the classic OAC use case.

---

## Trap 7 — CloudFront and Route 53 Do the Same Thing

False.

Route 53:

**DNS**

CloudFront:

**CDN / Content Delivery**

---

# Quick Cheat Sheet

| Requirement | CloudFront |
|---|---|
| Content Delivery Network | ✅ |
| Global Edge Locations | ✅ |
| Cache Content at Edge | ✅ |
| Improve Read Performance | ✅ |
| Reduce Global Latency | ✅ |
| S3 Origin | ✅ |
| Private S3 with OAC | ✅ |
| VPC Origin | ✅ |
| Private ALB / NLB / EC2 Origin | ✅ |
| Custom HTTP Origin | ✅ |
| Static Content | ✅ |
| Dynamic Content | ✅ |
| Shield Integration | ✅ |
| WAF Integration | ✅ |
| Original Source of Truth | ❌ |
| DNS Service | ❌ |
| TCP/UDP Static Anycast IP Acceleration | Use Global Accelerator |

---

## Master Memory Trick

> [!tip] Master Memory Trick
> **CloudFront = Global Content Delivery**
>
> **ORIGIN**
>
> → Holds the original content
>
> **EDGE**
>
> → Holds cached copies close to users
>
> **USER**
>
> → Gets content from the nearest useful edge

Remember:

**HIT**
→ Edge already has it

**MISS**
→ Edge fetches from origin

And:

> **S3 = STORE**
>
> **CloudFront = DELIVER**
>
> **Route 53 = FIND**
>
> **Global Accelerator = ACCELERATE CONNECTIONS**

The killer exam phrase:

> **Global users + low latency + cached HTTP/S content**
>
> → **CloudFront**

---

## Related Notes

- [[S3]]
- [[CloudFront Origin Access Control]]
- [[CloudFront Caching]]
- [[CloudFront Cache Invalidations]]
- [[CloudFront Signed URLs]]
- [[CloudFront Signed Cookies]]
- [[CloudFront Geo Restriction]]
- [[Application Load Balancer]]
- [[Network Load Balancer]]
- [[EC2]]
- [[Route 53]]
- [[05-Networking/Global Accelerator]]
- [[06-Security/Shield]]
- [[06-Security/WAF]]