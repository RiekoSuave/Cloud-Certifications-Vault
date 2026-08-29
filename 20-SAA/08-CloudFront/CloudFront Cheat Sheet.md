## CloudFront Exam Strategy

For SAA questions, do not think of [[CloudFront]] as simply:

**"AWS CDN"**

Instead ask:

> **"Does this architecture need global content delivery, caching, private origin protection, viewer restrictions, or network acceleration?"**

| Requirement | Immediately Think |
|---|---|
| Global CDN | [[CloudFront]] |
| Cache content near users | [[CloudFront Caching]] |
| Private S3 behind CloudFront | [[CloudFront Origin Access Control]] |
| Force fresh cached content | [[CloudFront Cache Invalidations]] |
| Restrict by country | [[CloudFront Geo Restriction]] |
| Protect one private CloudFront file | [[CloudFront Signed URLs]] |
| Protect many private CloudFront files | [[CloudFront Signed Cookies]] |
| Static Anycast IPs | [[Global Accelerator]] |
| TCP / UDP global acceleration | [[Global Accelerator]] |
| Fast deterministic regional failover | [[Global Accelerator]] |

> [!tip] Master Question
> Ask:
>
> **CONTENT?**
>
> **CACHE?**
>
> **PRIVATE ORIGIN?**
>
> **VIEWER ACCESS?**
>
> **COUNTRY?**
>
> **STATIC IP?**
>
> **TCP / UDP?**
>
> **FAILOVER?**

---

## CloudFront Core Purpose

[[CloudFront]] is AWS's:

**Content Delivery Network**

or:

**CDN**

It uses globally distributed:

**Edge Locations**

to deliver content closer to users.

Architecture:

Origin  
↓  
CloudFront  
↓  
Edge Locations  
↓  
Global Users

### Memory Trick

**CloudFront = Bring the content closer**

---

## CloudFront Origins

CloudFront retrieves original content from:

**Origins**

Important origin types include:

- [[S3]]
- VPC Origins
- Public HTTP Origins
- [[Application Load Balancer]]
- [[Network Load Balancer]]
- [[EC2]]
- S3 Website Endpoints

---

## S3 Origin

Classic architecture:

Private [[S3]]  
↓  
[[CloudFront Origin Access Control]]  
↓  
CloudFront  
↓  
Global Users

Best for:

- Images
- Videos
- CSS
- JavaScript
- Documents
- Static downloads

---

## VPC Origins

CloudFront can deliver content from applications hosted inside:

**Private VPC subnets**

Supported private origins include:

- [[Application Load Balancer]]
- [[Network Load Balancer]]
- [[EC2]]

### Exam Pattern

> **CloudFront + private application backend**
>
> → **VPC Origin**

---

## S3 Website Endpoint

An:

[[S3 Static Website Hosting|S3 Website Endpoint]]

is treated as:

**Custom HTTP Origin**

This is different from a normal private S3 bucket origin.

> [!warning] Exam Trap
> **S3 Bucket Origin**
> → Can use OAC
>
> **S3 Website Endpoint**
> → Custom HTTP Origin

---

# CloudFront Caching

[[CloudFront Caching]] stores content at:

**Edge Locations**

Architecture:

User  
↓  
Edge Location  
↓  
Cached Object

This reduces:

- Latency
- Origin requests
- Origin workload

---

## Cache Hit

CloudFront already has the object.

User  
↓  
CloudFront  
↓  
Cache HIT  
↓  
Content Returned

Origin:

**Not contacted**

### Memory Trick

**HIT = Edge has it**

---

## Cache Miss

CloudFront does not have a valid cached copy.

User  
↓  
CloudFront  
↓  
Cache MISS  
↓  
Origin  
↓  
Retrieve Object  
↓  
Cache Object  
↓  
User

### Memory Trick

**MISS = Go home to origin**

---

# TTL

TTL means:

**Time To Live**

It controls how long CloudFront keeps cached content before it needs refreshing.

Long TTL:

- More cache hits
- Less origin traffic
- Potentially older content

Short TTL:

- Fresher content
- More origin requests

### Memory Trick

**TTL = How long CloudFront trusts the copy**

---

# CloudFront Cache Invalidations

[[CloudFront Cache Invalidations]] force cached content to refresh:

**Before TTL expiration**

Use when:

Origin Updated  
↓  
CloudFront Still Serving Old Content  
↓  
Cannot Wait for TTL

Choose:

**Invalidation**

---

## Invalidation Paths

Specific file:

`/index.html`

Directory-style path:

`/images/*`

Everything:

`*`

### Memory Trick

**TTL = WAIT**

**Invalidation = NOW**

---

# CloudFront Origin Access Control

[[CloudFront Origin Access Control]]

or:

**OAC**

lets CloudFront securely access a:

**Private S3 Bucket**

Architecture:

User  
↓  
CloudFront  
↓  
OAC  
↓  
Private S3

The S3 Bucket Policy should authorize:

**The CloudFront Distribution**

---

## OAC Purpose

OAC prevents users from:

**Bypassing CloudFront**

Bad architecture:

User  
↓  
CloudFront

but also:

User  
↓  
Public S3

Better:

User  
↓  
CloudFront  
↓  
OAC  
↓  
Private S3

Direct S3:

**Denied**

### Memory Trick

**OAC = CloudFront's private backstage pass**

---

# OAC + Bucket Policy

OAC and:

[[S3 Bucket Policies]]

work together.

OAC:

**Authenticates the CloudFront origin request**

Bucket Policy:

**Authorizes CloudFront to access S3**

### Exam Pattern

> **Only CloudFront may access S3**
>
> → **OAC + Bucket Policy**

---

# CloudFront Viewer Access vs Origin Access

This distinction is crucial.

## Viewer Access

Controls:

**User → CloudFront**

Tools:

- [[CloudFront Signed URLs]]
- [[CloudFront Signed Cookies]]
- [[CloudFront Geo Restriction]]

---

## Origin Access

Controls:

**CloudFront → S3**

Tool:

[[CloudFront Origin Access Control]]

### Memory Trick

**Viewer protection = FRONT DOOR**

**OAC = BACK DOOR**

---

# CloudFront Signed URLs

[[CloudFront Signed URLs]] restrict access to:

**Individual protected resources**

Best when:

- One file
- One video
- One download
- Temporary access

Example:

Paid User  
↓  
Signed URL  
↓  
CloudFront  
↓  
Private Content

### Memory Trick

**One File = Signed URL**

---

# CloudFront Signed Cookies

[[CloudFront Signed Cookies]] are better when users need access to:

**Multiple protected resources**

Example:

Premium Subscriber  
↓  
Signed Cookies  
↓  
CloudFront  
↓  
Entire Premium Content Set

Best when:

- Many files
- Existing URLs should remain unchanged
- Entire protected section of a site

### Memory Trick

**Many Files = Signed Cookies**

---

# Signed URLs vs Signed Cookies

| Requirement | Signed URL | Signed Cookies |
|---|---:|---:|
| One File | ✅ | Possible |
| Many Files | Less Convenient | ✅ |
| Temporary Access | ✅ | ✅ |
| Existing URLs Remain Unchanged | ❌ | ✅ |
| Viewer Authorization | ✅ | ✅ |

---

# CloudFront Signed URL vs S3 Pre-Signed URL

This is a very important exam distinction.

## CloudFront Signed URL

Access path:

User  
↓  
CloudFront  
↓  
Origin

Provides:

**Private content through the CDN**

---

## [[S3 Pre-Signed URLs]]

Access path:

User  
↓  
S3

Provides:

**Temporary direct S3 access**

### Memory Trick

**CloudFront Signed URL**
→ Through CDN

**S3 Pre-Signed URL**
→ Direct to S3

---

# CloudFront Geo Restriction

[[CloudFront Geo Restriction]] controls viewer access based on:

**Country**

CloudFront determines the viewer country using:

**Geo-IP**

Two modes:

- Allowlist
- Blocklist

---

## Allowlist

Only listed countries:

**Allowed**

Everyone else:

**Blocked**

### Memory Trick

**ONLY these countries**
→ Allowlist

---

## Blocklist

Listed countries:

**Blocked**

Everyone else:

**Allowed**

### Memory Trick

**EVERYWHERE except these**
→ Blocklist

---

# Geo Restriction Use Cases

Classic exam use case:

**Copyright / Licensing**

Example:

Content licensed only in:

- United States
- Canada

Choose:

**CloudFront Geo Allowlist**

---

# Geo Restriction vs Route 53 Geolocation

## CloudFront Geo Restriction

Purpose:

**ALLOW or BLOCK**

---

## [[Route 53 Geolocation Routing]]

Purpose:

**ROUTE**

### Memory Trick

**CloudFront Geo = BLOCK**

**Route 53 Geo = ROUTE**

---

# CloudFront vs S3 Cross-Region Replication

Both can help global access but work differently.

## CloudFront

Creates:

**Temporary Edge Cache**

Best for:

**Global content distribution**

---

## [[S3 Cross-Region Replication]]

Creates:

**Actual object copies in selected Regions**

Best for:

- Compliance
- Disaster recovery
- Permanent regional copies

### Memory Trick

**CloudFront = CACHE**

**CRR = COPY**

---

# Global Accelerator

[[Global Accelerator]] improves global application performance by routing traffic onto:

**AWS's global network**

as early as possible.

Architecture:

Global User  
↓  
Anycast IP  
↓  
Nearest Edge Location  
↓  
AWS Global Network  
↓  
Application

---

# Global Accelerator Anycast IPs

Global Accelerator creates:

**2 static Anycast IP addresses**

These IPs remain stable even if backend endpoints change.

> [!tip] Exam Number
> **Global Accelerator = 2 Anycast IPs**

---

# Anycast

Anycast means:

**Multiple locations advertise the same IP**

The user is routed toward:

**The nearest appropriate location**

### Memory Trick

**Same IP everywhere**

---

# Global Accelerator Supported Endpoints

Important endpoint types include:

- Elastic IP
- [[EC2]]
- [[Application Load Balancer]]
- [[Network Load Balancer]]

---

# Global Accelerator Health Checks

Global Accelerator monitors:

**Endpoint health**

If one endpoint becomes unhealthy:

Traffic  
↓  
Redirected  
↓  
Healthy Endpoint

This provides:

**Fast regional failover**

and makes Global Accelerator useful for:

**Disaster Recovery**

---

# Static IP Requirement

Global Accelerator is a strong answer when the question says:

- Static IP addresses
- IP allowlisting
- Firewall allowlisting
- Client cannot rely on changing DNS
- Stable global endpoint

### Memory Trick

**Static IP + Global = Global Accelerator**

---

# Global Accelerator Supports TCP and UDP

This is a major distinction from CloudFront.

Use cases include:

- Gaming
- IoT
- MQTT
- Voice over IP
- Other TCP/UDP applications

### Exam Pattern

> **Global UDP application**
>
> → **Global Accelerator**

---

# CloudFront vs Global Accelerator

Both use:

- AWS global network
- Edge Locations
- [[06-Security/Shield]]

But they solve different problems.

## CloudFront

Primarily:

**Content Delivery**

Can cache content.

Best for:

- Images
- Videos
- Websites
- HTTP/S
- APIs
- Static and dynamic web content

---

## Global Accelerator

Primarily:

**Network Acceleration**

Does not rely on content caching.

Best for:

- TCP
- UDP
- Static IPs
- Gaming
- IoT
- VoIP
- Fast regional failover

### Master Difference

**CloudFront = CONTENT**

**Global Accelerator = CONNECTION**

---

# Global Accelerator vs Route 53

## [[Route 53]]

Routes using:

**DNS**

---

## Global Accelerator

Routes using:

**Static Anycast IP addresses**

### Memory Trick

**Route 53 = DNS**

**Global Accelerator = NETWORK**

---

# CloudFront Security Stack

A strong architecture can combine several controls.

User  
↓  
[[Route 53]]  
↓  
CloudFront  
↓  
[[06-Security/WAF]]  
↓  
Signed URL / Signed Cookie  
↓  
Geo Restriction  
↓  
OAC  
↓  
Private S3

Each solves a different problem.

---

## Route 53

**Find the endpoint**

---

## CloudFront

**Deliver content globally**

---

## WAF

**Filter malicious web requests**

---

## Signed URL / Cookie

**Authorize viewer**

---

## Geo Restriction

**Authorize viewer country**

---

## OAC

**Protect private S3 origin**

---

# Architecture Thinking

## Scenario 1 — Global Static Website

Static content is stored in S3.

Global users require low latency.

**Choose:**

[[CloudFront]]  
+  
[[S3]]

---

## Scenario 2 — Private S3 Behind CloudFront

Users must not directly access the S3 bucket.

**Choose:**

CloudFront  
+  
[[CloudFront Origin Access Control]]  
+  
Private S3

---

## Scenario 3 — Stale Cached Website

Developer updates S3.

CloudFront continues showing the old file.

Immediate refresh required.

**Choose → [[CloudFront Cache Invalidations]]**

---

## Scenario 4 — Content Available Only in Canada

**Choose → CloudFront Geo Allowlist**

---

## Scenario 5 — One Paid Video

One subscriber receives temporary access to one protected video.

**Choose → CloudFront Signed URL**

---

## Scenario 6 — Premium Video Library

A subscriber needs access to hundreds of protected files.

**Choose → CloudFront Signed Cookies**

---

## Scenario 7 — Temporary Direct S3 Download

User should temporarily access one S3 object directly.

**Do NOT choose CloudFront Signed URL**

Choose:

[[S3 Pre-Signed URLs]]

---

## Scenario 8 — Global UDP Gaming

Users worldwide need low-latency UDP connections.

**Choose → Global Accelerator**

---

## Scenario 9 — Static IP Requirement

Corporate clients require fixed IP addresses for firewall allowlisting.

**Choose → Global Accelerator**

---

## Scenario 10 — Fast Multi-Region Failover

Application runs in multiple Regions.

Traffic must rapidly move away from an unhealthy Region.

**Choose → Global Accelerator**

---

## Scenario 11 — Permanent S3 Copies in Europe and U.S.

**Do NOT choose CloudFront caching**

Choose:

[[S3 Cross-Region Replication]]

---

# Scenario Recognition

## Immediately Think CloudFront When You See

- CDN
- Global users
- Edge Locations
- Cache
- Reduce latency
- Static content
- Dynamic HTTP content
- S3 content delivery
- Global website

---

## Immediately Think OAC When You See

- Private S3
- CloudFront only
- Prevent direct S3 access
- Bucket Policy authorizes CloudFront

---

## Immediately Think Invalidation When You See

- Stale content
- Origin updated
- Cannot wait for TTL
- Force cache refresh

---

## Immediately Think Geo Restriction When You See

- Country
- Copyright
- Licensing
- Allowlist
- Blocklist

---

## Immediately Think Signed URL When You See

- One protected CloudFront file
- Temporary private CDN access

---

## Immediately Think Signed Cookies When You See

- Multiple protected files
- Entire premium section
- URLs cannot change

---

## Immediately Think Global Accelerator When You See

- Static IP
- Anycast
- TCP
- UDP
- Gaming
- VoIP
- MQTT
- Fast regional failover

---

# Biggest CloudFront Exam Traps

## Trap 1 — CloudFront Stores Original Content

False.

The:

**Origin**

remains the source of truth.

CloudFront stores:

**Cached copies**

---

## Trap 2 — CloudFront Contacts Origin for Every Request

False.

Cache hits can be served from:

**Edge Locations**

---

## Trap 3 — Updating Origin Immediately Refreshes Cache

False.

Wait for:

**TTL**

or use:

**Invalidation**

---

## Trap 4 — CloudFront Cache Is Permanent Replication

False.

Use:

[[S3 Cross-Region Replication]]

for permanent regional object copies.

---

## Trap 5 — OAC Authenticates End Users

False.

OAC protects:

**CloudFront → S3**

Viewer authorization uses:

**Signed URL / Cookie**

---

## Trap 6 — OAC Works with S3 Website Endpoint

False.

S3 Website Endpoint is:

**Custom HTTP Origin**

---

## Trap 7 — Geo Restriction Routes Users

False.

Geo Restriction:

**Allows / Blocks**

Route 53 geographic policies:

**Route**

---

## Trap 8 — Signed URL Protects S3 From Direct Access

Not by itself.

Use:

**OAC**

to protect the origin.

---

## Trap 9 — S3 Pre-Signed URL and CloudFront Signed URL Are Identical

False.

S3 Pre-Signed:

**Direct S3**

CloudFront Signed:

**Through CloudFront**

---

## Trap 10 — Global Accelerator Is a CDN

False.

It provides:

**Network acceleration**

CloudFront provides:

**CDN + caching**

---

## Trap 11 — Global Accelerator Only Supports HTTP

False.

It supports:

**TCP + UDP**

---

## Trap 12 — Global Accelerator IPs Change During Failover

False.

The:

**2 static Anycast IPs remain**

The backend routing changes.

---

# Quick Cheat Sheet

| Exam Clue | Answer |
|---|---|
| Global CDN | CloudFront |
| Cache content | CloudFront |
| Cache hit | Serve from Edge |
| Cache miss | Fetch Origin |
| Cache lifetime | TTL |
| Stale content | Invalidation |
| Refresh everything | `*` |
| Refresh image path | `/images/*` |
| Private S3 | OAC |
| Only CloudFront may access S3 | OAC + Bucket Policy |
| Restrict country | Geo Restriction |
| Only approved countries | Allowlist |
| Ban selected countries | Blocklist |
| One protected file | Signed URL |
| Many protected files | Signed Cookies |
| Direct temporary S3 access | S3 Pre-Signed URL |
| Global TCP / UDP | Global Accelerator |
| Static global IP | Global Accelerator |
| Anycast IP count | 2 |
| Gaming / VoIP | Global Accelerator |
| Fast regional failover | Global Accelerator |
| Permanent regional S3 copies | CRR |
| DNS routing | Route 53 |

---

## Master Memory Trick

> [!tip] CloudFront Master Memory Trick
> Think of CloudFront as a global movie theater chain.
>
> **EDGE LOCATION**
> → Local theater near the customer
>
> **CACHE**
> → Movie already stored at the theater
>
> **TTL**
> → How long the theater keeps that copy
>
> **INVALIDATION**
> → Throw the old copy away now
>
> **OAC**
> → Employee key to the private storage room
>
> **SIGNED URL**
> → Ticket for one movie
>
> **SIGNED COOKIE**
> → Wristband for many movies
>
> **GEO RESTRICTION**
> → Country-based entrance rule
>
> **GLOBAL ACCELERATOR**
> → Express highway to the application

---

## Final Exam Rapid-Fire

> **GLOBAL CONTENT → CloudFront**
>
> **CACHE HIT → Edge**
>
> **CACHE MISS → Origin**
>
> **CACHE LIFETIME → TTL**
>
> **STALE CACHE → Invalidation**
>
> **PRIVATE S3 → OAC**
>
> **ONLY CLOUDFRONT → OAC + Bucket Policy**
>
> **COUNTRY RESTRICTION → Geo Restriction**
>
> **ONE PRIVATE FILE → Signed URL**
>
> **MANY PRIVATE FILES → Signed Cookies**
>
> **DIRECT TEMPORARY S3 → Pre-Signed URL**
>
> **STATIC IP → Global Accelerator**
>
> **TCP / UDP → Global Accelerator**
>
> **GAMING / VOIP → Global Accelerator**
>
> **FAST REGIONAL FAILOVER → Global Accelerator**
>
> **PERMANENT S3 COPY → CRR**
>
> **DNS → Route 53**

---

## Related Notes

- [[CloudFront]]
- [[CloudFront Caching]]
- [[CloudFront Origin Access Control]]
- [[CloudFront Cache Invalidations]]
- [[CloudFront Geo Restriction]]
- [[CloudFront Signed URLs]]
- [[CloudFront Signed Cookies]]
- [[Global Accelerator]]
- [[S3]]
- [[S3 Pre-Signed URLs]]
- [[S3 Cross-Region Replication]]
- [[Application Load Balancer]]
- [[Network Load Balancer]]
- [[EC2]]
- [[Route 53]]
- [[06-Security/WAF]]
- [[06-Security/Shield]]