## What Problem Does It Solve?

[[Lambda@Edge]] allows you to run Lambda functions at:

**AWS edge locations**

in response to [[CloudFront]] events.

Instead of always sending a request all the way back to:

**The origin**

you can execute custom logic:

**Closer to the user**

Architecture:

User  
↓  
CloudFront Edge Location  
↓  
Lambda@Edge  
↓  
CloudFront / Origin

> [!tip] Memory Trick
> **Lambda@Edge = Lambda logic at CloudFront's edge**

---

## Core Concept

Normally:

User  
↓  
CloudFront  
↓  
Origin

With Lambda@Edge:

User  
↓  
CloudFront  
↓  
Lambda@Edge Logic  
↓  
Origin / Cached Content

This lets you customize:

**CloudFront requests and responses**

at different points in the request lifecycle.

---

## Lambda@Edge + CloudFront

Lambda@Edge is tightly integrated with:

[[CloudFront]]

You associate a Lambda function version with a:

**CloudFront distribution**

The function can then run when specific:

**CloudFront events**

occur.

### Killer Exam Clue

> **Run custom Lambda logic at edge locations during CloudFront request processing**
>
> → **Lambda@Edge**

---

## Why Run Code at the Edge?

Running logic closer to users can help with:

- Request modification
- Response modification
- Authentication / authorization logic
- URL rewrites
- Redirects
- Header manipulation
- Content personalization
- Bot handling
- A/B testing

The key idea:

**Customize content delivery close to users**

---

# CloudFront Request Flow

A simplified CloudFront flow:

Viewer  
↓  
CloudFront Edge  
↓  
Cache Check  
↓  
Origin  
↓  
CloudFront  
↓  
Viewer

Lambda@Edge can execute at specific points in:

**This request/response lifecycle**

---

# Lambda@Edge Event Types

There are four major CloudFront events:

1. **Viewer Request**
2. **Origin Request**
3. **Origin Response**
4. **Viewer Response**

These are extremely important for:

**SAA scenario questions**

---

# Viewer Request

Runs:

**When CloudFront receives a request from the viewer**

Architecture:

Viewer  
↓  
**Viewer Request Lambda@Edge**  
↓  
CloudFront Cache

This occurs:

**Before CloudFront checks the cache**

### Use Cases

- Authentication
- Authorization
- URL rewrites
- Redirects
- Header modification
- Request validation

### Memory Trick

**Viewer Request = User just arrived**

---

## Viewer Request Example

User requests:

`/`

Lambda@Edge changes it to:

`/en/index.html`

based on:

**Request characteristics**

Then CloudFront continues processing.

---

# Origin Request

Runs:

**Before CloudFront sends a request to the origin**

Architecture:

Viewer  
↓  
CloudFront Cache  
↓  
Cache Miss  
↓  
**Origin Request Lambda@Edge**  
↓  
Origin

Important:

Origin Request typically occurs when CloudFront needs:

**The origin**

such as on a:

**Cache miss**

### Use Cases

- Change origin request headers
- Rewrite origin paths
- Select or modify origin behavior
- Modify request before reaching origin

### Memory Trick

**Origin Request = About to leave CloudFront**

---

# Origin Response

Runs:

**After CloudFront receives a response from the origin**

Architecture:

Origin  
↓  
**Origin Response Lambda@Edge**  
↓  
CloudFront  
↓  
Viewer

### Use Cases

- Modify origin response headers
- Change response behavior
- Process response before CloudFront returns it

### Memory Trick

**Origin Response = Origin just answered**

---

# Viewer Response

Runs:

**Before CloudFront sends the response to the viewer**

Architecture:

CloudFront  
↓  
**Viewer Response Lambda@Edge**  
↓  
Viewer

### Use Cases

- Modify response headers
- Add security headers
- Customize response behavior

### Memory Trick

**Viewer Response = About to go back to user**

---

# Four Event Memory Map

```text
USER
 ↓
VIEWER REQUEST
 ↓
CLOUDFRONT
 ↓
ORIGIN REQUEST
 ↓
ORIGIN
 ↓
ORIGIN RESPONSE
 ↓
CLOUDFRONT
 ↓
VIEWER RESPONSE
 ↓
USER
```

### Master Memory Trick

**Viewer = User Side**

**Origin = Backend Side**

**Request = Going In**

**Response = Coming Back**

---

# Viewer vs Origin Events

## Viewer Events

Run around communication between:

**User ↔ CloudFront**

Think:

**Edge-facing**

---

## Origin Events

Run around communication between:

**CloudFront ↔ Origin**

Think:

**Backend-facing**

---

# Cache Behavior

Caching is important when deciding:

**Which event runs**

### Viewer Request

Runs when:

**Viewer sends the request**

including requests that may ultimately result in:

**Cache hits**

### Origin Request

Runs when CloudFront actually needs to:

**Contact the origin**

Therefore:

**Cache hits can avoid the origin-request path**

### Killer Exam Distinction

> Need logic to run for essentially every incoming viewer request?
>
> → **Viewer Request**
>
> Need logic only when CloudFront is going to the origin?
>
> → **Origin Request**

---

# Authentication at the Edge

One major use case is:

**Authentication / authorization**

Architecture:

User  
↓  
CloudFront  
↓  
Lambda@Edge  
↓  
Validate Request  
↓  
Allow / Deny

This can prevent unauthorized traffic from:

**Reaching the origin**

### Killer Exam Clue

> **Authenticate users at CloudFront before requests reach the backend**
>
> → **Lambda@Edge Viewer Request**

---

# URL Rewriting

Example:

User requests:

`example.com/products`

Lambda@Edge rewrites:

`/products`

to:

`/products/index.html`

without requiring:

**Application changes at the origin**

---

# Redirects

Lambda@Edge can return:

**Redirect responses**

Example:

User requests:

`http://example.com/old`

↓

Lambda@Edge

↓

Redirect:

`https://example.com/new`

This can happen:

**Closer to the viewer**

---

# Geographic Personalization

Request information can be used to customize:

**User experiences**

Example:

User in France  
↓  
CloudFront  
↓  
Lambda@Edge  
↓  
Redirect to French Content

User in Japan  
↓  
CloudFront  
↓  
Lambda@Edge  
↓  
Redirect to Japanese Content

### Exam Pattern

> **Customize CloudFront content based on viewer characteristics**
>
> → **Lambda@Edge**

---

# A/B Testing

Lambda@Edge can support:

**A/B testing**

Example:

Incoming Users  
↓  
Lambda@Edge  
↓  
├── Version A  
└── Version B

This allows content routing without requiring:

**Every request to reach application servers first**

---

# Header Manipulation

Lambda@Edge can:

- Read headers
- Add headers
- Modify headers
- Remove supported headers

Use cases include:

- Security
- Routing
- Authentication
- Device-specific behavior
- Application metadata

---

# Security Headers

Example response headers:

- Content-Security-Policy
- Strict-Transport-Security
- X-Content-Type-Options

Edge logic can modify responses before:

**They reach viewers**

---

# Lambda@Edge Deployment Region

This is a major exam fact.

Lambda@Edge functions are created in:

**US East (N. Virginia) — `us-east-1`**

CloudFront then replicates the function to:

**AWS edge locations**

### Killer Exam Clue

> **Which Region must Lambda@Edge be created in?**
>
> → **us-east-1**

### Memory Trick

**Lambda@Edge starts in Virginia, then travels the world**

---

# Global Replication

You do NOT manually deploy the function to:

**Every edge location**

Instead:

Create Lambda Function  
↓  
Publish Version  
↓  
Associate with CloudFront  
↓  
AWS Replicates to Edge Locations

This provides:

**Global execution**

---

# Published Version Requirement

Lambda@Edge requires:

**A numbered Lambda function version**

You do NOT associate CloudFront with:

`$LATEST`

### Killer Exam Clue

> **Lambda@Edge requires a published version**

---

# Lambda@Edge and Aliases

Lambda@Edge associations use:

**Published function versions**

rather than:

**Lambda aliases**

### Exam Trap

Do NOT choose:

`$LATEST`

or:

An alias

when the question asks what CloudFront associates with Lambda@Edge.

Think:

**Specific published version**

---

# Lambda@Edge Limitations

Lambda@Edge does not support every feature available to:

**Regional Lambda functions**

Important limitations include restrictions around features such as:

- VPC access
- Environment variables
- Layers
- Provisioned Concurrency

### SAA Principle

> **Do not assume every standard Lambda feature works with Lambda@Edge**

---

# Environment Variables

Lambda@Edge does not support:

**Custom environment variables**

in the same way as standard regional Lambda functions.

If an exam question requires extensive runtime configuration:

Consider whether:

**Lambda@Edge is appropriate**

---

# VPC Access

Lambda@Edge functions cannot be configured to access:

**Your VPC directly**

This is important if the application requires:

- Private RDS
- Private EC2
- Internal VPC resources

### Exam Trap

> Need edge code to directly connect to private VPC resources?
>
> Lambda@Edge is generally **not the right fit**

---

# Lambda Layers

Lambda@Edge does not support:

**Lambda Layers**

Therefore dependencies must be handled according to:

**Lambda@Edge packaging requirements**

---

# Provisioned Concurrency

Lambda@Edge does not support:

**Provisioned Concurrency**

Remember:

Lambda@Edge already runs through:

**CloudFront's distributed edge infrastructure**

---

# Lambda@Edge vs Regular Lambda

## Regular Lambda

Runs in:

**AWS Regions**

Can support features such as:

- VPC connectivity
- Layers
- Environment variables
- Provisioned Concurrency
- Broader event integrations

## Lambda@Edge

Runs at:

**CloudFront edge locations**

Primary purpose:

**Customize CloudFront request/response processing**

---

# Lambda@Edge vs CloudFront Functions

This is one of the biggest SAA comparisons.

Both can run code:

**At the edge**

But they target:

**Different workloads**

---

## CloudFront Functions

Designed for:

**Lightweight, extremely fast CloudFront logic**

Common uses:

- Header manipulation
- URL redirects
- URL rewrites
- Cache-key normalization
- Simple request processing

Runs only on:

- Viewer Request
- Viewer Response

### Memory Trick

**CloudFront Functions = LIGHT + FAST**

---

## Lambda@Edge

Designed for:

**More advanced edge processing**

Can work with:

- Viewer Request
- Viewer Response
- Origin Request
- Origin Response

Supports:

**More complex logic**

than CloudFront Functions.

### Memory Trick

**Lambda@Edge = HEAVIER + MORE POWERFUL**

---

# CloudFront Functions vs Lambda@Edge

| Feature | CloudFront Functions | Lambda@Edge |
|---|---:|---:|
| Runs at Edge | ✅ | ✅ |
| Viewer Request | ✅ | ✅ |
| Viewer Response | ✅ | ✅ |
| Origin Request | ❌ | ✅ |
| Origin Response | ❌ | ✅ |
| Lightweight Logic | ✅ Best | Possible |
| More Complex Logic | Limited | ✅ |
| Extremely High Scale / Low Latency | ✅ | Less Lightweight |
| CloudFront Integration | ✅ | ✅ |

---

# When to Choose CloudFront Functions

Think:

**Simple manipulation**

Examples:

- Add/remove headers
- Redirect URL
- Rewrite URI
- Normalize cache key
- Simple authorization logic

### Killer Exam Clue

> **Simple high-scale viewer request/response manipulation**
>
> → **CloudFront Functions**

---

# When to Choose Lambda@Edge

Think:

**More advanced processing**

especially when you need:

- Origin request logic
- Origin response logic
- More complex computation
- Advanced request/response customization

### Killer Exam Clue

> **Need code during CloudFront origin request or origin response**
>
> → **Lambda@Edge**

---

# Edge Computing Architecture

Without edge processing:

User  
↓  
CloudFront  
↓  
Origin  
↓  
Application Logic

With edge processing:

User  
↓  
CloudFront Edge  
↓  
Edge Logic  
↓  
Origin Only If Needed

Potential benefits:

- Lower latency
- Reduced origin workload
- Faster redirects
- Early authentication
- Customized content delivery

---

# Lambda@Edge + S3

Architecture:

User  
↓  
CloudFront  
↓  
Lambda@Edge  
↓  
[[S3]]

Possible uses:

- Rewrite object paths
- Authentication
- Content personalization
- Redirect requests

---

# Lambda@Edge + ALB

Architecture:

User  
↓  
CloudFront  
↓  
Lambda@Edge  
↓  
[[Application Load Balancer]]  
↓  
Application

Edge logic can process requests before:

**They reach the ALB**

---

# Lambda@Edge + API Gateway

Possible architecture:

User  
↓  
CloudFront  
↓  
Lambda@Edge  
↓  
[[API Gateway]]

However, always determine whether the extra edge logic is:

**Actually required**

CloudFront Functions may be sufficient for:

**Simple transformations**

---

# Architecture Thinking

## Scenario 1 — Authenticate Before Origin

Users access private content through CloudFront.

Authentication should occur:

**Before requests reach the origin**

Choose:

**Lambda@Edge Viewer Request**

---

## Scenario 2 — Modify Request Before Origin

Need to change headers only when CloudFront:

**Contacts the origin**

Choose:

**Origin Request**

---

## Scenario 3 — Modify Origin Response

Need to modify response immediately after:

**The origin responds**

Choose:

**Origin Response**

---

## Scenario 4 — Add Response Header

Need to modify a response immediately before:

**CloudFront sends it to the viewer**

Choose:

**Viewer Response**

---

## Scenario 5 — Simple URL Rewrite

Need:

**Extremely lightweight URI rewrite**

on every viewer request.

Choose:

**CloudFront Functions**

---

## Scenario 6 — Origin-Level Logic

Need code that executes:

**Before CloudFront contacts the origin**

Choose:

**Lambda@Edge**

because CloudFront Functions do not support:

**Origin events**

---

## Scenario 7 — Private RDS Connection

Edge function must directly connect to:

**Private RDS inside a VPC**

Lambda@Edge is:

**Not appropriate**

because it does not support:

**VPC access**

---

## Scenario 8 — Deployment Region

Company wants Lambda@Edge.

Where should the Lambda function be created?

**us-east-1**

---

## Scenario 9 — `$LATEST`

Developer tries to associate:

`$LATEST`

with CloudFront.

This is incorrect.

Use:

**Published Lambda Version**

---

# Scenario Recognition

Immediately think:

**Lambda@Edge**

when you see:

- CloudFront + Lambda
- Code at edge locations
- Origin request
- Origin response
- Advanced edge logic
- Authentication at edge
- Content personalization
- Complex CloudFront processing

---

## Think CloudFront Functions When You See

- Lightweight edge logic
- Simple redirects
- Simple URL rewrites
- Header manipulation
- Viewer request
- Viewer response
- Very high-scale simple processing

---

# Exam Traps

## Trap 1 — Lambda@Edge Runs in Your Application Region

❌

Create it in:

**us-east-1**

Then AWS replicates it globally.

---

## Trap 2 — Lambda@Edge Uses `$LATEST`

❌

Use:

**Published Version**

---

## Trap 3 — Lambda@Edge Uses Lambda Aliases for CloudFront Association

❌

CloudFront associates:

**A specific function version**

---

## Trap 4 — Lambda@Edge Supports VPC Access

❌

It does not support:

**VPC connectivity**

---

## Trap 5 — Lambda@Edge Supports Lambda Layers

❌

Layers are:

**Not supported**

---

## Trap 6 — Lambda@Edge Supports Provisioned Concurrency

❌

It does not.

---

## Trap 7 — CloudFront Functions Can Run on Origin Events

❌

CloudFront Functions support:

- Viewer Request
- Viewer Response

Lambda@Edge supports:

- Viewer Request
- Origin Request
- Origin Response
- Viewer Response

---

## Trap 8 — Every CloudFront Customization Needs Lambda@Edge

❌

For lightweight logic:

**CloudFront Functions**

may be simpler, faster, and cheaper.

---

## Quick Cheat Sheet

| Exam Clue | Answer |
|---|---|
| Advanced Code at CloudFront Edge | Lambda@Edge |
| Deployment Region | us-east-1 |
| CloudFront Association | Published Version |
| Before Cache Check | Viewer Request |
| Before Origin | Origin Request |
| After Origin Responds | Origin Response |
| Before Viewer Receives Response | Viewer Response |
| Simple Edge Logic | CloudFront Functions |
| Origin Event Logic | Lambda@Edge |
| Direct VPC Access | ❌ Lambda@Edge |
| Lambda Layers | ❌ Lambda@Edge |
| Provisioned Concurrency | ❌ Lambda@Edge |

---

# Event Decision Table

| Need | Event |
|---|---|
| Process Every Incoming Viewer Request | Viewer Request |
| Authenticate Before Cache Processing | Viewer Request |
| Modify Request Before Origin | Origin Request |
| Process Origin Response | Origin Response |
| Modify Response Before User | Viewer Response |

---

# CloudFront Functions vs Lambda@Edge Decision

Need:

**Simple viewer request/response logic**

→ CloudFront Functions

Need:

**Origin request/response logic**

→ Lambda@Edge

Need:

**More advanced edge processing**

→ Lambda@Edge

Need:

**Simple high-scale URL/header manipulation**

→ CloudFront Functions

---

# Final Exam Rapid-Fire

> **CLOUDFRONT + ADVANCED EDGE CODE**
> → LAMBDA@EDGE
>
> **CREATE REGION**
> → US-EAST-1
>
> **DEPLOYMENT**
> → PUBLISHED VERSION
>
> **USER JUST SENT REQUEST**
> → VIEWER REQUEST
>
> **ABOUT TO CONTACT ORIGIN**
> → ORIGIN REQUEST
>
> **ORIGIN JUST RESPONDED**
> → ORIGIN RESPONSE
>
> **ABOUT TO SEND TO USER**
> → VIEWER RESPONSE
>
> **SIMPLE EDGE LOGIC**
> → CLOUDFRONT FUNCTIONS
>
> **ORIGIN EVENT**
> → LAMBDA@EDGE
>
> **VPC ACCESS**
> → NOT SUPPORTED
>
> **LAYERS**
> → NOT SUPPORTED
>
> **PROVISIONED CONCURRENCY**
> → NOT SUPPORTED

---

## Master Memory Trick

> [!tip] Lambda@Edge Master Memory Trick
> Imagine CloudFront as:
>
> **A hotel between the customer and the kitchen**
>
> The customer walks in:
>
> **VIEWER REQUEST**
>
> The hotel decides it needs the kitchen:
>
> **ORIGIN REQUEST**
>
> The kitchen sends food back:
>
> **ORIGIN RESPONSE**
>
> The hotel hands it to the customer:
>
> **VIEWER RESPONSE**
>
> So remember:
>
> **VIEWER**
> → User Side
>
> **ORIGIN**
> → Backend Side
>
> **REQUEST**
> → Going In
>
> **RESPONSE**
> → Coming Back
>
> And:
>
> **LIGHT + FAST**
> → CloudFront Functions
>
> **ADVANCED + ORIGIN EVENTS**
> → Lambda@Edge
>
> **LAMBDA@EDGE HOME**
> → us-east-1
>
> **DEPLOY**
> → Published Version
>
> And the killer SAA question:
>
> **"Does the edge code need to execute on an origin request or origin response?"**
>
> YES
>
> → **Lambda@Edge**

---

## Related Notes

- [[Lambda]]
- [[CloudFront]]
- [[CloudFront Functions]]
- [[S3]]
- [[Application Load Balancer]]
- [[API Gateway]]
- [[Lambda Concurrency]]