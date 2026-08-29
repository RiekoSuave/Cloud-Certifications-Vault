## What Problem Does It Solve?

[[CloudFront Origin Access Control]] lets CloudFront securely access a **private S3 bucket** without making that bucket publicly accessible.

It solves the problem of:

> **"How can users retrieve S3 content through CloudFront while preventing them from bypassing CloudFront and accessing S3 directly?"**

Architecture:

User  
↓  
[[CloudFront]]  
↓  
Origin Access Control  
↓  
Private [[S3]] Bucket

The S3 bucket policy allows access from:

**The CloudFront Distribution**

instead of:

**The Public Internet**

> [!tip] Memory Trick
> **OAC = CloudFront's Private Pass into S3**

---

## Why OAC Matters

Without OAC, one possible architecture is:

Internet User  
↓  
[[CloudFront]]  
↓  
Public S3 Bucket

But if the S3 bucket is public:

Users may be able to bypass CloudFront:

User  
↓  
Direct S3 URL  
↓  
S3 Bucket

That defeats some of the advantages of placing CloudFront in front of S3.

With OAC:

User  
↓  
CloudFront  
↓  
OAC  
↓  
Private S3 Bucket

Direct request:

User  
↓  
S3 Bucket  
↓  
Access Denied

### Architecture Goal

> **CloudFront should be public**
>
> **S3 should remain private**

---

# Core Architecture

The Maarek slides show the security pattern as:

Public Internet  
↓  
CloudFront Edge Location  
↓  
[[CloudFront Origin Access Control]]  
+  
[[S3 Bucket Policies]]  
↓  
Private S3 Origin

Think:

CloudFront Distribution  
↓  
Authorized by Bucket Policy  
↓  
S3 Object

The user does NOT need direct S3 permission.

---

# OAC + S3 Bucket Policy

OAC does not work alone.

The S3 bucket must have a:

[[S3 Bucket Policies|Bucket Policy]]

that authorizes the CloudFront distribution to access the objects.

Architecture:

[[CloudFront]]  
↓  
OAC  
↓  
Bucket Policy Checks Request  
↓  
CloudFront Authorized  
↓  
Object Returned

The policy should restrict access so that:

**Only the intended CloudFront distribution**

can retrieve the content.

> [!tip] Memory Trick
> **OAC authenticates CloudFront**
>
> **Bucket Policy authorizes CloudFront**

---

# Private S3 Origin

A major reason to use OAC is to keep:

[[S3 Block Public Access]]

enabled.

Architecture:

S3 Bucket  
↓  
Block Public Access ON  
↓  
Private Bucket

CloudFront  
↓  
OAC  
↓  
Authorized Access

Internet Users  
↓  
Direct S3 Access  
↓  
Denied

### Exam Pattern

If the requirement says:

> **"The S3 bucket must not be publicly accessible."**

and:

> **"Users should receive the content through CloudFront."**

Think:

**CloudFront + OAC + Private S3 Bucket**

---

# CloudFront Becomes the Public Entry Point

With this design:

Users interact with:

**CloudFront**

not directly with:

**S3**

Architecture:

User  
↓  
CloudFront Domain / Custom Domain  
↓  
Edge Cache  
↓  
OAC  
↓  
Private S3 Origin

This gives the architecture access to CloudFront capabilities such as:

- Edge caching
- Global distribution
- [[06-Security/WAF]]
- [[06-Security/Shield]]
- Signed URLs
- Signed Cookies
- Geo Restriction

while keeping S3 private.

---

# Why Prevent Direct S3 Access?

Suppose CloudFront is configured with:

- [[06-Security/WAF]]
- Geo Restrictions
- Signed URLs
- Caching rules

But users can also access:

S3 directly.

Then they may bypass:

- CloudFront security controls
- CloudFront access restrictions
- CloudFront caching
- CloudFront distribution rules

OAC prevents this architecture weakness by making CloudFront the intended path to the origin.

> [!warning] Exam Trap
> **CloudFront security controls do not protect a public S3 URL if users can bypass CloudFront entirely.**

---

# OAC Request Flow

## First Request — Cache Miss

User  
↓  
CloudFront Edge Location  
↓  
Cache Miss  
↓  
CloudFront Sends Authenticated Origin Request  
↓  
OAC  
↓  
Private S3 Bucket  
↓  
Bucket Policy Allows CloudFront  
↓  
Object Returned  
↓  
CloudFront Caches Object  
↓  
User

---

## Later Request — Cache Hit

User  
↓  
CloudFront Edge Location  
↓  
Cache Hit  
↓  
Object Returned

S3 does not need to be contacted again until CloudFront needs to refresh the cached object.

---

# OAC Does Not Make S3 Public

This is an important distinction.

OAC provides:

**Private origin access**

It does NOT require:

- Public ACL
- Public Bucket Policy
- Public S3 website
- Disabling Block Public Access

The stronger architecture is:

Private S3  
+  
CloudFront OAC

---

# OAC and S3 Static Website Endpoints

This is a very important exam distinction.

There are two ways CloudFront may interact with S3.

## Normal S3 Bucket Origin

Example:

S3 REST endpoint

Architecture:

CloudFront  
↓  
OAC  
↓  
Private S3 Bucket

**OAC supported**

---

## S3 Static Website Endpoint

[[S3 Static Website Hosting]]

uses the:

**S3 Website Endpoint**

CloudFront treats this as:

**Custom HTTP Origin**

Architecture:

CloudFront  
↓  
S3 Website Endpoint

This is NOT the same private OAC architecture.

> [!warning] Exam Rule
> **S3 Website Endpoint = Custom Origin**
>
> **Normal S3 Bucket Origin = OAC architecture**

---

# OAC vs Public S3 Website

## OAC Architecture

CloudFront  
↓  
Private S3 Bucket

Best when:

- S3 should not be public
- CloudFront should be the only public entry point
- Security is important

---

## Direct S3 Static Website

Internet  
↓  
S3 Website Endpoint

May require:

**Public access**

depending on the architecture.

### Exam Decision

**Private origin behind CloudFront**
→ OAC

**Direct S3 website endpoint**
→ Public website-style architecture

---

# OAC and Uploads to S3

The Maarek slides also note that CloudFront can be used for:

**Uploading files to S3**

through the CloudFront distribution.

Conceptually:

Client  
↓  
CloudFront  
↓  
OAC  
↓  
S3 Bucket

This can allow CloudFront to serve as the controlled access path for supported S3 operations.

### Architecture Thinking

CloudFront is not limited to:

**GET-only content delivery**

depending on the configured behavior and allowed HTTP methods.

---

# OAC vs Origin Access Identity

You may encounter the older term:

**Origin Access Identity**

or:

**OAI**

OAI was the older CloudFront mechanism for restricting access to private S3 origins.

Modern architectures should recognize:

[[CloudFront Origin Access Control]]

as the newer mechanism.

### Exam Memory

**OAI = Older**

**OAC = Current preferred architecture**

Do not confuse the acronyms.

---

# OAC vs S3 Pre-Signed URLs

These solve different problems.

## OAC

Controls:

**CloudFront → S3**

Question:

> Can CloudFront access my private origin?

---

## [[S3 Pre-Signed URLs]]

Controls:

**Temporary client → S3**

Question:

> Can this user directly access a private S3 object temporarily?

### Memory Trick

**OAC = Service-to-Origin Access**

**Pre-Signed URL = Temporary User Access**

---

# OAC vs CloudFront Signed URLs

Again, different layers.

## OAC

Protects:

**The origin**

Stops direct S3 access.

---

## [[CloudFront Signed URLs]]

Protect:

**Viewer access to CloudFront content**

Architecture:

Authorized User  
↓  
Signed URL  
↓  
CloudFront  
↓  
OAC  
↓  
Private S3

These can work together.

> [!tip] Architecture Pattern
> **Signed URL protects the FRONT door**
>
> **OAC protects the BACK door**

---

# OAC vs CloudFront Signed Cookies

Same idea.

[[CloudFront Signed Cookies]]

control:

**Which viewers can access CloudFront content**

OAC controls:

**Whether CloudFront can access private S3**

Possible architecture:

User  
↓  
Signed Cookie  
↓  
CloudFront  
↓  
OAC  
↓  
Private S3

---

# Defense in Depth Architecture

A secure static-content architecture may look like:

User  
↓  
[[Route 53]]  
↓  
[[CloudFront]]  
↓  
[[06-Security/WAF]]  
↓  
Signed URL / Signed Cookie if needed  
↓  
[[CloudFront Origin Access Control]]  
↓  
Private [[S3]]

with:

[[S3 Block Public Access]]

enabled.

Each layer solves a different problem.

### Route 53

DNS

### CloudFront

Global distribution + caching

### WAF

Web request filtering

### Signed URL / Cookie

Viewer authorization

### OAC

Private origin access

### Block Public Access

Prevent direct public S3 exposure

---

# Architecture Thinking

## Scenario 1 — Private Static Assets

A company stores website images in S3.

Requirements:

- Global users
- CloudFront caching
- S3 must remain private
- Users cannot access S3 directly

**Choose:**

[[CloudFront]]  
+  
[[CloudFront Origin Access Control]]  
+  
[[S3 Bucket Policies]]  
+  
Private S3 Bucket

---

## Scenario 2 — Prevent Bypassing CloudFront

A company uses CloudFront and WAF.

However, users can still retrieve the same files using direct S3 URLs.

How should this be fixed?

**Choose → OAC + Private S3 Bucket**

The bucket policy should only authorize:

**The CloudFront distribution**

---

## Scenario 3 — Public S3 Website Endpoint

CloudFront uses an S3 static website endpoint as its origin.

Should you configure OAC?

**No.**

The website endpoint is treated as:

**Custom HTTP Origin**

---

## Scenario 4 — Viewer Authentication

S3 is private behind CloudFront using OAC.

Only paying customers should access premium videos.

OAC alone does not authenticate individual viewers.

Add:

[[CloudFront Signed URLs]]

or:

[[CloudFront Signed Cookies]]

depending on the requirement.

---

## Scenario 5 — Block Public Access

A company requires:

[[S3 Block Public Access]]

to remain enabled.

Users still need global access to objects.

**Choose:**

CloudFront  
↓  
OAC  
↓  
Private S3

---

# Scenario Recognition

## Immediately Think OAC When You See

- Private S3 origin
- CloudFront only access
- Prevent direct S3 access
- Secure S3 behind CloudFront
- Origin Access Control
- Bucket Policy authorizing CloudFront
- S3 Block Public Access stays enabled
- Users must not bypass CloudFront

### Strongest Exam Pattern

> **"Only CloudFront should access the S3 bucket."**
>
> → **Origin Access Control**

---

# Exam Traps

## Trap 1 — OAC Makes the S3 Bucket Public

False.

OAC is specifically used to help keep the S3 origin:

**Private**

---

## Trap 2 — OAC Replaces the Bucket Policy

False.

You still use:

[[S3 Bucket Policies]]

to authorize the CloudFront distribution.

---

## Trap 3 — Users Receive OAC Credentials

False.

OAC controls:

**CloudFront-to-origin access**

Users simply communicate with CloudFront.

---

## Trap 4 — OAC Is Viewer Authentication

False.

For viewer-level restricted content use:

- [[CloudFront Signed URLs]]
- [[CloudFront Signed Cookies]]

---

## Trap 5 — OAC Works with the S3 Website Endpoint

False.

S3 website endpoints are:

**Custom HTTP Origins**

---

## Trap 6 — S3 Must Disable Block Public Access for OAC

False.

The goal is usually to:

**Keep Block Public Access enabled**

and authorize CloudFront privately.

---

## Trap 7 — CloudFront + Public S3 Prevents Bypass

False.

If S3 is public:

Users may access S3 directly.

Use:

**OAC + Private S3**

---

# Quick Cheat Sheet

| Requirement | OAC |
|---|---|
| CloudFront Access Private S3 | ✅ |
| Keep S3 Private | ✅ |
| Prevent Direct S3 Access | ✅ |
| Works with S3 Bucket Origin | ✅ |
| Uses Bucket Policy | ✅ |
| Keep Block Public Access Enabled | ✅ |
| Viewer Authentication | ❌ |
| Replaces Signed URLs | ❌ |
| Works with S3 Website Endpoint | ❌ |
| Protects Origin | ✅ |
| Edge Caching | Provided by CloudFront |

---

## Master Memory Trick

> [!tip] Master Memory Trick
> **OAC = CloudFront's Backstage Pass**
>
> Public users:
>
> **STOP at CloudFront**
>
> CloudFront:
>
> **Gets the backstage pass**
>
> S3:
>
> **Only lets CloudFront through**

Remember:

**Viewer → CloudFront**

**CloudFront → OAC**

**OAC → Private S3**

And:

> **Signed URL = Who can enter CloudFront**
>
> **OAC = Who can enter S3**

The killer exam phrase:

> **"CloudFront should be the ONLY way to access the private S3 bucket."**
>
> → **OAC**

---

## Related Notes

- [[CloudFront]]
- [[S3]]
- [[S3 Bucket Policies]]
- [[S3 Block Public Access]]
- [[S3 Static Website Hosting]]
- [[S3 Pre-Signed URLs]]
- [[CloudFront Signed URLs]]
- [[CloudFront Signed Cookies]]
- [[CloudFront Caching]]
- [[06-Security/WAF]]
- [[06-Security/Shield]]
- [[Route 53]]