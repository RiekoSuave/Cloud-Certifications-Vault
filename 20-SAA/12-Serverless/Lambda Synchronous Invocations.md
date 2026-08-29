## What Is a Synchronous Invocation?

A:

**Synchronous Invocation**

means the caller invokes a [[Lambda]] function and:

**Waits for the function to finish and return a response**

Architecture:

Caller  
↓  
Invoke Lambda  
↓  
Lambda Executes  
↓  
Response Returned  
↓  
Caller

> [!tip] Memory Trick
> **Synchronous = CALL → WAIT → RESPONSE**

---

## Core Concept

With synchronous invocation:

1. Client sends request
2. Lambda executes
3. Client waits
4. Lambda returns result
5. Client receives response

Think:

**Request / Response**

This is ideal when the caller:

**Needs the result immediately**

---

## Common Synchronous Invocation Sources

Common examples include:

- [[API Gateway]]
- Application Load Balancer
- Lambda Function URLs
- AWS SDK
- AWS CLI
- Another Lambda function

### Killer Exam Clue

> **Caller must wait for Lambda to return a result**
>
> → **Synchronous Invocation**

---

# API Gateway + Lambda

One of the most important serverless architectures:

Client  
↓  
[[API Gateway]]  
↓  
Lambda  
↓  
Response  
↓  
API Gateway  
↓  
Client

Use this for:

- REST APIs
- HTTP APIs
- Serverless backends
- Mobile application APIs
- Web application APIs

### Memory Trick

**API Gateway = Front Door**

**Lambda = Logic**

---

## Example

Client sends:

`GET /products/123`

Architecture:

Client  
↓  
API Gateway  
↓  
Lambda  
↓  
DynamoDB  
↓  
Lambda  
↓  
API Gateway  
↓  
Client

The client waits for:

**The response**

Therefore:

**Synchronous**

---

# Application Load Balancer + Lambda

An:

[[Application Load Balancer]]

can invoke Lambda as a:

**Target**

Architecture:

Client  
↓  
ALB  
↓  
Lambda  
↓  
Response  
↓  
ALB  
↓  
Client

This provides another way to expose:

**HTTP/HTTPS Lambda applications**

---

## ALB Lambda Target

Instead of:

ALB  
↓  
EC2

or:

ALB  
↓  
ECS

you can use:

ALB  
↓  
Lambda

### Exam Clue

> **Existing ALB architecture needs serverless backend processing**
>
> → **Lambda as an ALB target**

---

# Lambda Function URLs

A Lambda function can have a:

**Dedicated HTTPS endpoint**

Architecture:

Client  
↓  
Function URL  
↓  
Lambda  
↓  
Response

This provides:

**Direct HTTP access**

without requiring:

**API Gateway**

---

## Function URL vs API Gateway

### Function URL

Think:

**Simple HTTPS endpoint**

Best when:

- One function
- Simple HTTP access
- Minimal API features

### API Gateway

Think:

**Full API management**

Useful when you need features such as:

- Multiple routes
- Authentication / authorization options
- Throttling
- Request/response transformations
- API stages
- More advanced API management

### Killer Exam Shortcut

**Simple HTTPS → Lambda**
→ Function URL

**Full API platform**
→ API Gateway

---

# AWS SDK / CLI

Applications can invoke Lambda directly through:

**AWS APIs**

Examples:

Application  
↓  
AWS SDK  
↓  
Lambda

or:

Administrator  
↓  
AWS CLI  
↓  
Lambda

If the invocation requests:

**A synchronous response**

the caller waits for:

**The function result**

---

# Lambda Calling Lambda

One Lambda function can invoke:

**Another Lambda function**

Architecture:

Lambda A  
↓  
Lambda B  
↓  
Response  
↓  
Lambda A

If Lambda A waits for Lambda B:

**Synchronous Invocation**

---

## Lambda-to-Lambda Exam Consideration

Although possible, tightly chaining many Lambda functions directly can create:

- Increased coupling
- More complicated error handling
- Longer execution duration
- Harder workflow management

If multiple functions form:

**A workflow**

consider:

[[Step Functions]]

### Memory Trick

**Lambda = Do Work**

**Step Functions = Coordinate Work**

---

# Error Handling

This is one of the most important differences between:

**Synchronous**

and:

**Asynchronous**

Lambda invocation.

With synchronous invocation:

> **The caller is responsible for handling errors and retries**

Architecture:

Caller  
↓  
Lambda  
↓  
Error  
↓  
Caller

Lambda returns:

**The error response**

to the caller.

Lambda does NOT automatically provide the same built-in retry behavior used for:

**Asynchronous invocation**

---

## Killer Exam Clue

> **Synchronous Lambda invocation fails. Who handles retries?**
>
> → **The caller**

---

# Retry Responsibility

Example:

Application  
↓  
Lambda  
↓  
Failure

The application can:

- Retry immediately
- Use exponential backoff
- Stop retrying
- Return an error to the user

The decision belongs to:

**The caller**

### Memory Trick

**SYNC = Caller Owns Retry**

---

# Timeout Behavior

The caller waits while:

**Lambda executes**

This creates an important architecture consideration.

Even though Lambda can execute for up to:

**15 minutes**

the calling service may have:

**A shorter timeout**

### SAA Principle

> **Always consider the timeout of the entire request path, not only Lambda's timeout.**

---

# API Gateway Timeout Consideration

Suppose:

Client  
↓  
API Gateway  
↓  
Lambda

Even if Lambda supports a longer runtime:

The API layer may have:

**Its own integration timeout**

Therefore, long-running work may not fit:

**A synchronous API architecture**

---

# Long-Running Work

If processing takes a long time:

Instead of:

Client  
↓  
Wait  
↓  
Lambda

consider:

Client  
↓  
Submit Job  
↓  
Queue / Workflow  
↓  
Background Processing

This changes the architecture toward:

**Asynchronous processing**

---

# Synchronous vs Asynchronous Thinking

## Synchronous

Caller:

**Waits**

Best for:

- APIs
- Immediate validation
- Queries
- Interactive applications

---

## Asynchronous

Caller:

**Does not wait**

Best for:

- Background processing
- Event processing
- Notifications
- File processing
- Decoupled workflows

### Memory Trick

**SYNC = I NEED THE ANSWER**

**ASYNC = JUST DO THE JOB**

---

# Synchronous Invocation Permissions

The caller needs permission to:

**Invoke the Lambda function**

This may involve:

- IAM permissions
- Lambda resource-based policies

depending on:

**Who is invoking the function**

---

# Resource-Based Policy

Lambda resource-based policies determine:

**Who or what can invoke the function**

Examples:

API Gateway  
↓  
Permission  
↓  
Lambda

ALB  
↓  
Permission  
↓  
Lambda

### Memory Trick

**Resource Policy = Who Can Call Me?**

---

# Execution Role

Do NOT confuse invocation permissions with:

**Lambda Execution Role**

The execution role determines:

**What Lambda can access after it starts**

Example:

API Gateway  
↓  
Lambda  
↓  
Execution Role  
↓  
DynamoDB

### Master IAM Distinction

**Who can invoke Lambda?**
→ Invocation permission / resource-based policy

**What can Lambda access?**
→ Execution role

---

# API Gateway + Lambda + DynamoDB

Classic architecture:

Client  
↓  
API Gateway  
↓  
Lambda  
↓  
DynamoDB  
↓  
Lambda  
↓  
API Gateway  
↓  
Client

This provides:

- Serverless API layer
- Serverless compute
- Serverless database

### Killer Exam Pattern

> **Highly scalable serverless REST API**
>
> → **API Gateway + Lambda + DynamoDB**

---

# API Gateway Authentication

API Gateway can sit in front of Lambda and provide:

**Authentication and authorization mechanisms**

This is one reason to choose API Gateway instead of:

**A basic Function URL**

when building more advanced APIs.

---

# ALB vs API Gateway for Lambda

Both can invoke:

**Lambda synchronously**

But they solve different problems.

### ALB

Think:

- Load balancing
- Existing HTTP architecture
- Multiple target types
- Host/path routing

### API Gateway

Think:

- API management
- REST/HTTP APIs
- API authentication
- Throttling
- Request transformation

### Function URL

Think:

**Simple direct HTTPS**

---

# Comparison Table

| Requirement | Function URL | API Gateway | ALB |
|---|---:|---:|---:|
| Invoke Lambda via HTTP | ✅ | ✅ | ✅ |
| Simple Direct Endpoint | ✅ | Possible | ❌ |
| Full API Management | ❌ | ✅ | ❌ |
| API Throttling / Stages | ❌ | ✅ | ❌ |
| Load Balancer Architecture | ❌ | ❌ | ✅ |
| Path-Based Routing | Limited | ✅ | ✅ |
| Existing ALB Environment | ❌ | ❌ | ✅ |

---

# Client Error Handling

Suppose:

Client  
↓  
API Gateway  
↓  
Lambda  
↓  
Database

Database temporarily fails.

Lambda returns:

**Error**

The synchronous caller can then:

- Retry
- Display an error
- Apply backoff
- Use another recovery strategy

### Key Point

Lambda itself does NOT guarantee:

**Automatic synchronous retries**

---

# Throttling

If Lambda cannot accept additional executions because of:

**Concurrency limits**

the synchronous caller can receive:

**A throttling error**

The caller should implement:

**Retry with exponential backoff**

when appropriate.

### Killer Exam Pattern

> **Synchronous Lambda calls are throttled**
>
> → **Caller should retry with exponential backoff**

---

# Exponential Backoff

Instead of retrying:

Immediately  
↓  
Immediately  
↓  
Immediately

use increasing delays:

Retry  
↓  
Wait  
↓  
Retry  
↓  
Wait Longer  
↓  
Retry

This reduces:

**Additional pressure on the service**

---

# Synchronous API Performance

For interactive applications:

**Latency matters**

Possible sources of latency include:

- Lambda cold starts
- Database calls
- External API calls
- VPC networking
- Large initialization code

If cold starts are unacceptable:

Think:

**Provisioned Concurrency**

---

# Provisioned Concurrency

For synchronous workloads requiring:

**Consistent low latency**

use:

**Provisioned Concurrency**

Architecture:

API Request  
↓  
Pre-Initialized Lambda Environment  
↓  
Fast Execution

### Killer Exam Clue

> **Interactive Lambda API has unacceptable cold-start latency**
>
> → **Provisioned Concurrency**

---

# Reserved Concurrency

If the synchronous function could overwhelm:

**A downstream system**

use:

**Reserved Concurrency**

to control:

**Maximum simultaneous executions**

Example:

API Gateway  
↓  
Lambda  
↓  
RDS

Limit Lambda concurrency to help protect:

**RDS**

---

# RDS Proxy

For synchronous Lambda APIs connecting to:

[[RDS]]

consider:

[[RDS Proxy]]

Architecture:

Client  
↓  
API Gateway  
↓  
Lambda  
↓  
RDS Proxy  
↓  
RDS

RDS Proxy helps:

**Pool database connections**

### Killer Exam Clue

> **High-concurrency Lambda API overwhelms RDS with connections**
>
> → **RDS Proxy**

---

# Architecture Thinking

## Scenario 1 — REST API

Client sends request and expects:

**Immediate JSON response**

Choose:

API Gateway  
↓  
Lambda

Invocation:

**Synchronous**

---

## Scenario 2 — Direct HTTPS

A simple application needs:

**One HTTPS endpoint directly invoking Lambda**

No advanced API management required.

Choose:

**Lambda Function URL**

---

## Scenario 3 — Existing ALB

Company already uses:

**Application Load Balancer**

and wants:

**Serverless backend logic**

Choose:

ALB  
↓  
Lambda

---

## Scenario 4 — Function Failure

A synchronous Lambda invocation fails.

Who retries?

**The caller**

---

## Scenario 5 — Cold Starts

Customer-facing API requires:

**Predictable low latency**

Choose:

**Provisioned Concurrency**

---

## Scenario 6 — Database Overload

API traffic causes Lambda concurrency to explode.

RDS receives too many connections.

Choose:

**RDS Proxy**

Potentially combine with:

**Concurrency controls**

---

## Scenario 7 — Long Processing

API request triggers processing that takes:

**Several minutes**

Users should not wait.

Move toward:

**Asynchronous architecture**

Example:

API Gateway  
↓  
Queue  
↓  
Background Processor

---

## Scenario 8 — Multiple Workflow Steps

Lambda A synchronously calls B, which calls C, which calls D.

Architecture becomes difficult to manage.

Think:

[[Step Functions]]

---

# Scenario Recognition

Immediately think:

**Synchronous Lambda**

when you see:

- Caller waits
- Immediate response
- Request/response
- REST API
- HTTP API
- Function URL
- ALB Lambda target
- Direct SDK invocation

---

# Think Asynchronous Instead When You See

- Background processing
- Caller should not wait
- Event processing
- File processing
- Long-running workflow
- Decoupling
- Buffering

---

# Exam Traps

## Trap 1 — Lambda Automatically Retries Failed Synchronous Invocations

❌

The:

**Caller handles retries**

---

## Trap 2 — Lambda's 15-Minute Timeout Means Every Caller Waits 15 Minutes

❌

The calling service may have:

**A shorter timeout**

---

## Trap 3 — API Gateway Is Required for Every HTTP Lambda

❌

Options include:

- Function URL
- API Gateway
- ALB

---

## Trap 4 — Function URL Provides Every API Gateway Feature

❌

Function URL is:

**Simpler**

API Gateway provides:

**Advanced API management**

---

## Trap 5 — Lambda Execution Role Controls Who Can Invoke It

❌

Execution Role:

**Lambda → AWS**

Invocation permission:

**Caller → Lambda**

---

## Trap 6 — Reserved Concurrency Fixes Cold Starts

❌

Think:

**Provisioned Concurrency**

---

## Trap 7 — Provisioned Concurrency Protects RDS by Limiting Maximum Executions

❌

Think:

**Reserved Concurrency**

for concurrency control.

---

## Trap 8 — Synchronous Is Best for Long Background Processing

❌

Use:

**Asynchronous / decoupled architecture**

when the caller does not need to wait.

---

# Quick Cheat Sheet

| Exam Clue | Answer |
|---|---|
| Caller Waits | Synchronous |
| Immediate Response | Synchronous |
| REST API | API Gateway + Lambda |
| Simple HTTPS Endpoint | Function URL |
| Existing Load Balancer | ALB + Lambda |
| Sync Failure Retry | Caller |
| Throttled Sync Call | Exponential Backoff |
| Reduce Cold Starts | Provisioned Concurrency |
| Control Max Concurrency | Reserved Concurrency |
| Too Many DB Connections | RDS Proxy |
| Complex Function Workflow | Step Functions |
| Background Processing | Asynchronous |

---

# Invocation Comparison

| Feature | Synchronous | Asynchronous |
|---|---|---|
| Caller Waits | ✅ | ❌ |
| Immediate Response | ✅ | ❌ |
| Request / Response | ✅ | ❌ |
| Caller Handles Retry | ✅ | ❌ Normally |
| Background Processing | ❌ | ✅ |
| API Workloads | ✅ | Possible |
| Event Processing | Possible | ✅ |

---

# HTTP Lambda Decision

Need HTTP access to Lambda?

↓

Need:

**Full API management**

→ [[API Gateway]]

Need:

**Simple direct HTTPS**

→ Function URL

Already using:

**Application Load Balancer**

→ ALB Lambda Target

---

# Final Exam Rapid-Fire

> **CALLER WAITS**
> → SYNCHRONOUS
>
> **REQUEST / RESPONSE**
> → SYNCHRONOUS
>
> **SERVERLESS REST API**
> → API GATEWAY + LAMBDA
>
> **SIMPLE HTTPS**
> → FUNCTION URL
>
> **EXISTING LOAD BALANCER**
> → ALB + LAMBDA
>
> **SYNC FAILURE**
> → CALLER HANDLES RETRY
>
> **THROTTLING**
> → EXPONENTIAL BACKOFF
>
> **COLD START LATENCY**
> → PROVISIONED CONCURRENCY
>
> **LIMIT SCALE**
> → RESERVED CONCURRENCY
>
> **RDS CONNECTIONS**
> → RDS PROXY
>
> **COMPLEX WORKFLOW**
> → STEP FUNCTIONS
>
> **CALLER SHOULD NOT WAIT**
> → ASYNCHRONOUS

---

## Master Memory Trick

> [!tip] Synchronous Invocation Master Memory Trick
> Think of synchronous Lambda like:
>
> **Calling a restaurant to place an order while staying on the phone.**
>
> You:
>
> **CALL**
>
> Then:
>
> **WAIT**
>
> The restaurant finishes:
>
> **WORK**
>
> Then gives you:
>
> **THE ANSWER**
>
> Only then do you hang up.

So remember:

> **SYNC**
> → CALL
> → WAIT
> → RESPONSE
>
> **FAILURE**
> → CALLER RETRIES
>
> **WEB API**
> → API GATEWAY
>
> **SIMPLE HTTPS**
> → FUNCTION URL
>
> **EXISTING LOAD BALANCER**
> → ALB
>
> **COLD START**
> → PROVISIONED CONCURRENCY
>
> **DATABASE CONNECTION EXPLOSION**
> → RDS PROXY

And the killer SAA question:

> **"Does the caller need the Lambda result before it can continue?"**
>
> YES
>
> → **Synchronous Invocation**

---

## Related Notes

- [[Lambda]]
- [[API Gateway]]
- [[Application Load Balancer]]
- [[04-Databases/DynamoDB]]
- [[RDS]]
- [[RDS Proxy]]
- [[Step Functions]]
- [[IAM]]