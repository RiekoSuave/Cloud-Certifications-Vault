
## What Problem Does It Solve?

[[Lambda Concurrency]] controls:

**How many Lambda function executions can run at the same time**

This matters because Lambda can scale:

**Very quickly**

and that can affect:

- Downstream databases
- APIs
- Queues
- Account limits
- Latency
- Cost

Architecture:

Many Requests  
↓  
Lambda  
↓  
Concurrent Executions

> [!tip] Memory Trick
> **Concurrency = How many Lambdas are running RIGHT NOW**

---

## Core Concept

Suppose a Lambda function takes:

**1 second**

to process one request.

If:

10 requests arrive at once

Lambda may need:

**10 concurrent executions**

If:

1,000 requests arrive at once

Lambda may need:

**1,000 concurrent executions**

Concurrency is therefore:

**Simultaneous function execution**

---

## Concurrency Formula

A useful mental model:

**Concurrency ≈ Requests per Second × Average Duration**

Example:

100 requests/sec  
×  
2 seconds

≈

**200 concurrent executions**

This is useful for understanding:

**Why long-running functions consume more concurrency**

---

## Why Concurrency Matters

Lambda scaling can be:

**Much faster**

than some downstream systems.

Example:

Traffic Spike  
↓  
Lambda Scales Rapidly  
↓  
Thousands of Executions  
↓  
RDS

Potential problem:

**Too many database connections**

So concurrency is not only about:

**Lambda performance**

It is also about:

**Protecting the rest of the architecture**

---

# Account Concurrency

Lambda concurrency is generally governed by:

**Regional account concurrency limits**

Functions in the same Region can share:

**The available concurrency pool**

Conceptually:

Regional Concurrency Pool  
↓  
├── Function A
├── Function B
└── Function C

If one function consumes too much:

Other functions may have:

**Less capacity available**

---

## Unreserved Concurrency

Functions without dedicated reserved concurrency use:

**The shared unreserved concurrency pool**

Example:

Account Pool  
↓  
Function A  
Function B  
Function C

They compete for:

**Available concurrency**

---

# Reserved Concurrency

**Reserved Concurrency**

reserves part of the concurrency pool for:

**A specific function**

and simultaneously sets:

**That function's maximum concurrency**

Example:

Function A  
Reserved Concurrency = 100

Result:

Function A has:

**Up to 100 concurrent executions reserved**

and cannot exceed:

**100**

### Killer Exam Clue

> **Guarantee concurrency for one function while limiting how much it can consume**
>
> → **Reserved Concurrency**

---

## Reserved Concurrency Does Two Things

Reserved Concurrency:

### 1. Reserves Capacity

Makes concurrency available specifically for:

**That function**

### 2. Limits Maximum Scale

The function cannot exceed:

**Its reserved amount**

### Memory Trick

**RESERVED = RESERVE + RESTRICT**

---

## Example

Account concurrency pool:

1,000

Function A:

Reserved = 200

Function B:

No reservation

Function C:

No reservation

Function A has:

**200 concurrency reserved**

The remaining shared pool is reduced accordingly.

---

## Why Reserve Concurrency?

Use Reserved Concurrency when:

- Function must have guaranteed capacity
- Function must not consume the whole account pool
- Downstream system needs protection
- You need predictable maximum parallelism

---

# Protecting a Database

Architecture:

API Gateway  
↓  
Lambda  
↓  
RDS

Problem:

Lambda scales to:

2,000 executions

RDS can only safely support:

200 application connections

Solution can include:

**Reserved Concurrency**

to limit function parallelism.

Example:

Reserved Concurrency = 200

### Killer Exam Pattern

> **Prevent Lambda from overwhelming a downstream database**
>
> → **Reserved Concurrency**

---

# Reserved Concurrency = 0

A special case:

Reserved Concurrency = 0

Result:

**The function cannot execute**

This can be used to:

**Temporarily stop function invocations**

### Memory Trick

**Reserved 0 = OFF**

---

# Provisioned Concurrency

**Provisioned Concurrency**

solves a different problem.

It keeps:

**Execution environments initialized and ready**

to reduce:

**Cold-start latency**

Architecture:

Request  
↓  
Pre-Warmed Lambda Environment  
↓  
Fast Execution

### Killer Exam Clue

> **Need predictable low latency**
>
> → **Provisioned Concurrency**

---

# Reserved vs Provisioned Concurrency

This distinction is one of the most important Lambda exam topics.

## Reserved Concurrency

Think:

- Capacity allocation
- Maximum concurrency
- Protect downstream systems
- Prevent noisy-neighbor functions

## Provisioned Concurrency

Think:

- Pre-initialized environments
- Reduce cold starts
- Predictable latency

### Memory Trick

**RESERVED = CAPACITY CONTROL**

**PROVISIONED = LATENCY CONTROL**

---

## Quick Comparison

| Requirement | Reserved | Provisioned |
|---|---:|---:|
| Reserve Capacity | ✅ | ❌ Primary Purpose |
| Set Max Concurrency | ✅ | ❌ |
| Reduce Cold Starts | ❌ | ✅ |
| Protect RDS | ✅ | ❌ |
| Predictable Low Latency | ❌ | ✅ |
| Pre-Warm Environments | ❌ | ✅ |

---

# Cold Starts

When Lambda needs a new execution environment:

It may need to:

- Initialize runtime
- Load code
- Load dependencies
- Run initialization logic

This creates:

**Cold-start latency**

Provisioned Concurrency keeps environments:

**Ready ahead of time**

---

# Provisioned Concurrency Example

Customer-facing API:

Client  
↓  
API Gateway  
↓  
Lambda

Requirement:

P99 latency must remain:

**Very low**

Problem:

Cold starts occasionally add latency.

Solution:

**Provisioned Concurrency**

---

# Reserved + Provisioned Together

A function can use:

**Both concepts**

because they solve:

**Different problems**

Example:

Reserved Concurrency:

200

Provisioned Concurrency:

50

Meaning:

- Function maxes out around 200 concurrent executions
- 50 execution environments are kept warm

### Memory Trick

**Reserved says HOW MANY MAX**

**Provisioned says HOW MANY READY**

---

# Lambda Scaling

Lambda automatically scales as:

**Concurrent requests increase**

Conceptually:

1 Concurrent Request  
↓  
1 Execution Environment

100 Concurrent Requests  
↓  
Many Execution Environments

This is why Lambda can handle:

**Bursty workloads**

without manually configuring servers.

---

# Scaling Rate

Lambda scaling is managed by AWS and can increase rapidly.

For SAA, the important point is:

> **Lambda scales automatically, but service quotas and concurrency controls still matter**

Do NOT assume:

**Unlimited instant scale**

---

# Throttling

When Lambda cannot obtain more concurrency:

Invocations can be:

**Throttled**

Possible causes:

- Account concurrency exhausted
- Function reserved concurrency reached
- Other quota constraints

### Memory Trick

**No Concurrency Available = Throttle**

---

# Throttling and Synchronous Invocations

For:

**Synchronous invocations**

the caller receives:

**A throttling error**

The caller should generally handle:

**Retries with exponential backoff**

---

# Throttling and Asynchronous Invocations

For:

**Asynchronous invocations**

Lambda can retry according to:

**Async retry behavior**

because:

**Lambda manages the event**

---

# Throttling and Event Source Mapping

For sources such as:

- SQS
- Kinesis
- DynamoDB Streams

the behavior depends on:

**The source integration**

Messages or stream records remain in:

**The source**

until processing can continue according to source semantics.

---

# Concurrency + SQS

Architecture:

SQS Backlog  
↓  
Lambda Event Source Mapping  
↓  
Lambda Scaling

As queue depth rises:

Lambda can increase:

**Concurrent processing**

This helps clear:

**The backlog**

---

## Why SQS Can Protect Lambda Workloads

SQS provides:

**Buffering**

If traffic spikes:

Messages wait in:

**The queue**

rather than requiring all work to execute:

**Immediately**

This can protect:

- Lambda
- Downstream APIs
- Databases

---

# Reserved Concurrency + SQS

Suppose:

10,000 messages are waiting.

Without a concurrency limit:

Lambda may scale aggressively.

With:

Reserved Concurrency = 50

only approximately:

**50 concurrent function executions**

can run.

The rest of the work remains:

**Buffered in SQS**

### Killer Architecture Pattern

> **Control serverless worker throughput**
>
> → **SQS + Reserved Concurrency**

---

# Concurrency + Kinesis

With [[20-SAA/10-Messaging/Kinesis Data Streams]]:

Lambda concurrency is closely related to:

- Number of shards
- Event source mapping settings
- Parallelization factor

This differs from:

**Request-driven Lambda scaling**

---

# Concurrency + DynamoDB Streams

DynamoDB Streams behaves similarly to:

**Ordered stream processing**

Concurrency depends on:

**Stream partitions and event source mapping behavior**

---

# Concurrency + API Gateway

Architecture:

Clients  
↓  
API Gateway  
↓  
Lambda

A traffic burst can create:

**Large Lambda concurrency**

If the backend cannot handle that load:

Possible controls include:

- API Gateway throttling
- Reserved Concurrency
- Queue-based architecture
- RDS Proxy

depending on the requirement.

---

# API Gateway Throttling vs Lambda Reserved Concurrency

These protect at:

**Different layers**

### API Gateway Throttling

Controls:

**Incoming API request rate**

### Lambda Reserved Concurrency

Controls:

**Concurrent function execution**

### Memory Trick

**API Gateway = Control requests BEFORE Lambda**

**Reserved Concurrency = Control executions AT Lambda**

---

# Concurrency + RDS Proxy

If Lambda connects to:

[[RDS]]

two major problems can arise:

### Problem 1

Too many Lambda executions

Solution:

**Reserved Concurrency**

### Problem 2

Too many database connections

Solution:

[[RDS Proxy]]

These can be used:

**Together**

Architecture:

API Gateway  
↓  
Lambda  
↓  
RDS Proxy  
↓  
RDS

---

# Reserved Concurrency vs RDS Proxy

Do not confuse them.

### Reserved Concurrency

Limits:

**How many Lambda executions run**

### RDS Proxy

Pools:

**Database connections**

### Memory Trick

**Reserved = Control Lambda**

**Proxy = Control Connections**

---

# Concurrency + Downstream API

Suppose Lambda calls:

**An external API**

that allows only:

100 requests/second

If Lambda scales too quickly:

External API may return:

**Rate-limit errors**

Possible solution:

Limit Lambda concurrency or:

**Buffer work through SQS**

depending on architecture.

---

# Concurrency and Function Duration

Longer functions hold:

**Concurrency slots longer**

Example:

Function A:

100 requests/sec  
×  
0.1 sec

≈ 10 concurrency

Function B:

100 requests/sec  
×  
10 sec

≈ 1,000 concurrency

### Exam Principle

> **Long execution duration can dramatically increase concurrency requirements**

---

# Optimize Duration

Reducing Lambda duration can:

- Reduce concurrency consumption
- Improve latency
- Lower compute cost in some scenarios
- Increase throughput

Possible methods:

- More efficient code
- Increase memory if CPU-limited
- Cache reusable resources
- Optimize downstream calls

---

# Connection Reuse

Warm Lambda environments can sometimes reuse:

- Database clients
- HTTP connections
- SDK clients

when initialized outside:

**The handler**

This can improve:

**Performance**

But do not store critical application state that assumes:

**The environment will always persist**

---

# Concurrency and Stateless Design

Because multiple Lambda executions can run:

**Simultaneously**

functions should avoid relying on:

**Shared local mutable state**

Persistent state belongs in:

- DynamoDB
- S3
- RDS
- ElastiCache
- EFS

depending on requirements.

---

# Architecture Thinking

## Scenario 1 — Protect RDS

Lambda scales too quickly and overloads:

**RDS**

Choose:

**Reserved Concurrency**

and potentially:

**RDS Proxy**

---

## Scenario 2 — Cold Start

Interactive API has unpredictable:

**Startup latency**

Choose:

**Provisioned Concurrency**

---

## Scenario 3 — Critical Function Needs Guaranteed Capacity

Other Lambda functions consume account concurrency.

Critical function must always retain:

**100 concurrent executions**

Choose:

**Reserved Concurrency = 100**

---

## Scenario 4 — Stop Function Temporarily

Need to prevent:

**Any invocation**

without deleting the function.

Set:

**Reserved Concurrency = 0**

---

## Scenario 5 — Queue Backlog

SQS backlog can be processed, but downstream service allows only:

**50 concurrent operations**

Choose:

SQS  
↓  
Lambda  
↓  
Reserved Concurrency = 50

---

## Scenario 6 — Low Latency + Capacity Control

Function needs:

- 50 warm environments
- Maximum 200 concurrent executions

Use:

- Provisioned Concurrency = 50
- Reserved Concurrency = 200

---

## Scenario 7 — API Request Flood

Public API receives huge burst traffic.

Need to limit request rate before Lambda.

Think:

**API Gateway Throttling**

rather than relying only on:

Lambda concurrency limits.

---

# Scenario Recognition

Immediately think:

**Reserved Concurrency**

when you see:

- Limit Lambda scaling
- Protect downstream resource
- Reserve capacity
- Prevent function from using all concurrency
- Guaranteed concurrency
- Disable function with zero

---

## Immediately Think Provisioned Concurrency When You See

- Cold starts
- Predictable latency
- Pre-warmed Lambda
- Customer-facing low-latency API

---

## Think RDS Proxy When You See

- Too many database connections
- Lambda + RDS
- Connection pooling
- Bursty DB connections

---

# Exam Traps

## Trap 1 — Reserved Concurrency Removes Cold Starts

❌

Use:

**Provisioned Concurrency**

---

## Trap 2 — Provisioned Concurrency Limits Maximum Scale

❌

Think:

**Reserved Concurrency**

---

## Trap 3 — Reserved Concurrency Only Guarantees Capacity

Incomplete.

It also:

**Limits the function's maximum concurrency**

---

## Trap 4 — Lambda Automatically Has Unlimited Concurrency

❌

Concurrency is governed by:

**Quotas and available capacity**

---

## Trap 5 — More Requests Always Means Faster Processing

❌

Downstream systems can become:

**The bottleneck**

---

## Trap 6 — RDS Proxy Limits Lambda Concurrency

❌

RDS Proxy manages:

**Database connections**

---

## Trap 7 — SQS Backlog Is Lost When Reserved Concurrency Is Low

❌

Messages remain:

**Buffered in SQS**

according to queue semantics.

---

## Trap 8 — Reserved Concurrency = 0 Deletes the Function

❌

It effectively:

**Prevents execution**

but the function still exists.

---

# Quick Cheat Sheet

| Exam Clue | Answer |
|---|---|
| Simultaneous Lambda Executions | Concurrency |
| Limit Function Scaling | Reserved Concurrency |
| Guarantee Function Capacity | Reserved Concurrency |
| Protect Downstream Resource | Reserved Concurrency |
| Disable Function | Reserved Concurrency = 0 |
| Reduce Cold Starts | Provisioned Concurrency |
| Pre-Warm Lambda | Provisioned Concurrency |
| Too Many RDS Connections | RDS Proxy |
| Control API Request Rate | API Gateway Throttling |
| Queue Work While Limited | SQS |
| Throttled Sync Invocation | Caller Retry / Backoff |

---

# Reserved vs Provisioned

| Requirement | Reserved | Provisioned |
|---|---:|---:|
| Maximum Execution Limit | ✅ | ❌ |
| Dedicated Capacity | ✅ | ❌ Primary |
| Prevent Noisy Neighbor | ✅ | ❌ |
| Protect Database | ✅ | ❌ |
| Reduce Cold Start | ❌ | ✅ |
| Keep Environments Warm | ❌ | ✅ |
| Improve Predictable Latency | ❌ | ✅ |

---

# Concurrency Decision Tree

Need to control:

**HOW MANY Lambda executions can run?**

→ Reserved Concurrency

Need to control:

**HOW FAST the first request starts?**

→ Provisioned Concurrency

Need to control:

**HOW MANY database connections exist?**

→ RDS Proxy

Need to control:

**HOW MANY requests enter the API?**

→ API Gateway Throttling

Need to hold:

**Work that cannot execute yet?**

→ SQS

---

# Final Exam Rapid-Fire

> **SIMULTANEOUS EXECUTIONS**
> → CONCURRENCY
>
> **LIMIT LAMBDA SCALE**
> → RESERVED CONCURRENCY
>
> **GUARANTEE CAPACITY**
> → RESERVED CONCURRENCY
>
> **PROTECT RDS**
> → RESERVED CONCURRENCY
>
> **DATABASE CONNECTION POOL**
> → RDS PROXY
>
> **COLD START**
> → PROVISIONED CONCURRENCY
>
> **PRE-WARM**
> → PROVISIONED CONCURRENCY
>
> **STOP FUNCTION**
> → RESERVED CONCURRENCY = 0
>
> **API RATE LIMIT**
> → API GATEWAY THROTTLING
>
> **WORK BACKLOG**
> → SQS
>
> **LONG FUNCTION**
> → MORE CONCURRENCY CONSUMED

---

## Master Memory Trick

> [!tip] Lambda Concurrency Master Memory Trick
> Imagine a restaurant.
>
> Each active Lambda execution is:
>
> **One cook working at the same time**
>
> Concurrency asks:
>
> **"How many cooks are currently working?"**
>
> **Reserved Concurrency**
>
> tells the manager:
>
> **"This kitchen gets at most 100 cooks, and those spots are reserved for it."**
>
> **Provisioned Concurrency**
>
> tells the manager:
>
> **"Have 20 cooks already standing at their stations."**

So remember:

> **CONCURRENCY**
> → Simultaneous executions
>
> **RESERVED**
> → Reserve + Restrict
>
> **PROVISIONED**
> → Pre-Warm
>
> **RDS PROXY**
> → Pool DB connections
>
> **SQS**
> → Hold excess work
>
> **API GATEWAY THROTTLING**
> → Control incoming requests

And the killer SAA distinction:

> **"Do I need to control SCALE or LATENCY?"**
>
> SCALE
> → **Reserved Concurrency**
>
> LATENCY
> → **Provisioned Concurrency**

---

## Related Notes

- [[Lambda]]
- [[Lambda Synchronous Invocations]]
- [[Lambda Asynchronous Invocations]]
- [[Lambda Event Source Mapping]]
- [[Lambda Execution Roles]]
- [[API Gateway]]
- [[SQS]]
- [[20-SAA/10-Messaging/Kinesis Data Streams]]
- [[04-Databases/DynamoDB]]
- [[RDS]]
- [[RDS Proxy]]