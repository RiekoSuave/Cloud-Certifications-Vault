## What Problem Does It Solve?

[[S3 Pre-Signed URLs]] provide **temporary access to a specific S3 object or object operation without making the bucket public**.

They solve the problem of:

> **"How can I temporarily let someone download or upload an S3 object without giving them AWS credentials or permanent permissions?"**

Think:

Private S3 Bucket  
↓  
Generate Pre-Signed URL  
↓  
Temporary Access  
↓  
Specific User / Client

> [!tip] Memory Trick
> **Pre-Signed URL = Temporary Key to One S3 Door**

---

## Core Architecture

The S3 bucket can remain:

**Private**

An authorized AWS principal generates:

**Pre-Signed URL**

Then:

User  
↓  
Temporary URL  
↓  
[[S3]]  
↓  
Specific Object

No AWS account or IAM credentials need to be given directly to the end user.

---

## Who Can Generate a Pre-Signed URL?

A Pre-Signed URL can be generated using:

- S3 Console
- AWS CLI
- AWS SDK

The person or application generating the URL must already have the required S3 permission.

Example:

IAM User  
↓  
Has `s3:GetObject`  
↓  
Generates Pre-Signed GET URL  
↓  
External User  
↓  
Downloads Object

---

# Permission Inheritance

This is the most important exam rule.

The user who receives the Pre-Signed URL effectively uses the permissions of:

**The principal that generated the URL**

for that specific signed operation.

If the signer has:

`s3:GetObject`

the URL can provide temporary download access.

If the signer has:

`s3:PutObject`

the URL can provide temporary upload access.

> [!warning] Exam Rule
> **Pre-Signed URL inherits the permissions of the principal that created it**

---

## Permission Boundary

A Pre-Signed URL cannot magically grant permissions the signer does not have.

Example:

IAM User  
↓  
No `s3:GetObject`

tries to generate a usable download URL.

Result:

The URL cannot successfully provide access beyond that principal's permissions.

### Memory Trick

**Signer can't give what signer doesn't have**

---

# Pre-Signed GET URL

A:

**GET Pre-Signed URL**

allows temporary object download.

Architecture:

Private Object  
↓  
Owner Generates GET URL  
↓  
User Receives URL  
↓  
Temporary Download

### Example Use Cases

- Premium video download
- Private report download
- Customer invoice
- Temporary document sharing
- Protected application download

---

## Premium Content Architecture

Example:

User logs into application  
↓  
Application verifies entitlement  
↓  
Backend generates Pre-Signed URL  
↓  
User downloads premium video from S3

This avoids:

Making the entire S3 bucket public.

> [!tip] Exam Pattern
> **Authenticated user + temporary private S3 download**
>
> → **Pre-Signed URL**

---

# Pre-Signed PUT URL

A Pre-Signed URL can also allow:

**Temporary uploads**

using PUT.

Architecture:

Application Backend  
↓  
Generate PUT Pre-Signed URL  
↓  
User Browser / Client  
↓  
Upload Directly to S3

This is extremely useful because the client can upload straight to S3 without sending the file through your application server.

---

## Direct Upload Architecture

Without Pre-Signed URL:

Client  
↓  
Application Server  
↓  
Large File  
↓  
S3

Your server handles all file traffic.

With Pre-Signed URL:

Client  
↓  
Get Temporary URL from Application  
↓  
Client Uploads Directly to S3

This can reduce:

- Application-server bandwidth
- Compute load
- Scaling complexity

---

# Precise Upload Location

The Maarek slides highlight the ability to allow a user to upload:

**To a precise location inside the S3 bucket**

Example:

`s3://uploads/user123/profile.jpg`

The application generates a PUT Pre-Signed URL for that exact key.

User can upload:

profile.jpg

without gaining broad access to:

Other S3 objects.

### Memory Trick

**Pre-Signed PUT = Temporary Upload Slot**

---

# URL Expiration

Pre-Signed URLs are:

**Temporary**

They expire after a configured period.

This is the entire security model:

Valid URL  
↓  
Time Passes  
↓  
Expiration  
↓  
URL No Longer Works

---

## Console Expiration

The Maarek slides show the S3 Console supporting expiration from:

**1 minute**

up to:

**720 minutes**

which equals:

**12 hours**

---

## CLI Expiration

With AWS CLI:

`--expires-in`

sets the expiration period in:

**Seconds**

The Maarek slides show:

Default:

**3600 seconds**

which is:

**1 hour**

Maximum:

**604800 seconds**

which is approximately:

**168 hours / 7 days**

> [!tip] Memory Trick
> **CLI default = 1 hour**
>
> **CLI max = 7 days**

---

# Pre-Signed URL Security

Treat a Pre-Signed URL like a:

**Temporary credential**

Anyone who obtains the URL can potentially use it until it expires.

Therefore:

Do not expose Pre-Signed URLs unnecessarily.

### Architecture Thinking

Pre-Signed URL  
↓  
Possession = Temporary Access

So:

**Protect the URL itself**

---

# Bucket Can Stay Private

This is one of the biggest advantages.

You do NOT need:

- Public Bucket Policy
- Public ACL
- Block Public Access disabled

to share a specific object temporarily.

Architecture:

[[S3 Block Public Access]] ON  
↓  
Private Bucket  
↓  
Pre-Signed URL  
↓  
Temporary Authorized Access

> [!tip] Exam Pattern
> **Keep bucket private + temporary external access**
>
> → **Pre-Signed URL**

---

# Pre-Signed URL vs Public Bucket

## Public Bucket

Potentially allows broad access depending on policy.

Think:

Everyone  
↓  
Bucket / Objects

---

## Pre-Signed URL

Allows:

**Temporary scoped access**

Think:

Specific operation  
+  
Specific object  
+  
Limited time

### Exam Decision

**Permanent public content**

→ Public architecture may make sense

**Temporary private object access**

→ Pre-Signed URL

---

# Pre-Signed URL vs IAM User

Suppose an external customer needs to download:

One report

for:

10 minutes

Creating an IAM user would be:

- Excessive
- Operationally heavy
- Long-lived access

Instead:

Generate:

**Pre-Signed GET URL**

### Memory Trick

**Temporary user → Temporary URL**

Not:

**Permanent IAM identity**

---

# Pre-Signed URL vs CloudFront Signed URL

These are easy to confuse.

## S3 Pre-Signed URL

Provides temporary direct access to:

**S3**

Think:

S3 object access

---

## [[CloudFront Signed URLs]]

Provide controlled access through:

**CloudFront**

Think:

Private CDN content

### Architecture Decision

Direct temporary S3 access  
↓  
Pre-Signed URL

Private globally distributed cached content  
↓  
CloudFront Signed URL

---

# Pre-Signed URLs and Upload Applications

A common serverless architecture is:

User  
↓  
Application  
↓  
Authenticate  
↓  
[[02-Compute/Lambda]] / Backend  
↓  
Generate Pre-Signed PUT URL  
↓  
User Uploads Directly to [[S3]]

This works especially well for:

- Photos
- Videos
- Documents
- User-generated content

---

# Architecture Thinking

## Scenario 1 — Premium Video

A website stores premium videos in a private S3 bucket.

Only authenticated paying users should download them.

The company does not want to make the bucket public.

**Choose → Generate temporary S3 Pre-Signed GET URLs**

---

## Scenario 2 — Temporary Customer Download

A customer needs access to one private report for one hour.

They do not have AWS credentials.

**Choose → Pre-Signed GET URL**

---

## Scenario 3 — User Uploads Large File

Users need to upload large files directly into a private S3 bucket.

The company does not want files to pass through the application server.

**Choose → Pre-Signed PUT URL**

Architecture:

Client  
↓  
Application Generates URL  
↓  
Direct Upload to S3

---

## Scenario 4 — Constantly Changing User List

A company has a changing list of users who need access to private files.

Creating permanent S3 permissions for each user would be operationally expensive.

**Choose → Dynamically generate Pre-Signed URLs**

---

## Scenario 5 — Permanent Public Website Assets

A company hosts images that should be publicly available to everyone indefinitely.

A Pre-Signed URL would be unnecessary overhead.

Use the appropriate:

Public / CloudFront architecture

instead.

---

# Scenario Recognition

## Immediately Think Pre-Signed URL When You See

- Temporary S3 access
- Private object
- User has no AWS credentials
- Temporary download
- Temporary upload
- Premium content
- Time-limited access
- Direct client upload
- Precise S3 key
- Dynamically generated download URL

### Strongest Exam Pattern

> **"Temporarily allow access to a private S3 object"**
>
> → **Pre-Signed URL**

---

# Exam Traps

## Trap 1 — Pre-Signed URL Makes the Bucket Public

False.

The bucket can remain:

**Private**

---

## Trap 2 — User Receiving URL Needs AWS Credentials

False.

Possession of the valid URL provides temporary access for the signed operation.

---

## Trap 3 — Pre-Signed URL Has Unlimited Lifetime

False.

It has:

**Expiration**

---

## Trap 4 — Pre-Signed URL Can Grant More Permission Than Signer Has

False.

The URL inherits the permissions of:

**The principal that generated it**

---

## Trap 5 — Pre-Signed URLs Are Download-Only

False.

They can support operations such as:

- GET
- PUT

The Maarek slides explicitly highlight both temporary downloads and uploads.

---

## Trap 6 — User Must Upload Through Application Server

False.

A PUT Pre-Signed URL can allow:

**Direct upload to S3**

---

## Trap 7 — Public Bucket Required for Pre-Signed URL

False.

Pre-Signed URLs are particularly useful precisely because:

**The bucket can stay private**

---

# Quick Cheat Sheet

| Requirement | Pre-Signed URL |
|---|---|
| Temporary S3 Access | ✅ |
| Private Bucket Can Remain Private | ✅ |
| AWS Credentials Needed by End User | ❌ |
| GET / Download | ✅ |
| PUT / Upload | ✅ |
| Expiration | ✅ |
| Signer Permissions Inherited | ✅ |
| Direct Client Upload | ✅ |
| Precise Object Key | ✅ |
| Permanent Public Access | ❌ |
| Console Max in Maarek Slides | 12 hours |
| CLI Default | 1 hour |
| CLI Max in Maarek Slides | 7 days |

---

## Master Memory Trick

> [!tip] Master Memory Trick
> **Pre-Signed URL = Temporary VIP Pass**
>
> The bucket stays:
>
> **PRIVATE**
>
> The user gets:
>
> **TEMPORARY ACCESS**
>
> to:
>
> **A SPECIFIC ACTION / OBJECT**

Remember:

**GET → Temporary Download**

**PUT → Temporary Upload**

**Signer has permission → URL can use it**

**Signer lacks permission → URL cannot invent it**

And the killer exam phrase:

> **Private S3 + External User + Limited Time**
>
> → **Pre-Signed URL**

---

## Related Notes

- [[S3]]
- [[S3 Bucket Policies]]
- [[S3 Block Public Access]]
- [[IAM]]
- [[05-Networking/CloudFront]]
- [[CloudFront Signed URLs]]
- [[S3 Static Website Hosting]]
- [[02-Compute/Lambda]]