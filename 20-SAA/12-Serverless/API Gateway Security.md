## What Problem Does It Solve?

[[API Gateway Security]] controls:

**Who can call an API, what they can access, and how the API is protected**

Important security mechanisms include:

- IAM Authorization
- Cognito User Pools
- Lambda Authorizers
- Resource Policies
- API Keys
- Usage Plans
- AWS WAF
- Private APIs

> [!tip] Master Memory Trick
> **IAM = AWS identities**
>
> **Cognito = Application users**
>
> **Lambda Authorizer = Custom auth**
>
> **Resource Policy = Who can reach API Gateway**
>
> **WAF = Web attack protection**

---

# IAM Authorization

API Gateway can use:

**AWS IAM**

to authorize requests.

This works well when callers already have:

**AWS credentials**

Examples:

- IAM users
- IAM roles
- AWS services
- Applications using temporary AWS credentials

Architecture:

Caller  
↓  
AWS Credentials  
↓  
API Gateway  
↓  
IAM Authorization  
↓  
Backend

### Killer Exam Clue

> **AWS-authenticated client needs access to an API**
>
> → **IAM Authorization**

---

## Signature Version 4

IAM-authorized API requests are signed using:

**AWS Signature Version 4 — SigV4**

This proves:

- Caller identity
- Request integrity
- AWS credential ownership

### Memory Trick

**IAM API Access = Signed AWS Request**

---

# Cognito User Pools

[[Cognito]] User Pools are designed for:

**Application user authentication**

Examples:

- Web users
- Mobile users
- Customers
- Subscribers

Architecture:

User  
↓  
Cognito User Pool  
↓  
Token  
↓  
API Gateway  
↓  
Backend

### Killer Exam Clue

> **Authenticate web/mobile users before they call API Gateway**
>
> → **Cognito User Pool**

---

## Cognito Token Flow

User Signs In  
↓  
Cognito  
↓  
JWT Token  
↓  
Client Sends Token  
↓  
API Gateway Validates Token  
↓  
Backend

This allows API Gateway to authorize:

**Authenticated application users**

without writing all authentication logic yourself.

---

# IAM vs Cognito

### IAM

Think:

**AWS identities**

### Cognito

Think:

**Application users**

### Memory Trick

**AWS Employee / Service**
→ IAM

**Customer / Mobile User**
→ Cognito

---

# Lambda Authorizers

A:

**Lambda Authorizer**

uses custom Lambda code to:

**Authorize API requests**

Architecture:

Client  
↓  
API Gateway  
↓  
Lambda Authorizer  
↓  
Allow / Deny  
↓  
Backend

Use when authorization depends on:

- Custom tokens
- Legacy authentication
- External identity providers
- Custom business rules

### Killer Exam Clue

> **Need custom authorization logic for API Gateway**
>
> → **Lambda Authorizer**

---

## Lambda Authorizer Flow

Client Sends Credential  
↓  
API Gateway  
↓  
Lambda Authorizer  
↓  
Validate Credential  
↓  
Return IAM Policy / Authorization Result  
↓  
Allow or Deny Request

---

# Cognito vs Lambda Authorizer

| Requirement | Cognito | Lambda Authorizer |
|---|---:|---:|
| User Sign-Up / Sign-In | ✅ | ❌ |
| Managed User Directory | ✅ | ❌ |
| JWT-Based User Auth | ✅ | ✅ Possible |
| Custom Token Logic | Limited | ✅ |
| Legacy Auth Integration | ❌ | ✅ |
| Custom Authorization Code | ❌ | ✅ |

### Memory Trick

**Cognito = Managed Users**

**Authorizer = Custom Logic**

---

# Resource Policies

API Gateway supports:

**Resource Policies**

These control:

**Who can access the API itself**

They can restrict access based on:

- AWS account
- IAM principal
- Source IP
- VPC endpoint
- Other supported conditions

### Killer Exam Clue

> **Restrict which AWS accounts or network sources can access the API**
>
> → **API Gateway Resource Policy**

---

# Resource Policy vs IAM Authorization

These solve related but different problems.

### IAM Authorization

Answers:

> **Is this caller identity allowed to invoke this API method?**

### Resource Policy

Answers:

> **Which principals or network sources may access this API at all?**

They can be used:

**Together**

---

# Cross-Account Access

Suppose:

Account A  
↓  
API Gateway in Account B

Cross-account access may require:

- Caller IAM permissions
- API Gateway resource policy

### Exam Principle

> **Cross-account authorization often requires permission on both sides**

---

# Source IP Restrictions

Resource policies can restrict:

**Specific source IP ranges**

Example:

Only corporate network:

`203.0.113.0/24`

may access the API.

### Killer Exam Clue

> **Only requests from corporate public IP addresses should reach API Gateway**
>
> → **Resource Policy with IP restriction**

---

# Private API Security

A:

**Private API**

is accessible through:

**VPC Interface Endpoints**

Architecture:

Private Client  
↓  
Interface VPC Endpoint  
↓  
Private API Gateway

This keeps the API:

**Off the public Internet**

### Killer Exam Clue

> **API should only be reachable from inside selected VPCs**
>
> → **Private API Gateway**

---

# VPC Endpoint Policies

A VPC endpoint can have:

**An endpoint policy**

controlling:

**Which API Gateway APIs or actions can be accessed through the endpoint**

This provides another:

**Authorization layer**

---

# Private API Resource Policies

Private APIs commonly use:

**Resource policies**

to restrict access to:

- Specific VPCs
- Specific VPC endpoints
- Specific AWS accounts

### Memory Trick

**Private API + Resource Policy = Internal API Boundary**

---

# API Keys

API Gateway REST APIs can use:

**API Keys**

to identify:

**API consumers**

API keys are useful for:

- Usage tracking
- Usage plans
- Quotas
- Rate management

### Important Exam Trap

API keys are NOT:

**Strong authentication credentials**

### Memory Trick

**API Key = Metering ID**

not:

**User identity**

---

# Usage Plans

A:

**Usage Plan**

can define:

- Throttling
- Quotas

for clients associated with:

**API Keys**

Example:

Bronze Plan  
→ 1,000 requests/day

Gold Plan  
→ 100,000 requests/day

---

# API Keys vs Authentication

Do NOT use API keys alone to protect:

**Sensitive application access**

Use:

- IAM
- Cognito
- Lambda Authorizers

for actual:

**Authorization / authentication**

### Killer Exam Distinction

**Who are you?**
→ Auth mechanism

**How much can you use?**
→ API Key + Usage Plan

---

# AWS WAF

[[06-Security/WAF]] can protect API Gateway from:

**Common web attacks**

Examples:

- SQL injection
- Cross-site scripting
- Malicious IP addresses
- Suspicious request patterns
- Bot traffic

Architecture:

Internet  
↓  
WAF  
↓  
API Gateway  
↓  
Backend

### Killer Exam Clue

> **Protect public API Gateway API from common web exploits**
>
> → **AWS WAF**

---

# WAF Web ACL

A:

**Web ACL**

contains:

**WAF rules**

that determine whether traffic should be:

- Allowed
- Blocked
- Counted
- Challenged according to supported rule behavior

---

# WAF Managed Rules

AWS WAF supports:

**Managed Rule Groups**

These can help protect against:

- Common vulnerabilities
- Known malicious patterns
- OWASP-style attacks

This reduces:

**Manual rule creation**

---

# Rate-Based WAF Rules

WAF can also detect:

**High request rates from individual sources**

and apply protections.

### Exam Distinction

API Gateway throttling:

**Controls API request rates overall/per configured limits**

WAF rate-based rules:

**Detect abusive source request patterns**

---

# WAF vs API Gateway Throttling

| Requirement | WAF | API Gateway Throttling |
|---|---:|---:|
| SQL Injection Protection | ✅ | ❌ |
| XSS Protection | ✅ | ❌ |
| Malicious IP Blocking | ✅ | ❌ |
| Backend Request Rate Control | Limited Security Use | ✅ |
| Client Quotas | ❌ | Usage Plans |
| Web Attack Filtering | ✅ | ❌ |

### Memory Trick

**WAF = SECURITY FILTER**

**THROTTLING = TRAFFIC CONTROL**

---

# TLS / HTTPS

API Gateway exposes APIs using:

**HTTPS**

This provides:

**Encryption in transit**

between clients and API Gateway.

For custom domains:

You can use certificates from:

**AWS Certificate Manager**

---

# Custom Domain Names

Instead of using:

`execute-api...amazonaws.com`

you can configure:

**Custom Domain Names**

such as:

`api.example.com`

Architecture:

Client  
↓  
`api.example.com`  
↓  
API Gateway

---

# ACM Certificates

[[AWS Certificate Manager]] provides:

**TLS certificates**

for custom API domains.

### Killer Exam Clue

> **Secure custom API Gateway domain with HTTPS**
>
> → **ACM Certificate**

---

# Mutual TLS

API Gateway can support:

**Mutual TLS — mTLS**

for supported custom-domain configurations.

With normal TLS:

Server proves identity to client.

With mTLS:

**Client and server authenticate each other**

### Killer Exam Clue

> **Clients must present certificates before accessing the API**
>
> → **Mutual TLS**

---

# Authorization Layers

A secure API can have multiple layers:

Internet  
↓  
WAF  
↓  
API Gateway  
↓  
Authentication / Authorization  
↓  
Backend

Possible controls:

- WAF
- Resource Policy
- IAM
- Cognito
- Lambda Authorizer
- Usage Plans

### SAA Principle

> **Security mechanisms can be layered rather than mutually exclusive**

---

# Backend Permissions

Securing API Gateway does not automatically grant the backend:

**AWS permissions**

Example:

Client  
↓  
API Gateway  
↓  
Lambda  
↓  
DynamoDB

Separate security questions exist:

### Client → API Gateway

Controlled by:

- IAM
- Cognito
- Authorizer
- Resource policy

### Lambda → DynamoDB

Controlled by:

**Lambda Execution Role**

---

# API Gateway Invoking Lambda

API Gateway needs permission to:

**Invoke Lambda**

This is generally represented through:

**Lambda resource-based invocation permission**

Architecture:

API Gateway  
↓  
Lambda Resource Policy  
↓  
Lambda

### Memory Trick

**API Gateway → Lambda**
→ Lambda resource permission

---

# Lambda Accessing AWS Services

After invocation:

Lambda  
↓  
Execution Role  
↓  
AWS Service

This is completely separate from:

**API Gateway authorization**

---

# Authentication vs Authorization

### Authentication

Answers:

> **Who are you?**

Examples:

- Cognito login
- IAM identity
- Token validation

### Authorization

Answers:

> **What are you allowed to do?**

Examples:

- IAM policies
- Authorizer decision
- Resource policies

### Memory Trick

**AUTHN = WHO**

**AUTHZ = WHAT**

---

# CORS

**CORS**

controls whether browsers allow:

**Cross-origin web requests**

Example:

Frontend:

`https://app.example.com`

API:

`https://api.example.com`

CORS determines whether the browser may:

**Send/read the cross-origin request**

### Important Trap

CORS is NOT:

- Authentication
- Authorization
- WAF
- Encryption

---

# CORS Preflight

Browsers may send an:

**OPTIONS preflight request**

before the actual API request.

API Gateway must return:

**Appropriate CORS headers**

for the browser to allow:

**The real request**

---

# CloudWatch Logging

API Gateway integrates with:

[[07-Monitoring/CloudWatch]]

for:

- Access logging
- Execution logging
- Metrics
- Alarms

Security teams can monitor:

- Unauthorized requests
- Error rates
- Suspicious usage
- High traffic patterns

---

# CloudTrail

[[06-Security/CloudTrail]] records:

**API-level AWS management activity**

related to API Gateway configuration.

Use CloudTrail when asking:

> **Who changed the API Gateway configuration?**

Use CloudWatch when asking:

> **How is the API behaving?**

### Memory Trick

**CloudTrail = Who changed AWS?**

**CloudWatch = How is it running?**

---

# Architecture Thinking

## Scenario 1 — Mobile Users

Mobile users need:

- Sign-up
- Sign-in
- JWT tokens
- API access

Choose:

[[Cognito]]  
↓  
API Gateway

---

## Scenario 2 — AWS Service Caller

An AWS workload using IAM role credentials needs to call:

API Gateway.

Choose:

**IAM Authorization**

---

## Scenario 3 — Legacy Authentication

Company has a custom token system.

Need API Gateway to call code that validates tokens.

Choose:

**Lambda Authorizer**

---

## Scenario 4 — Corporate IP Only

API is public but should only accept:

**Corporate public IP ranges**

Choose:

**API Gateway Resource Policy**

with:

**Source IP restrictions**

---

## Scenario 5 — VPC-Only API

API must never be publicly reachable.

Choose:

**Private API + Interface VPC Endpoint**

---

## Scenario 6 — Specific VPC Endpoint Only

Private API should only allow access through:

`vpce-123`

Choose:

**Resource Policy restricting the VPC endpoint**

---

## Scenario 7 — Paid API Plans

Customers have:

Different request quotas.

Choose:

**API Keys + Usage Plans**

Do NOT treat API key as:

**Primary user authentication**

---

## Scenario 8 — SQL Injection

Public API is receiving:

**SQL injection attempts**

Choose:

[[06-Security/WAF]]

---

## Scenario 9 — Too Many Legitimate Requests

Backend must be protected from:

**Excessive request rate**

Choose:

**API Gateway Throttling**

---

## Scenario 10 — Client Certificates

Business partners must authenticate with:

**Client TLS certificates**

Choose:

**Mutual TLS**

---

## Scenario 11 — Browser Block

Authenticated request works in curl but:

**Browser blocks cross-origin request**

Think:

**CORS**

not:

IAM.

---

## Scenario 12 — Lambda Cannot Access DynamoDB

User successfully authenticates through Cognito.

API Gateway invokes Lambda.

Lambda gets:

`AccessDenied`

from DynamoDB.

Problem is NOT Cognito.

Check:

**Lambda Execution Role**

---

# Scenario Recognition

Immediately think:

**IAM Authorization**

when you see:

- AWS credentials
- IAM users/roles
- SigV4
- AWS-to-AWS API calls

---

## Think Cognito When You See

- Mobile users
- Web users
- Sign-up
- Sign-in
- User pools
- JWT authentication

---

## Think Lambda Authorizer When You See

- Custom token
- Custom authorization
- Legacy identity system
- Custom validation logic

---

## Think Resource Policy When You See

- Specific AWS accounts
- Source IP restriction
- VPC restriction
- VPC endpoint restriction
- Cross-account API access

---

## Think WAF When You See

- SQL injection
- XSS
- IP blocking
- Web exploit protection
- Malicious request filtering

---

# Exam Traps

## Trap 1 — API Key Authenticates Users

❌

API keys are primarily used for:

**Usage identification and plans**

---

## Trap 2 — Cognito and Lambda Authorizer Are the Same

❌

Cognito:

**Managed user authentication**

Lambda Authorizer:

**Custom authorization logic**

---

## Trap 3 — Resource Policy Replaces IAM Authorization in Every Case

❌

They can be:

**Used together**

---

## Trap 4 — CORS Secures API Gateway

❌

CORS is:

**Browser behavior**

---

## Trap 5 — WAF Controls Application User Identity

❌

WAF filters:

**Web requests**

It does not authenticate:

**Users**

---

## Trap 6 — API Gateway Throttling Stops SQL Injection

❌

Use:

**WAF**

---

## Trap 7 — Private API Means Private Backend

❌

Private API controls:

**API access**

For API Gateway to reach a private backend:

Think:

**VPC Link**

---

## Trap 8 — Cognito Permission Lets Lambda Access DynamoDB

❌

Lambda needs:

**Its own Execution Role**

---

## Trap 9 — HTTPS Replaces Authorization

❌

HTTPS provides:

**Encryption in transit**

not:

**Access control**

---

## Quick Cheat Sheet

| Exam Clue | Answer |
|---|---|
| AWS Identity Calling API | IAM Authorization |
| Mobile/Web User Login | Cognito User Pool |
| Custom Token Logic | Lambda Authorizer |
| Restrict AWS Accounts | Resource Policy |
| Restrict Source IP | Resource Policy |
| VPC-Only API | Private API |
| Restrict VPC Endpoint | Resource Policy |
| Customer Usage Quota | Usage Plan |
| Usage Tracking ID | API Key |
| SQL Injection / XSS | WAF |
| Limit Request Rate | API Gateway Throttling |
| Client Certificate Authentication | mTLS |
| HTTPS Custom Domain | ACM |
| Browser Cross-Origin | CORS |
| Lambda → DynamoDB Permission | Lambda Execution Role |

---

# Authentication Decision Tree

Who is calling?

AWS identity?

→ **IAM Authorization**

Application user?

→ **Cognito**

Custom token / legacy authentication?

→ **Lambda Authorizer**

Need network/account restriction?

→ **Resource Policy**

---

# Security Layer Decision

Need:

**User identity**
→ Cognito / IAM / Authorizer

Need:

**Network or account restriction**
→ Resource Policy

Need:

**Attack filtering**
→ WAF

Need:

**Usage quota**
→ API Key + Usage Plan

Need:

**Encryption in transit**
→ HTTPS / TLS

Need:

**Client certificates**
→ mTLS

---

# Final Exam Rapid-Fire

> **AWS CREDENTIALS**
> → IAM AUTHORIZATION
>
> **WEB/MOBILE USERS**
> → COGNITO
>
> **CUSTOM TOKEN**
> → LAMBDA AUTHORIZER
>
> **WHO CAN REACH API**
> → RESOURCE POLICY
>
> **CORPORATE IP ONLY**
> → RESOURCE POLICY
>
> **VPC ONLY**
> → PRIVATE API
>
> **CUSTOMER QUOTA**
> → USAGE PLAN
>
> **METER CLIENT USAGE**
> → API KEY
>
> **SQL INJECTION / XSS**
> → WAF
>
> **LIMIT REQUEST RATE**
> → API GATEWAY THROTTLING
>
> **CLIENT CERTIFICATES**
> → MUTUAL TLS
>
> **CUSTOM HTTPS DOMAIN**
> → ACM
>
> **BROWSER CROSS-ORIGIN**
> → CORS
>
> **LAMBDA AWS PERMISSIONS**
> → EXECUTION ROLE

---

## Master Memory Trick

> [!tip] API Gateway Security Master Memory Trick
> Imagine API Gateway as a secured office building.
>
> **IAM**
> → Employee badge
>
> **Cognito**
> → Customer login system
>
> **Lambda Authorizer**
> → Custom security guard
>
> **Resource Policy**
> → Rules saying which buildings, networks, or people may approach
>
> **API Key**
> → Membership number used to measure usage
>
> **Usage Plan**
> → Membership limits
>
> **WAF**
> → Security screening at the entrance
>
> **TLS**
> → Encrypted conversation
>
> **mTLS**
> → Both sides show identification

So remember:

> **IAM**
> → AWS IDENTITIES
>
> **COGNITO**
> → USERS
>
> **AUTHORIZER**
> → CUSTOM AUTH
>
> **RESOURCE POLICY**
> → ACCESS BOUNDARY
>
> **API KEY**
> → METER
>
> **WAF**
> → FILTER ATTACKS
>
> **THROTTLING**
> → CONTROL RATE
>
> **CORS**
> → BROWSER RULE

And the killer SAA question:

> **"Is the requirement about identity, network access, usage limits, or attack protection?"**
>
> Identity  
> → IAM / Cognito / Authorizer
>
> Network or account access  
> → Resource Policy
>
> Usage limits  
> → API Keys + Usage Plans
>
> Web attacks  
> → WAF

---

## Related Notes

- [[API Gateway]]
- [[Lambda]]
- [[Lambda Execution Roles]]
- [[Cognito]]
- [[IAM]]
- [[06-Security/WAF]]
- [[07-Monitoring/CloudWatch]]
- [[06-Security/CloudTrail]]
- [[AWS Certificate Manager]]
- [[05-Networking/VPC Endpoints]]