## What Problem Does It Solve?

[[S3 CORS]] allows web browsers to make requests from one origin to another origin.

It solves the problem of:

> **"My website is loaded from one domain, but the browser needs to request files from another domain or S3 bucket."**

Think:

Website Origin  
↓  
Browser  
↓ Cross-Origin Request  
S3 Bucket  
↓  
CORS Rules Decide Whether Browser Can Continue

> [!tip] Memory Trick
> **CORS = Can One Origin Request Something from Another Origin?**

---

## What Is an Origin?

An origin is made of:

**Scheme + Host + Port**

Example:

`https://www.example.com`

Breakdown:

Scheme:

`https`

Host:

`www.example.com`

Port:

`443`

For HTTPS, port 443 is implied.

For HTTP, port 80 is implied.

### Memory Trick

> **Origin = Protocol + Domain + Port**

---

## Same Origin

Two URLs are considered the same origin when they use the same:

- Scheme
- Host
- Port

Example:

`http://example.com/app1`

and:

`http://example.com/app2`

These are:

**Same Origin**

Why?

They both use:

- HTTP
- example.com
- Port 80

The path does not determine the origin.

---

## Different Origins

Example:

`http://www.example.com`

and:

`http://other.example.com`

These are:

**Different Origins**

because the hosts are different.

Another example:

`http://example.com`

and:

`https://example.com`

are also different origins because the:

**Scheme is different**

---

# Browser Security Model

CORS is primarily a:

**Web browser security mechanism**

Suppose a user visits:

`https://www.example.com`

The JavaScript on that page tries to request data from:

`https://assets.example.net`

The browser recognizes:

**Different Origin**

and asks:

> **"Does assets.example.net allow www.example.com to make this request?"**

The destination must return the appropriate:

**CORS Headers**

or the browser blocks access to the response.

---

# CORS Does Not Grant AWS Permissions

This is extremely important.

CORS does NOT replace:

- [[IAM]]
- [[S3 Bucket Policies]]
- [[S3 Block Public Access]]
- Authentication
- Authorization

CORS answers:

> **"Is this browser allowed to make a cross-origin request?"**

IAM and Bucket Policies answer:

> **"Is this principal actually allowed to access the object?"**

### Architecture Thinking

A request may pass CORS but still fail authorization.

Example:

Browser  
↓  
CORS Allowed ✅  
↓  
S3 Authorization  
↓  
Access Denied ❌

> [!warning] Exam Trap
> **CORS ≠ Permission**

---

# S3 CORS

If a browser makes a cross-origin request to an S3 bucket:

You must configure the appropriate:

**CORS Rules**

on the destination S3 bucket.

Example:

Website:

`https://www.example.com`

requests:

`https://my-assets-bucket.s3.amazonaws.com/logo.png`

The S3 bucket must allow the website's origin.

Architecture:

Browser  
↓  
Origin: www.example.com  
↓  
S3 Assets Bucket  
↓  
CORS Rule  
↓  
Allow Origin  
↓  
Response Accessible to Browser

---

# Access-Control-Allow-Origin

One of the most important CORS response headers is:

`Access-Control-Allow-Origin`

This tells the browser:

> **"This origin is allowed to access my response."**

Example:

`Access-Control-Allow-Origin: https://www.example.com`

means:

Requests originating from:

`https://www.example.com`

are allowed.

---

## Allow All Origins

You can also configure:

`*`

meaning:

**All Origins**

Example:

`Access-Control-Allow-Origin: *`

### Architecture Thinking

Use specific origins when possible.

Wildcard access may be appropriate for truly public resources, but it provides broader access.

> [!tip] Exam Rule
> **CORS can allow a specific origin OR `*` for all origins.**

---

# Allowed Methods

CORS rules can specify which HTTP methods are permitted.

Examples:

- GET
- PUT
- DELETE
- POST
- HEAD

Example response:

`Access-Control-Allow-Methods: GET, PUT, DELETE`

This tells the browser which cross-origin operations are acceptable.

---

# Preflight Requests

For some cross-origin requests, the browser performs a:

**Preflight Request**

before sending the real request.

This is typically done using:

**HTTP OPTIONS**

The browser asks:

> **"If I send this request, will you allow it?"**

Architecture:

Browser  
↓  
OPTIONS Preflight  
↓  
S3 / Web Server  
↓  
CORS Response Headers  
↓  
Browser evaluates response  
↓  
Actual request sent

---

## Preflight Example

Website:

`https://www.example.com`

wants to send:

PUT request

to:

`https://www.other.com`

The browser first sends:

OPTIONS  
↓  
www.other.com

The response may include:

`Access-Control-Allow-Origin`

and:

`Access-Control-Allow-Methods`

If allowed:

Browser  
↓  
PUT Request

If not:

Browser blocks the request.

---

# Simple Cross-Origin Architecture

Suppose you have:

### Bucket 1

Hosts:

`index.html`

Website:

`my-bucket-html`

### Bucket 2

Stores:

`images/coffee.jpg`

Website:

`my-bucket-assets`

The browser loads:

index.html  
↓  
Bucket 1

Then the HTML requests:

coffee.jpg  
↓  
Bucket 2

Because the resources come from different origins:

Bucket 2 must allow Bucket 1's origin through:

[[S3 CORS]]

---

## Architecture

Browser  
↓  
GET index.html  
↓  
S3 Bucket A

index.html contains request for image  
↓  
Browser  
↓  
GET coffee.jpg  
↓  
S3 Bucket B  
↓  
CORS Rule checks Origin  
↓  
Allow / Block

---

# CORS Configuration Belongs on the Destination

This is a very common exam trap.

Suppose:

Website A  
↓ requests resource from  
Bucket B

Which side needs the CORS configuration?

**Bucket B**

Why?

Bucket B is the destination receiving the cross-origin request.

> [!tip] Memory Trick
> **CORS goes where the request is GOING**

Not where it started.

---

# Architecture Thinking

## Scenario 1 — Website Loads Images from Another S3 Bucket

A static website hosted in Bucket A loads images from Bucket B.

The browser blocks the image requests because the two buckets use different origins.

**Choose → Configure CORS on Bucket B**

Allow the origin of Bucket A.

---

## Scenario 2 — Public Assets for Any Website

A company stores public assets in S3.

Any website should be allowed to request them.

**Choose → CORS allowing `*`**

assuming the security requirements allow that level of openness.

---

## Scenario 3 — Only One Website Should Access Assets

Assets in S3 should only be used by:

`https://www.example.com`

Configure:

`Access-Control-Allow-Origin: https://www.example.com`

Do not use:

`*`

if the requirement explicitly says only one origin.

---

## Scenario 4 — CORS Is Correct but Access Is Denied

A browser receives correct CORS headers but S3 still returns:

Access Denied

Check:

- [[IAM]]
- [[S3 Bucket Policies]]
- [[S3 Block Public Access]]
- Object permissions

Why?

CORS does not grant S3 authorization.

---

## Scenario 5 — PUT Request Blocked Before It Happens

A browser application needs to send cross-origin PUT requests to S3.

The browser first sends:

**OPTIONS preflight**

The S3 CORS policy must allow the required origin and method.

---

# CORS vs Bucket Policy

These are completely different.

## CORS

Controls:

**Browser cross-origin behavior**

Question:

> Is the browser allowed to use this response?

---

## [[S3 Bucket Policies]]

Controls:

**AWS resource authorization**

Question:

> Is the requester allowed to access the S3 resource?

### Memory Trick

**CORS = Browser**

**Bucket Policy = AWS Permission**

---

# CORS vs Block Public Access

## CORS

Does not make a bucket public.

It only controls cross-origin browser behavior.

## [[S3 Block Public Access]]

Controls:

**Whether S3 resources can become publicly accessible**

### Exam Trap

Configuring:

`Access-Control-Allow-Origin: *`

does NOT automatically make the S3 bucket publicly accessible.

Actual resource permissions still apply.

---

# CORS vs Same-Origin Policy

Browsers normally enforce the:

**Same-Origin Policy**

This restricts JavaScript from freely accessing resources from different origins.

CORS provides a controlled exception.

Think:

Same-Origin Policy  
↓  
Cross-Origin Request Blocked by Default  
↓  
CORS Headers  
↓  
Explicitly Allow Request

---

# Scenario Recognition

## Immediately Think S3 CORS When You See

- Browser
- Different origins
- Cross-origin request
- Website loads files from another S3 bucket
- JavaScript requests another domain
- Access-Control-Allow-Origin
- OPTIONS
- Preflight request
- Allowed methods
- Same-origin policy

### Strongest Exam Pattern

> **"Browser from Domain A needs resources from Domain B"**
>
> → **CORS**

---

# Exam Traps

## Trap 1 — CORS Grants S3 Access

False.

CORS does not replace:

- IAM
- Bucket Policies
- S3 permissions

---

## Trap 2 — CORS Is Configured on the Source Website

Usually false.

Configure CORS on the:

**Destination receiving the cross-origin request**

---

## Trap 3 — Different Paths Mean Different Origins

False.

These:

`http://example.com/app1`

and:

`http://example.com/app2`

are the same origin.

Paths do not matter.

---

## Trap 4 — HTTP and HTTPS Are the Same Origin

False.

Scheme is part of the origin.

Therefore:

`http://example.com`

and:

`https://example.com`

are different origins.

---

## Trap 5 — Different Subdomains Are the Same Origin

False.

These:

`www.example.com`

and:

`other.example.com`

are different hosts and therefore different origins.

---

## Trap 6 — `*` Means Public S3 Permissions

False.

`*` in CORS means:

**Allow requests from all origins**

It does not automatically grant:

`s3:GetObject`

or any other AWS permission.

---

# Quick Cheat Sheet

| Requirement | CORS Concept |
|---|---|
| Browser requests another domain | CORS |
| Origin definition | Scheme + Host + Port |
| Same domain, different path | Same Origin |
| Different subdomain | Different Origin |
| HTTP vs HTTPS | Different Origin |
| Allow one website | Specific Allowed Origin |
| Allow all websites | `*` |
| Cross-origin PUT/DELETE | May trigger Preflight |
| Preflight method | OPTIONS |
| Destination allows request | CORS Headers |
| Grant S3 object access | Not CORS |
| AWS authorization | IAM / Bucket Policy |

---

## Master Memory Trick

> [!tip] Master Memory Trick
> **CORS = Browser asking permission to cross a border**
>
> Website A  
> ↓  
> Browser sees a different origin  
> ↓  
> Browser asks Website/Bucket B:
>
> **"Do you allow Website A?"**
>
> Bucket B responds with:
>
> `Access-Control-Allow-Origin`

Remember:

**Origin = Scheme + Host + Port**

**Different Origin + Browser = Think CORS**

**CORS goes on the destination**

And the biggest exam warning:

> **CORS allows browser interaction**
>
> **It does NOT grant S3 permissions**

---

## Related Notes

- [[S3]]
- [[S3 Static Website Hosting]]
- [[S3 Bucket Policies]]
- [[S3 Block Public Access]]
- [[IAM]]
- [[HTTP]]
- [[HTTPS]]