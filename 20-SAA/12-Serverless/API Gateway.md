## What Problem Does It Solve?

[[API Gateway]] is AWS's:

**Fully managed service for creating, publishing, securing, monitoring, and scaling APIs**

It is commonly used as the:

**Front door**

for applications that expose:

- REST APIs
- HTTP APIs
- WebSocket APIs

Architecture:

Client  
↓  
API Gateway  
↓  
Backend

Possible backends:

- [[Lambda]]
- HTTP endpoints
- AWS services

> [!tip] Memory Trick
> **API Gateway = Front Door for APIs**

---

## Core Concept

Without API Gateway:

Client  
↓  
Application Server  
↓  
Backend Logic

With API Gateway:

Client  
↓  
API Gateway  
↓  
Backend Service

API Gateway handles many API concerns such as:

- Routing
- Authentication
- Authorization
- Throttling
- Monitoring
- Request/response transformation
- API lifecycle management

---

# API Gateway + Lambda

The classic serverless architecture:

Client  
↓  
API Gateway  
↓  
[[Lambda]]  
↓  
DynamoDB

This provides:

- Managed API endpoint
- Serverless compute
- Serverless database
- Automatic scaling

### Killer Exam Clue

> **Build a serverless REST API**
>
> → **API Gateway + Lambda**

---

# API Gateway + DynamoDB

A common serverless backend:

Client  
↓  
API Gateway  
↓  
Lambda  
↓  
[[DynamoDB]]

Think:

**API Gateway = Front Door**

**Lambda = Logic**

**DynamoDB = Data**

---

# API Types

API Gateway supports several API models.

Important ones for SAA:

1. REST APIs
2. HTTP APIs
3. WebSocket APIs

---

# REST API

REST APIs provide:

**Feature-rich API management**

Think:

- RESTful endpoints
- API keys
- Usage plans
- Request validation
- Request/response transformation
- Caching
- Advanced API features

### Killer Exam Clue

> **Need advanced API Gateway features and full REST API management**
>
> → **REST API**

---

# HTTP API

HTTP APIs are designed for:

**Lower-cost, lower-latency HTTP API use cases**

They are simpler than:

**REST APIs**

and work well for common serverless API architectures.

Architecture:

Client  
↓  
HTTP API  
↓  
Lambda / HTTP Backend

### Exam Shortcut

**Simple HTTP API**
→ HTTP API

**Advanced API management**
→ REST API

---

# REST API vs HTTP API

| Requirement | REST API | HTTP API |
|---|---:|---:|
| RESTful HTTP Endpoints | ✅ | ✅ |
| Lower Cost | ❌ | ✅ |
| Lower Latency | Usually Higher | ✅ |
| API Caching | ✅ | More Limited |
| Usage Plans / API Keys | ✅ | More Limited |
| Advanced Transformations | ✅ | Simpler |
| Simple Lambda API | ✅ | ✅ Best Fit Often |

### Memory Trick

**REST API = MORE FEATURES**

**HTTP API = SIMPLE + FAST + CHEAPER**

---

# WebSocket API

WebSocket APIs support:

**Persistent two-way communication**

between:

**Clients and backend applications**

Architecture:

Client  
↕  
API Gateway WebSocket  
↕  
Backend

Use cases:

- Chat
- Live dashboards
- Notifications
- Multiplayer applications
- Real-time updates

### Killer Exam Clue

> **Clients need persistent bidirectional communication**
>
> → **API Gateway WebSocket API**

---

# WebSocket Connections

Unlike normal request/response APIs:

A WebSocket connection can remain:

**Open**

This allows:

Server  
→ Client

and:

Client  
→ Server

without creating:

**A brand-new HTTP connection for every message**

---

# Routes

API Gateway routes requests based on:

**Defined paths and methods**

Example:

`GET /users`

`POST /orders`

`DELETE /products/{id}`

Each route can map to:

**A backend integration**

---

# API Gateway Integration

API Gateway can integrate with:

- Lambda
- HTTP services
- Other AWS services

Think:

Request  
↓  
API Gateway  
↓  
Integration  
↓  
Backend

---

# Lambda Proxy Integration

One of the most common integrations:

Client  
↓  
API Gateway  
↓  
Lambda Proxy Integration  
↓  
Lambda

API Gateway sends request information to Lambda.

Lambda returns:

**The HTTP-style response**

### SAA Concept

> **Lambda proxy integration simplifies API Gateway + Lambda communication**

---

# AWS Service Integration

API Gateway can integrate directly with:

**Some AWS services**

without always requiring:

**Lambda**

Conceptually:

Client  
↓  
API Gateway  
↓  
AWS Service

This can reduce:

**Unnecessary compute layers**

when simple service integration is enough.

---

# API Gateway Stages

An API can have:

**Stages**

such as:

- dev
- test
- prod

Architecture:

API  
↓  
├── dev
├── test
└── prod

Each stage can represent:

**A deployed version/configuration of the API**

### Memory Trick

**Stage = Environment**

---

# Stage Variables

Stage variables can provide:

**Stage-specific configuration**

Example:

`dev`

→ Lambda Dev Alias

`prod`

→ Lambda Prod Alias

This can help route different stages toward:

**Different backend environments**

---

# API Gateway + Lambda Aliases

Architecture:

API Gateway Dev Stage  
↓  
Lambda Alias `dev`

API Gateway Prod Stage  
↓  
Lambda Alias `prod`

This supports:

**Environment separation**

and controlled deployments.

---

# Canary Deployments

API Gateway can support:

**Canary deployments**

where a percentage of traffic is sent to:

**A new deployment**

Example:

90%  
→ Current Version

10%  
→ New Version

This supports:

**Gradual rollout**

### Killer Exam Clue

> **Gradually test a new API deployment with a small percentage of production traffic**
>
> → **Canary Deployment**

---

# API Gateway Throttling

API Gateway can control:

**Request rates**

This helps protect:

- Lambda
- Databases
- Backend applications
- Third-party services

Architecture:

Client Traffic  
↓  
API Gateway Throttling  
↓  
Backend

### Killer Exam Clue

> **Protect backend from too many API requests**
>
> → **API Gateway Throttling**

---

# Throttling vs Lambda Reserved Concurrency

These operate at:

**Different layers**

### API Gateway Throttling

Limits:

**Incoming request rate**

### Lambda Reserved Concurrency

Limits:

**Simultaneous Lambda executions**

### Memory Trick

**API Gateway = Limit BEFORE Lambda**

**Reserved Concurrency = Limit AT Lambda**

---

# Usage Plans

REST APIs can use:

**Usage Plans**

to control how clients use APIs.

A usage plan can define:

- Throttling
- Quotas

and can be associated with:

**API keys**

---

# API Keys

API keys can identify:

**API consumers**

and work with usage plans.

Important:

API keys are NOT a replacement for:

**Strong authentication**

### Exam Trap

> **API key does not automatically mean secure user authentication**

Think of API keys primarily for:

**Usage tracking and plan enforcement**

---

# Quotas

Usage plans can enforce:

**Request quotas**

Example:

Customer A:

10,000 requests/month

Customer B:

100,000 requests/month

This supports:

**Tiered API consumption**

---

# API Gateway Authentication

API Gateway can secure APIs through several mechanisms.

Important concepts include:

- IAM authorization
- Cognito User Pools
- Lambda Authorizers

---

# IAM Authorization

IAM can authorize API requests using:

**AWS credentials**

Useful when callers are:

- AWS users
- AWS services
- Applications using IAM credentials

### Killer Exam Clue

> **AWS-authenticated client should call API Gateway using IAM**
>
> → **IAM Authorization**

---

# Cognito User Pools

[[Cognito]] can handle:

**User authentication**

Architecture:

User  
↓  
Cognito  
↓  
Token  
↓  
API Gateway  
↓  
Backend

Use for:

- Web app users
- Mobile app users
- User sign-up/sign-in
- Token-based API authorization

### Killer Exam Clue

> **Authenticate application users before allowing API access**
>
> → **Cognito + API Gateway**

---

# Lambda Authorizer

A:

**Lambda Authorizer**

uses custom Lambda logic to:

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

Use when:

**Custom authorization logic**

is required.

---

# Lambda Authorizer Use Cases

Examples:

- Custom bearer tokens
- Legacy authentication systems
- Custom authorization rules
- External identity providers

### Memory Trick

**Authorizer = Custom Gatekeeper**

---

# Authentication Decision

Need AWS IAM credentials?

→ IAM Authorization

Need normal application users?

→ Cognito

Need custom authorization logic?

→ Lambda Authorizer

---

# API Gateway Caching

REST API Gateway can:

**Cache responses**

This can reduce:

- Backend calls
- Lambda invocations
- Database load
- Response latency

Architecture:

Client  
↓  
API Gateway Cache  
↓  
Cache Hit?

Yes  
→ Return Response

No  
→ Backend

### Killer Exam Clue

> **Reduce repeated backend API processing for identical requests**
>
> → **API Gateway Caching**

---

# Cache TTL

Cached API responses have:

**A configured TTL**

Before expiration:

Requests can receive:

**Cached responses**

After expiration:

API Gateway returns to:

**The backend**

---

# API Gateway + CloudFront

Edge-optimized REST API endpoints use:

**CloudFront infrastructure**

to improve access for:

**Geographically distributed clients**

Think:

Global User  
↓  
CloudFront Edge  
↓  
API Gateway

---

# Endpoint Types

Important API Gateway endpoint concepts include:

- Edge-Optimized
- Regional
- Private

---

# Edge-Optimized Endpoint

Best for:

**Globally distributed clients**

Traffic enters through:

**CloudFront edge locations**

### Memory Trick

**EDGE = GLOBAL CLIENTS**

---

# Regional Endpoint

Best when clients are primarily:

**In the same AWS Region**

or when you want to place your own:

**CloudFront distribution**

in front of the API.

### Memory Trick

**REGIONAL = REGION-LOCAL API**

---

# Private API

A:

**Private API**

is accessible only from:

**Inside a VPC**

through:

**VPC endpoints**

Architecture:

Private Client  
↓  
Interface VPC Endpoint  
↓  
Private API Gateway

### Killer Exam Clue

> **API must not be publicly accessible and should only be reachable from a VPC**
>
> → **Private API Gateway**

---

# Edge vs Regional vs Private

| Requirement | Endpoint Type |
|---|---|
| Global Public Clients | Edge-Optimized |
| Regional Public Clients | Regional |
| Private VPC Access Only | Private |

---

# API Gateway + VPC Link

API Gateway can connect to:

**Private resources inside a VPC**

using:

**VPC Link**

Architecture:

Client  
↓  
API Gateway  
↓  
VPC Link  
↓  
Private Backend

This is useful for private backends such as:

- NLB-backed services
- Private application services

### Killer Exam Clue

> **Public API Gateway must invoke a private VPC backend**
>
> → **VPC Link**

---

# Private API vs VPC Link

Do not confuse these.

### Private API

Controls:

**Who can reach API Gateway**

Think:

Client → API Gateway

### VPC Link

Controls:

**How API Gateway reaches private backend**

Think:

API Gateway → Backend

### Memory Trick

**PRIVATE API = Private FRONT door**

**VPC LINK = Private BACK door**

---

# Request Transformation

API Gateway can transform:

**Incoming requests**

before sending them to:

**The backend**

This is especially relevant with:

**REST APIs**

---

# Response Transformation

API Gateway can also modify:

**Backend responses**

before returning them to:

**Clients**

This can help decouple:

**Client API format**

from:

**Backend implementation format**

---

# Mapping Templates

REST API Gateway supports:

**Mapping Templates**

for transforming request and response payloads.

Think:

Client Format  
↓  
Mapping Template  
↓  
Backend Format

### Killer Exam Clue

> **Transform request payload before sending it to backend**
>
> → **API Gateway Mapping Template**

---

# CORS

**Cross-Origin Resource Sharing — CORS**

controls whether a web application from:

**One origin**

can call an API hosted on:

**Another origin**

Example:

Web App:

`https://app.example.com`

API:

`https://api.example.com`

Browser needs:

**CORS permissions**

---

## CORS Is Browser-Enforced

CORS primarily affects:

**Web browsers**

It does not act as:

**General API authentication**

### Exam Trap

> CORS is NOT an authentication mechanism.

---

# API Gateway Logging

API Gateway integrates with:

[[07-Monitoring/CloudWatch]]

for:

- Access logs
- Execution logs
- Metrics
- Monitoring

This helps troubleshoot:

- API errors
- Latency
- Backend failures
- Request patterns

---

# Important Metrics

Think about metrics such as:

- Request count
- Latency
- Integration latency
- 4XX errors
- 5XX errors

These help determine whether problems originate from:

- Client
- API Gateway
- Backend

---

# 4XX Errors

Generally represent:

**Client-side request problems**

Examples:

- Unauthorized
- Forbidden
- Bad request
- Too many requests

---

# 5XX Errors

Generally represent:

**Server-side / integration problems**

Examples:

- Backend failure
- Lambda error
- Integration issue

---

# API Gateway + WAF

API Gateway can integrate with:

[[06-Security/WAF]]

for protection against:

- Common web attacks
- IP-based rules
- SQL injection patterns
- Cross-site scripting patterns
- Malicious request patterns

### Killer Exam Clue

> **Protect an API from common web exploits**
>
> → **WAF + API Gateway**

---

# API Gateway vs Application Load Balancer

Both can route HTTP traffic.

But they solve different problems.

## API Gateway

Think:

- API management
- Authentication
- Throttling
- Usage plans
- Request transformation
- API stages

## [[Application Load Balancer]]

Think:

- Load balancing
- HTTP routing
- Host/path routing
- EC2/ECS targets
- Lambda targets

### Exam Shortcut

**Full API management**
→ API Gateway

**Load balance web applications**
→ ALB

---

# API Gateway vs Lambda Function URL

### Function URL

Think:

**Simple HTTPS endpoint for one Lambda**

### API Gateway

Think:

**Managed API platform**

Use API Gateway for:

- Multiple routes
- Authentication
- Throttling
- Caching
- Stages
- Transformations

### Memory Trick

**Function URL = Simple Door**

**API Gateway = Full Reception Desk**

---

# API Gateway vs App Runner

### [[App Runner]]

Hosts:

**A web application/API**

### API Gateway

Provides:

**API front door / management**

App Runner can expose its own managed web endpoint.

API Gateway becomes valuable when you need:

**More sophisticated API controls**

---

# API Gateway vs CloudFront

### [[CloudFront]]

Think:

- CDN
- Content caching
- Global content delivery

### API Gateway

Think:

- API management
- Backend integration
- Authorization
- Throttling

They can also work:

**Together**

---

# Serverless API Architecture

One of the strongest SAA patterns:

User  
↓  
CloudFront  
↓  
API Gateway  
↓  
Lambda  
↓  
DynamoDB

Possible additions:

- Cognito
- WAF
- CloudWatch

This provides:

- Global delivery
- API management
- Serverless compute
- Serverless database
- Authentication
- Security

---

# Architecture Thinking

## Scenario 1 — Serverless REST API

Need:

- No servers
- REST endpoints
- Backend logic
- NoSQL database

Choose:

API Gateway  
↓  
Lambda  
↓  
DynamoDB

---

## Scenario 2 — Simple Low-Cost API

Need:

- Basic HTTP API
- Lambda backend
- Lower cost
- No advanced REST features

Choose:

**HTTP API**

---

## Scenario 3 — Advanced API Management

Need:

- API keys
- Usage plans
- Caching
- Request transformations

Choose:

**REST API**

---

## Scenario 4 — Real-Time Chat

Clients need:

**Persistent bidirectional connections**

Choose:

**WebSocket API**

---

## Scenario 5 — Global Clients

Public clients worldwide need:

**Optimized API access**

Choose:

**Edge-Optimized Endpoint**

---

## Scenario 6 — Regional Clients

Most users are:

**In the same Region**

Choose:

**Regional Endpoint**

---

## Scenario 7 — Internal API

API must be accessible only:

**From inside the VPC**

Choose:

**Private API**

---

## Scenario 8 — Private Backend

Public API Gateway needs to invoke:

**Private application service inside VPC**

Choose:

**VPC Link**

---

## Scenario 9 — Backend Overload

Too many requests are reaching:

**Lambda**

Need to limit incoming API rate.

Choose:

**API Gateway Throttling**

---

## Scenario 10 — Subscription Plans

Customers have different:

**Request quotas**

Choose:

**API Keys + Usage Plans**

---

## Scenario 11 — User Authentication

Mobile users need:

**Sign-in and token-based API access**

Choose:

[[Cognito]]  
+  
API Gateway

---

## Scenario 12 — Custom Authentication

Company has custom:

**Bearer token validation logic**

Choose:

**Lambda Authorizer**

---

## Scenario 13 — Repeated GET Requests

Backend repeatedly calculates:

**The same response**

Need lower latency and fewer backend calls.

Choose:

**API Gateway Cache**

---

## Scenario 14 — Transform Payload

Client sends one JSON format.

Backend requires:

**A different format**

Choose:

**Mapping Template**

---

## Scenario 15 — Browser CORS Error

Web frontend and API are hosted on:

**Different origins**

Browser blocks request.

Configure:

**CORS**

---

# Scenario Recognition

Immediately think:

**API Gateway**

when you see:

- Managed API
- REST API
- HTTP API
- WebSocket API
- Serverless API
- Lambda front end
- API throttling
- Usage plans
- API keys
- API stages
- Request transformation

---

## Think REST API When You See

- API cache
- Usage plans
- API keys
- Advanced transformations
- Rich API management features

---

## Think HTTP API When You See

- Simple API
- Lower cost
- Lower latency
- Lambda backend
- Fewer advanced features needed

---

## Think WebSocket When You See

- Real-time
- Persistent connection
- Bidirectional
- Chat
- Live notifications

---

# Exam Traps

## Trap 1 — API Keys Are Strong User Authentication

❌

API keys are mainly associated with:

**Usage tracking and usage plans**

For authentication:

Think IAM, Cognito, or authorizers.

---

## Trap 2 — Private API and VPC Link Are the Same

❌

Private API:

**Private access TO API Gateway**

VPC Link:

**Private access FROM API Gateway to backend**

---

## Trap 3 — CORS Secures the API

❌

CORS is:

**Browser cross-origin policy**

not:

Authentication.

---

## Trap 4 — Function URL Has Every API Gateway Feature

❌

Function URL is:

**Simpler**

---

## Trap 5 — API Gateway and ALB Are Interchangeable

❌

ALB:

**Load balancing**

API Gateway:

**API management**

---

## Trap 6 — HTTP API Always Has Every REST API Feature

❌

HTTP APIs are:

**Simpler**

REST APIs provide:

**More advanced features**

---

## Trap 7 — WebSocket API Uses Normal One-Way Request/Response Only

❌

It supports:

**Persistent two-way communication**

---

## Trap 8 — API Gateway Throttling Controls Lambda Database Connections Directly

❌

It controls:

**Incoming API traffic**

For database connections:

Think:

- Reserved Concurrency
- RDS Proxy

---

# Quick Cheat Sheet

| Exam Clue | Answer |
|---|---|
| Serverless API Front Door | API Gateway |
| Advanced API Features | REST API |
| Simple Low-Cost HTTP API | HTTP API |
| Real-Time Bidirectional API | WebSocket API |
| Global Public Clients | Edge-Optimized |
| Regional Public Clients | Regional |
| VPC-Only API | Private API |
| API → Private VPC Backend | VPC Link |
| Limit Requests | Throttling |
| Customer Quotas | Usage Plans |
| Identify API Consumers | API Keys |
| User Authentication | Cognito |
| Custom Authorization | Lambda Authorizer |
| Cache API Responses | API Gateway Cache |
| Transform Payload | Mapping Template |
| Browser Cross-Origin Access | CORS |
| Protect Web API | WAF |

---

# Authentication Decision

AWS caller?

→ IAM

Application users?

→ Cognito

Custom token/auth logic?

→ Lambda Authorizer

---

# Endpoint Decision

Global public clients?

→ Edge-Optimized

Regional public clients?

→ Regional

Internal VPC clients only?

→ Private

---

# API Type Decision

Need:

**Advanced REST features**

→ REST API

Need:

**Simple low-cost HTTP API**

→ HTTP API

Need:

**Persistent bidirectional connection**

→ WebSocket API

---

# Final Exam Rapid-Fire

> **SERVERLESS API**
> → API GATEWAY + LAMBDA
>
> **ADVANCED API FEATURES**
> → REST API
>
> **SIMPLE + CHEAPER**
> → HTTP API
>
> **CHAT / LIVE CONNECTION**
> → WEBSOCKET API
>
> **GLOBAL CLIENTS**
> → EDGE-OPTIMIZED
>
> **REGION-LOCAL CLIENTS**
> → REGIONAL
>
> **VPC-ONLY API**
> → PRIVATE API
>
> **API → PRIVATE BACKEND**
> → VPC LINK
>
> **LIMIT REQUEST RATE**
> → THROTTLING
>
> **CLIENT QUOTA**
> → USAGE PLAN
>
> **API CONSUMER ID**
> → API KEY
>
> **USER LOGIN**
> → COGNITO
>
> **CUSTOM AUTH**
> → LAMBDA AUTHORIZER
>
> **REPEATED RESPONSE**
> → API CACHE
>
> **CHANGE REQUEST FORMAT**
> → MAPPING TEMPLATE
>
> **BROWSER CROSS-ORIGIN**
> → CORS
>
> **WEB ATTACK PROTECTION**
> → WAF

---

## Master Memory Trick

> [!tip] API Gateway Master Memory Trick
> Imagine API Gateway as:
>
> **A hotel front desk**
>
> A guest arrives:
>
> **REQUEST**
>
> The front desk checks:
>
> **WHO ARE YOU?**
> → Authentication
>
> **ARE YOU ALLOWED?**
> → Authorization
>
> **ARE YOU CALLING TOO MUCH?**
> → Throttling
>
> **WHICH ROOM DO YOU NEED?**
> → Routing
>
> **DO I ALREADY HAVE THE ANSWER?**
> → Caching
>
> **DOES YOUR REQUEST NEED TRANSLATING?**
> → Transformation
>
> Then it sends the request to:
>
> **THE BACKEND**

So remember:

> **API GATEWAY**
> → FRONT DOOR
>
> **REST API**
> → MORE FEATURES
>
> **HTTP API**
> → SIMPLE + CHEAPER
>
> **WEBSOCKET**
> → TWO-WAY REAL-TIME
>
> **THROTTLING**
> → LIMIT RATE
>
> **USAGE PLAN**
> → QUOTA
>
> **COGNITO**
> → USERS
>
> **AUTHORIZER**
> → CUSTOM AUTH
>
> **CACHE**
> → REDUCE BACKEND WORK
>
> **VPC LINK**
> → PRIVATE BACKEND

And the killer SAA question:

> **"Does the application need a managed API front door with routing, security, throttling, and backend integration?"**
>
> YES
>
> → **API Gateway**

---

## Related Notes

- [[Lambda]]
- [[DynamoDB]]
- [[Cognito]]
- [[Application Load Balancer]]
- [[CloudFront]]
- [[06-Security/WAF]]
- [[07-Monitoring/CloudWatch]]
- [[RDS Proxy]]