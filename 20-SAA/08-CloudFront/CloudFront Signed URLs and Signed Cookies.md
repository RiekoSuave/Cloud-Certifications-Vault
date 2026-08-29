## What Problem Does It Solve?

[[CloudFront Signed URLs]] and [[CloudFront Signed Cookies]] restrict access to private content delivered through [[CloudFront]].

They solve the problem of:

> **"How can I use CloudFront to distribute private content only to authorized users?"**

Example:

Private Content  
↓  
CloudFront  
↓  
Authorized User ✅  
Unauthorized User ❌

Common use cases:

- Paid content
- Premium videos
- Private downloads
- Subscription websites
- Content available only to authenticated users

> [!tip] Memory Trick
> **Signed = Prove you're allowed before CloudFront serves the content**

---

## Private Content Architecture

A common secure architecture is:

User  
↓  
Application Authentication  
↓  
Signed URL or Signed Cookie  
↓  
[[CloudFront]]  
↓  
[[CloudFront Origin Access Control]]  
↓  
Private [[S3]]

There are two separate security checks:

**Viewer → CloudFront**

and:

**CloudFront → S3**

These solve different problems.

---

# Viewer Access vs Origin Access

This distinction is extremely important.

## Signed URL / Signed Cookie

Controls:

**Viewer → CloudFront**

Question:

> **Is this user allowed to access the content?**

---

## Origin Access Control

[[CloudFront Origin Access Control]]

controls:

**CloudFront → Private S3**

Question:

> **Is CloudFront allowed to access the origin?**

### Memory Trick

**Signed URL / Cookie = FRONT DOOR**

**OAC = BACK DOOR**

---

# CloudFront Signed URLs

A:

[[CloudFront Signed URLs|Signed URL]]

provides authorized access to:

**A specific CloudFront resource**

The URL contains information proving that the request is authorized.

Conceptually:

User Authenticates  
↓  
Application Determines User Is Authorized  
↓  
Signed URL Generated  
↓  
User Requests CloudFront Resource  
↓  
CloudFront Validates Signature  
↓  
Content Returned

---

# Signed URL Architecture

Example:

User  
↓  
Application  
↓  
Authentication Successful  
↓  
Generate Signed CloudFront URL  
↓  
User Receives URL  
↓  
CloudFront  
↓  
Validate Signature  
↓  
Authorized?  
├── Yes → Serve Content
└── No → Deny Access

The origin can remain:

**Private**

---

# When to Use Signed URLs

Signed URLs are especially useful when access is needed to:

**Individual files**

Example:

Premium User  
↓  
Needs one video  
↓  
Signed URL  
↓  
`/videos/movie.mp4`

Another example:

Customer purchases:

`report.pdf`

Application generates:

**Signed URL for that specific report**

### Memory Trick

**One File → Signed URL**

---

# Signed URL Expiration

Signed URLs can be configured with:

**Expiration**

This means access can be temporary.

Example:

Signed URL  
↓  
Valid for Limited Time  
↓  
Expiration Reached  
↓  
Access Denied

This is useful for:

- Paid downloads
- Temporary video access
- Secure file delivery
- Time-limited content

---

# Signed URL Policy

A signed URL can enforce conditions controlling access.

Conceptually:

Signed URL  
↓  
Policy  
↓  
CloudFront Validates Conditions  
↓  
Allow / Deny

Conditions can be used to restrict access according to the authorization requirements.

### Architecture Thinking

A signed URL is not simply:

**A secret URL**

It is:

**Cryptographically signed authorization**

---

# CloudFront Signed Cookies

[[CloudFront Signed Cookies]] provide restricted access without changing the URL for each protected object.

Architecture:

User Authenticates  
↓  
Application Sends Signed Cookies  
↓  
Browser Stores Cookies  
↓  
User Requests CloudFront Content  
↓  
Cookies Sent Automatically  
↓  
CloudFront Validates Cookies  
↓  
Content Returned

---

# When to Use Signed Cookies

Signed Cookies are especially useful when users need access to:

**Multiple restricted files**

Example:

Premium Course  
├── video1.mp4
├── video2.mp4
├── video3.mp4
├── notes.pdf
└── images/

Instead of creating a separate signed URL for every object:

User  
↓  
Signed Cookies  
↓  
Access Entire Authorized Content Set

> [!tip] Memory Trick
> **Many Files → Signed Cookies**

---

# Signed URL vs Signed Cookies

This is the core exam distinction.

| Requirement | Signed URL | Signed Cookies |
|---|---:|---:|
| One Individual File | ✅ | Possible |
| Multiple Files | Less Convenient | ✅ |
| URL Can Change | ✅ | Not Required |
| Keep Existing URLs | ❌ | ✅ |
| Temporary Access | ✅ | ✅ |
| Private CloudFront Content | ✅ | ✅ |

### Fast Exam Rule

**One File**
→ Signed URL

**Many Files**
→ Signed Cookies

---

# Why Signed Cookies Are Useful

Suppose a subscriber can access:

`/premium/*`

That could include:

- Videos
- Images
- Documents
- JavaScript
- Other assets

Generating individual signed URLs for every resource could become cumbersome.

Instead:

Authenticated Subscriber  
↓  
Signed Cookies  
↓  
Requests `/premium/video1.mp4`  
↓  
Requests `/premium/image1.jpg`  
↓  
Requests `/premium/notes.pdf`

CloudFront checks:

**The Signed Cookies**

---

# Keep URLs Unchanged

Signed Cookies are also useful when:

**You do not want to change existing URLs**

Example:

Existing Website:

`cdn.example.com/videos/movie.mp4`

With signed cookies:

The URL can remain the same.

Authorization information is carried through:

**Cookies**

rather than embedded into the URL.

---

# Trusted Signers

CloudFront must trust the entity responsible for signing access requests.

The signing process uses:

**Public / Private Key Cryptography**

Conceptually:

Application  
↓  
Private Key  
↓  
Signs Authorization

CloudFront  
↓  
Public Key  
↓  
Verifies Signature

### Memory Trick

**Private Key = SIGN**

**Public Key = VERIFY**

---

# Key Groups

CloudFront can use:

**Trusted Key Groups**

for signed URL and signed cookie authorization.

Architecture:

Application  
↓  
Private Key  
↓  
Creates Signature

CloudFront Distribution  
↓  
Trusted Key Group  
↓  
Public Key  
↓  
Validates Signature

If valid:

Content Served

If invalid:

Access Denied

---

# Private S3 + Signed URL Architecture

A very strong SAA architecture is:

User  
↓  
Application Login  
↓  
Signed CloudFront URL  
↓  
CloudFront  
↓  
OAC  
↓  
Private S3

Security responsibilities:

**Application**
→ Determines whether user should receive access

**Signed URL**
→ Authorizes viewer to CloudFront

**OAC**
→ Authorizes CloudFront to S3

**Bucket Policy**
→ Allows CloudFront distribution

**S3 Block Public Access**
→ Prevents public S3 access

---

# Private S3 + Signed Cookies Architecture

For multiple protected files:

User  
↓  
Application Login  
↓  
Signed Cookies  
↓  
CloudFront  
↓  
OAC  
↓  
Private S3

This is excellent for:

- Paid websites
- Premium media libraries
- Subscription platforms
- Protected course content

---

# Signed URLs + CloudFront Caching

Signed URLs do NOT mean CloudFront loses its CDN benefits.

CloudFront can still:

**Cache content at Edge Locations**

Architecture:

Authorized User  
↓  
Signed URL  
↓  
CloudFront Edge  
↓  
Authorization Check  
↓  
Cached Content

This provides:

**Private access + global performance**

---

# Signed Cookies + CloudFront Caching

Same principle:

Authorized User  
↓  
Signed Cookies  
↓  
CloudFront  
↓  
Cached Protected Content

CloudFront still provides:

- Edge delivery
- Lower latency
- Reduced origin load

while restricting viewer access.

---

# CloudFront Signed URL vs S3 Pre-Signed URL

This is one of the most important exam comparisons.

## [[CloudFront Signed URLs]]

Access path:

User  
↓  
CloudFront  
↓  
Origin

Benefits include:

- CloudFront Edge caching
- Global content delivery
- CloudFront security controls
- Private content distribution

---

## [[S3 Pre-Signed URLs]]

Access path:

User  
↓  
S3

The user accesses:

**S3 directly**

The URL is generated using the permissions of the principal creating it.

### Memory Trick

**CloudFront Signed URL**
→ Temporary access through the CDN

**S3 Pre-Signed URL**
→ Temporary direct access to S3

---

# Signed URL vs OAC

Do not confuse these.

## Signed URL

Controls:

**User access to CloudFront**

---

## OAC

Controls:

**CloudFront access to S3**

Architecture:

User  
↓  
Signed URL  
↓  
CloudFront  
↓  
OAC  
↓  
Private S3

### Memory Trick

**Signed URL checks USER**

**OAC checks CLOUDFRONT**

---

# Signed Cookies vs Browser Authentication

Signed Cookies are not the same as:

**Username + Password authentication**

Typically:

Application  
↓  
Authenticates User  
↓  
Determines Authorization  
↓  
Issues Signed Cookies

Then CloudFront uses those cookies to determine whether:

**Protected content may be served**

---

# Geo Restriction + Signed Access

You can combine:

[[CloudFront Geo Restriction]]

with:

Signed URLs / Signed Cookies

Example requirement:

User must:

1. Be a paying subscriber
2. Be located in an approved country

Architecture:

User  
↓  
Signed Authorization  
↓  
Geo Restriction  
↓  
CloudFront  
↓  
Private Origin

### Architecture Lesson

Signed access answers:

**WHO?**

Geo Restriction answers:

**WHERE?**

---

# WAF + Signed Access

[[06-Security/WAF]] can also sit in front of protected CloudFront content.

Architecture:

Internet  
↓  
CloudFront  
↓  
WAF  
↓  
Signed Viewer Authorization  
↓  
OAC  
↓  
Private S3

Different controls solve different problems.

**WAF**
→ Filter malicious HTTP/S requests

**Signed URL / Cookie**
→ Viewer authorization

**OAC**
→ Protect private origin

---

# Architecture Thinking

## Scenario 1 — Paid Video Download

A customer purchases one video.

The video is delivered globally through CloudFront.

Access should expire after a limited period.

**Choose → CloudFront Signed URL**

Why?

One protected resource + temporary access.

---

## Scenario 2 — Premium Video Library

A subscriber should access:

Hundreds of videos

under:

`/premium/videos/`

Generating a signed URL for every video would be inconvenient.

**Choose → CloudFront Signed Cookies**

---

## Scenario 3 — Existing Website URLs Cannot Change

A website already contains hundreds of protected content URLs.

The company wants to add authorization without modifying each URL.

**Choose → Signed Cookies**

---

## Scenario 4 — Temporary Direct S3 Upload

A user needs permission to upload one object directly to S3.

CloudFront distribution is not required.

**Do NOT choose → CloudFront Signed URL**

Choose:

[[S3 Pre-Signed URLs|S3 Pre-Signed URL]]

---

## Scenario 5 — Prevent Users from Bypassing CloudFront

Users are authorized using CloudFront Signed URLs.

However, the underlying S3 objects are publicly accessible.

This architecture is incomplete.

Add:

[[CloudFront Origin Access Control]]

and make S3:

**Private**

---

## Scenario 6 — Premium Content by Country

A streaming service requires:

- Paying subscriber
- Approved country
- Private S3 origin

Architecture:

Subscriber  
↓  
Signed URL / Signed Cookie  
↓  
[[CloudFront Geo Restriction]]  
↓  
CloudFront  
↓  
OAC  
↓  
Private S3

---

# Scenario Recognition

## Immediately Think Signed URL When You See

- One private file
- Individual protected object
- Temporary CloudFront access
- Paid download
- Expiring access
- Private CDN content

---

## Immediately Think Signed Cookies When You See

- Multiple private files
- Entire protected section
- Premium content library
- Do not want to change URLs
- Subscriber access to many objects

---

# Exam Traps

## Trap 1 — CloudFront Signed URL and S3 Pre-Signed URL Are the Same

False.

CloudFront Signed URL:

**User → CloudFront**

S3 Pre-Signed URL:

**User → S3**

---

## Trap 2 — Signed URL Protects the S3 Origin from Direct Access

Not by itself.

Use:

[[CloudFront Origin Access Control]]

to prevent direct S3 access.

---

## Trap 3 — Signed Cookies Are Best for One Download

Usually not.

For one individual object:

**Signed URL**

is generally the cleaner exam answer.

---

## Trap 4 — Signed URLs Disable CloudFront Caching

False.

You can still benefit from:

**Edge caching**

---

## Trap 5 — OAC Authenticates Individual Viewers

False.

OAC handles:

**CloudFront → S3**

Viewer authorization uses:

**Signed URLs / Signed Cookies**

---

## Trap 6 — Signed Cookies Require Changing Every Object URL

False.

One of their major advantages is:

**URLs can remain unchanged**

---

## Trap 7 — Geo Restriction Replaces Signed URLs

False.

Geo Restriction:

**WHERE**

Signed URL / Cookie:

**WHO**

They can work together.

---

# Quick Cheat Sheet

| Requirement | Best Choice |
|---|---|
| One Protected CloudFront File | Signed URL |
| Multiple Protected Files | Signed Cookies |
| Keep Existing URLs | Signed Cookies |
| Temporary CloudFront Access | Signed URL |
| Temporary Direct S3 Access | S3 Pre-Signed URL |
| Protect CloudFront Viewer Access | Signed URL / Cookie |
| Protect Private S3 Origin | OAC |
| Restrict by Country | Geo Restriction |
| Verify CloudFront Signature | Public Key |
| Create Signature | Private Key |
| Global Private Content | CloudFront Signed Access |
| Edge Caching Still Available | ✅ |

---

## Master Memory Trick

> [!tip] Master Memory Trick
> Think of CloudFront as a private movie theater.
>
> **SIGNED URL**
>
> → Ticket for one movie
>
> **SIGNED COOKIE**
>
> → Wristband for the whole movie festival
>
> **OAC**
>
> → Employee-only key to the storage room
>
> **GEO RESTRICTION**
>
> → Country restriction at the entrance

Remember:

**ONE FILE**
→ Signed URL

**MANY FILES**
→ Signed Cookies

**DIRECT S3**
→ S3 Pre-Signed URL

**PRIVATE S3 BEHIND CLOUDFRONT**
→ OAC

And the killer exam distinction:

> **Viewer Authorization = Signed URL / Cookie**
>
> **Origin Authorization = OAC**

---

## Related Notes

- [[CloudFront]]
- [[CloudFront Signed URLs]]
- [[CloudFront Signed Cookies]]
- [[CloudFront Origin Access Control]]
- [[CloudFront Caching]]
- [[CloudFront Geo Restriction]]
- [[CloudFront Cache Invalidations]]
- [[S3]]
- [[S3 Pre-Signed URLs]]
- [[S3 Bucket Policies]]
- [[S3 Block Public Access]]
- [[06-Security/WAF]]