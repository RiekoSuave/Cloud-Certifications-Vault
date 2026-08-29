## What Problem Does It Solve?

[[S3 Static Website Hosting]] lets an S3 bucket serve a website directly over the internet.

It solves the problem of:

> **"How can I host a simple website without running web servers?"**

This works for websites made of static files such as:

- HTML
- CSS
- JavaScript
- Images
- Documents

Think:

User  
↓  
Internet  
↓  
S3 Website Endpoint  
↓  
Static Files

> [!tip] Memory Trick
> **S3 Website = Files, not Servers**
>
> If the site only needs static content:
>
> **Think S3 Static Website Hosting**

---

## What Does "Static" Mean?

Static means S3 returns files exactly as they are stored.

Examples:

- `index.html`
- `error.html`
- `styles.css`
- `app.js`
- `logo.png`

S3 does not run traditional server-side application code.

So S3 website hosting is not designed to directly run:

- PHP
- Java
- .NET
- Python backend code
- Node.js server processes

### Architecture Thinking

If the website is:

**HTML + CSS + JavaScript + Images**

S3 may be enough.

If the application requires:

**Server-side processing**

you need compute such as:

- [[EC2]]
- [[02-Compute/Lambda]]
- [[Elastic Beanstalk]]
- Containers

---

## Website Endpoint

When Static Website Hosting is enabled, S3 provides a:

**Website Endpoint**

The Maarek slides show formats such as:

`http://bucket-name.s3-website-aws-region.amazonaws.com`

or:

`http://bucket-name.s3-website.aws-region.amazonaws.com`

The exact format varies by Region.

### Important

This is different from the normal S3 API endpoint.

> [!tip] Memory Trick
> **Website Hosting → Use Website Endpoint**

---

## Basic Architecture

Example bucket contents:

my-website-bucket

├── index.html  
├── styles.css  
├── app.js  
└── images/

Then:

Browser  
↓  
S3 Website Endpoint  
↓  
index.html  
↓  
Static Website

No EC2 web server is required.

---

## Index Document

You normally configure an:

**Index Document**

Example:

`index.html`

When a user visits the root website URL:

S3 returns:

`index.html`

Conceptually:

Website Root  
↓  
index.html

---

## Error Document

You can also configure an:

**Error Document**

Example:

`error.html`

If a requested page cannot be found:

S3 can return the configured error page.

Example:

User requests:

`/missing-page.html`

↓  

Object not found

↓  

`error.html`

---

## Public Internet Access

The Maarek slides emphasize that S3 static websites can be made accessible on the:

**Internet**

For direct S3 website hosting, the website objects must be readable by the users requesting them.

That usually means configuring the necessary:

[[S3 Bucket Policies]]

and ensuring:

[[S3 Block Public Access]]

is not preventing the required public access.

> [!warning] Exam Trap
> **Website hosting enabled does NOT automatically make the objects publicly readable.**

---

## Website Hosting + Bucket Policy

Architecture:

Internet User  
↓  
S3 Website Endpoint  
↓  
[[S3 Bucket Policies|Bucket Policy]]  
↓  
Allow `s3:GetObject`  
↓  
Website Objects

If the objects are not publicly readable:

Users may receive:

**403 Access Denied**

---

## 403 Forbidden Scenario

This is a classic troubleshooting pattern.

Scenario:

- Static Website Hosting is enabled
- `index.html` exists
- Website endpoint is correct
- Browser receives 403 Forbidden

Likely issue:

**Permissions**

Check:

- Bucket Policy
- Block Public Access
- Object access settings

### Memory Trick

> **Website exists + 403 = Think permissions**

---

## S3 Block Public Access

[[S3 Block Public Access]] can stop the bucket from being publicly accessible.

Therefore:

Static Website Hosting  
+  
Public Bucket Policy  
+  
Block Public Access ON

may still result in:

**Public website inaccessible**

### Architecture Thinking

If the requirement is specifically:

> **Direct public S3 website**

then public access must be intentionally allowed.

---

# S3 Website vs Private S3 + CloudFront

This distinction matters a lot.

There are two common architectures.

---

## Architecture 1 — Direct S3 Website

Users  
↓  
Internet  
↓  
S3 Website Endpoint  
↓  
Public S3 Bucket

Simple and inexpensive.

Useful for:

- Small static sites
- Basic public content
- Simple demonstrations

---

## Architecture 2 — CloudFront + Private S3

Users  
↓  
[[05-Networking/CloudFront]]  
↓  
[[CloudFront Origin Access Control]]  
↓  
Private S3 Bucket

This architecture allows the bucket itself to remain:

**Private**

CloudFront becomes the public-facing entry point.

### Architecture Thinking

For a secure production design:

**CloudFront + Private S3**

is often stronger than:

**Direct Public S3**

---

# Important CloudFront Origin Distinction

CloudFront can use S3 in different ways.

## Normal S3 Bucket Origin

You can keep the bucket private and secure access using:

[[CloudFront Origin Access Control]]

Think:

CloudFront  
↓  
Private S3 Bucket

---

## S3 Website Endpoint as Origin

An S3 Website Endpoint is treated by CloudFront as a:

**Custom HTTP Origin**

The Maarek CloudFront material specifically distinguishes S3 websites as custom origins.

That means the normal private-bucket OAC pattern is not the same architecture when using the website endpoint.

> [!warning] Exam Trap
> **S3 Website Endpoint ≠ Normal private S3 origin**

---

# Route 53 + S3 Website

[[Route 53 Alias Records]] can point DNS names to:

**S3 Website endpoints**

Example:

example.com  
↓  
[[Route 53]] Alias  
↓  
S3 Website

This gives users a friendly domain instead of the long S3 website hostname.

---

## Root Domain Architecture

Example:

User  
↓  
example.com  
↓  
[[Route 53]]  
↓ Alias  
S3 Website Endpoint  
↓  
index.html

This is useful when hosting a static site directly from S3.

---

# Bucket Naming and Custom Domains

When configuring certain direct S3 static-site architectures with a custom domain, bucket naming can become important.

Conceptually:

Domain:

example.com

Bucket:

example.com

Then:

[[Route 53]]  
↓  
Alias  
↓  
S3 Website

For exam purposes, recognize the pattern:

**Route 53 + S3 Website = Static Custom Domain**

---

# Static Website Use Cases

Common use cases include:

- Portfolio site
- Documentation site
- Landing page
- Marketing website
- Public static files
- Frontend for a serverless application

---

# Serverless Website Architecture

S3 can form the frontend of a larger serverless architecture.

Example:

Browser  
↓  
Static HTML / JS from S3  
↓  
[[API Gateway]]  
↓  
[[02-Compute/Lambda]]  
↓  
[[04-Databases/DynamoDB]]

S3 serves:

**Frontend files**

while other AWS services handle:

**Dynamic backend logic**

### Architecture Thinking

S3 itself stays static.

The JavaScript running in the user's browser can call dynamic APIs.

---

# Architecture Thinking

## Scenario 1 — Simple Portfolio Website

A company needs a small public website containing:

- HTML
- CSS
- JavaScript
- Images

No server-side application logic is needed.

**Choose → [[S3 Static Website Hosting]]**

---

## Scenario 2 — PHP Website

A company needs to run PHP scripts directly on the web server.

**Do NOT choose → S3 Static Website Hosting**

S3 does not execute PHP.

Choose compute such as:

[[EC2]]

or another application-hosting service.

---

## Scenario 3 — Website Returns 403

Static Website Hosting is enabled and `index.html` exists.

Users receive:

**403 Access Denied**

Check:

- [[S3 Bucket Policies]]
- [[S3 Block Public Access]]

---

## Scenario 4 — Friendly Domain Name

A company hosts:

example.com

from an S3 static website.

They want users to enter:

example.com

instead of the S3 website hostname.

**Choose → [[Route 53 Alias Records]] pointing to the S3 Website**

---

## Scenario 5 — Private Bucket Behind CDN

A company wants:

- Global caching
- HTTPS-facing distribution
- S3 inaccessible directly
- CloudFront as the only public entry point

**Choose:**

[[05-Networking/CloudFront]]  
+  
Private S3 Bucket  
+  
[[CloudFront Origin Access Control]]

Do not make the S3 bucket publicly accessible unnecessarily.

---

# Static vs Dynamic Website

## Static

Content already exists as files.

Examples:

- HTML
- CSS
- Images
- JavaScript

Think:

[[S3 Static Website Hosting]]

---

## Dynamic

Server generates content based on requests.

Examples:

- Login processing
- Database queries
- Server-side business logic

Think:

Compute backend

Examples:

- [[02-Compute/Lambda]]
- [[EC2]]
- Containers

---

# S3 Website Endpoint vs S3 API Endpoint

Do not confuse them.

## Website Endpoint

Designed for:

**Website hosting**

Provides website-style behavior.

---

## S3 API Endpoint

Designed for:

**S3 API operations**

Example:

- GetObject
- PutObject
- ListBucket

### Memory Trick

**Website Endpoint = Browser website**

**API Endpoint = S3 service API**

---

# Scenario Recognition

## Immediately Think S3 Static Website Hosting When You See

- Static website
- HTML/CSS/JS
- No server required
- Public website files
- S3 website endpoint
- index.html
- error.html
- Portfolio
- Documentation website
- Landing page

### Strongest Exam Phrase

> **"Host a static website with no servers"**
>
> → **S3 Static Website Hosting**

---

# Exam Traps

## Trap 1 — S3 Can Execute Server-Side Code

False.

S3 serves static files.

It does not execute:

- PHP
- Python
- Java
- Node.js servers

---

## Trap 2 — Enabling Website Hosting Automatically Grants Public Access

False.

Permissions still matter.

Check:

- Bucket Policy
- Block Public Access

---

## Trap 3 — Public Bucket Policy Always Works

False.

[[S3 Block Public Access]] may prevent public access.

---

## Trap 4 — S3 Website Endpoint and Normal S3 Origin Are Identical

False.

CloudFront treats the S3 website endpoint as a:

**Custom HTTP origin**

This differs from using a normal S3 bucket origin with OAC.

---

## Trap 5 — S3 Website Is Best for Every Production Website

Not necessarily.

For stronger production architectures, you may want:

[[05-Networking/CloudFront]]

in front of S3.

---

## Trap 6 — Dynamic Backend Means S3 Cannot Be Used At All

False.

S3 can still host the:

**Static frontend**

while:

[[API Gateway]] + [[02-Compute/Lambda]]

handle the dynamic backend.

---

# Quick Cheat Sheet

| Requirement | Best Choice |
|---|---|
| Static HTML/CSS/JS website | S3 Static Website Hosting |
| No web servers | S3 Static Website Hosting |
| Execute PHP/Python server-side | Not S3 |
| Default homepage | Index Document |
| Custom error page | Error Document |
| Friendly domain | Route 53 Alias |
| Direct public S3 site | Public access required |
| Website returns 403 | Check permissions |
| Keep S3 private | CloudFront + OAC |
| Dynamic serverless backend | API Gateway + Lambda |

---

## Master Memory Trick

> [!tip] Master Memory Trick
> **S3 Website = Files on the Web**
>
> Ask:
>
> **"Does this website only need files?"**
>
> If yes:
>
> → **S3 Static Website Hosting**
>
> If it needs server-side execution:
>
> → **Not S3 alone**

Remember:

**HTML/CSS/JS → YES**

**PHP/Python Server → NO**

**403 → Check Permissions**

**Custom Domain → Route 53**

**Private Production Origin → CloudFront + OAC**

And:

> **S3 Website Endpoint = Public HTTP website-style endpoint**
>
> **Normal S3 Origin + OAC = Private CloudFront architecture**

---

## Related Notes

- [[S3]]
- [[S3 Bucket Policies]]
- [[S3 Block Public Access]]
- [[Route 53]]
- [[Route 53 Alias Records]]
- [[05-Networking/CloudFront]]
- [[CloudFront Origin Access Control]]
- [[API Gateway]]
- [[02-Compute/Lambda]]
- [[04-Databases/DynamoDB]]