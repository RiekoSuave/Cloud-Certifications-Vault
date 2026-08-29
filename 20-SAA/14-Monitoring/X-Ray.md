## What Problem Does It Solve?

[[X-Ray]] provides:

**Distributed tracing for applications**

It helps developers understand how requests travel through:

**Distributed applications and microservices**

Architecture:

User Request  
↓  
Service A  
↓  
Service B  
↓  
Database  
↓  
Response

X-Ray traces the request across:

**The entire path**

> [!tip] Memory Trick
> **X-Ray = See INSIDE the request**

---

## Core Concept

Modern applications may contain:

- APIs
- Lambda functions
- EC2 instances
- Microservices
- Databases
- Queues
- Downstream services

When something becomes:

**Slow or fails**

it can be difficult to determine:

**Which component caused the problem**

X-Ray helps trace:

**Individual requests across application components**

### Killer Exam Clue

> **Need to trace requests across a distributed application to find latency or errors**
>
> → **X-Ray**

---

# Distributed Tracing

A:

**Distributed Trace**

follows a request as it moves through:

**Multiple application components**

Example:

Client  
↓  
API Gateway  
↓  
Lambda  
↓  
Application Service  
↓  
Database

X-Ray can help identify:

**Where time was spent**

and:

**Where errors occurred**

### Memory Trick

**Trace = Follow the Request**

---

# Traces

A:

**Trace**

represents the complete journey of:

**A request through an application**

A trace contains:

**Segments**

from participating services.

Architecture:

Trace  
↓  
├── Segment A
├── Segment B
└── Segment C

---

# Segments

A:

**Segment**

contains tracing information from:

**A service handling the request**

It can contain information such as:

- Service name
- Request details
- Response details
- Processing time
- Errors
- Faults

### Memory Trick

**Trace = Whole Journey**

**Segment = One Service**

---

# Subsegments

A:

**Subsegment**

provides more detailed information about:

**Work performed inside a segment**

Example:

Application Segment  
↓  
├── DynamoDB Call
├── External API Call
└── Internal Function

### Memory Trick

**Segment = Service**

**Subsegment = Work Inside Service**

---

# Service Map

X-Ray can generate a:

**Service Map**

showing application components and:

**How they communicate**

Example:

Client  
↓  
API Gateway  
↓  
Lambda  
↓  
DynamoDB

The map can help visualize:

- Dependencies
- Latency
- Errors
- Faults
- Service relationships

### Killer Exam Clue

> **Need a visual map of dependencies in a distributed application**
>
> → **X-Ray Service Map**

---

# Latency Analysis

X-Ray helps identify:

**Which service is causing latency**

Example:

API Gateway  
→ 20 ms

Lambda  
→ 100 ms

Database  
→ 2.8 seconds

The likely bottleneck is:

**The database interaction**

### Killer Exam Clue

> **Determine which microservice causes slow requests**
>
> → **X-Ray**

---

# Error Analysis

X-Ray can help investigate:

- Errors
- Faults
- Exceptions
- Failed downstream calls

This makes it useful for:

**Application troubleshooting**

---

# Errors vs Faults

Conceptually:

## Errors

Often represent:

**Client-side or application-level problems**

## Faults

Often represent:

**Server-side failures**

For SAA, the bigger concept is:

> **X-Ray helps locate where failures occur within a distributed request**

---

# Annotations

**Annotations**

are indexed:

**Key-value pairs**

that can be used to:

**Filter and search traces**

Example:

`customerType = premium`

### Killer Exam Concept

> **Need searchable metadata attached to traces**
>
> → **Annotations**

---

# Metadata

**Metadata**

can store additional information in traces.

Unlike annotations:

**Metadata is not indexed for trace filtering**

### Memory Trick

**Annotation = Searchable**

**Metadata = Extra Detail**

---

# Annotations vs Metadata

| Feature | Annotation | Metadata |
|---|---:|---:|
| Key-Value Data | ✅ | ✅ |
| Indexed | ✅ | ❌ |
| Search / Filter Traces | ✅ | ❌ |
| Extra Context | ✅ | ✅ |

### Killer Shortcut

**Need to filter traces by value**
→ Annotation

**Need extra diagnostic information only**
→ Metadata

---

# Sampling

Tracing every request can:

- Generate large amounts of data
- Increase overhead
- Increase cost

X-Ray therefore supports:

**Sampling**

Sampling determines:

**Which requests are recorded**

### Memory Trick

**Sampling = Trace Some, Not Necessarily All**

---

# Sampling Rules

Sampling rules can control:

**Which requests are traced and at what rate**

This allows organizations to balance:

- Visibility
- Performance
- Cost

### Killer Exam Clue

> **Reduce tracing volume while retaining representative request data**
>
> → **X-Ray Sampling**

---

# X-Ray SDK

Applications can use:

**X-Ray instrumentation**

to generate tracing information.

Application code can record:

- Segments
- Subsegments
- Annotations
- Metadata

For SAA, focus on:

**Applications must be instrumented appropriately for detailed tracing**

---

# X-Ray Daemon

In traditional X-Ray architectures, the:

**X-Ray Daemon**

collects trace information from:

**Instrumented applications**

and sends it to:

**X-Ray**

Architecture:

Application  
↓  
X-Ray SDK  
↓  
X-Ray Daemon  
↓  
X-Ray Service

### Memory Trick

**SDK = Creates Trace Data**

**Daemon = Sends Trace Data**

---

# X-Ray + Lambda

[[Lambda]] supports integration with:

**X-Ray**

This can provide tracing for:

**Serverless applications**

Architecture:

API Gateway  
↓  
Lambda  
↓  
DynamoDB

X-Ray can trace:

**The request path**

### Killer Exam Clue

> **Troubleshoot latency across a serverless application**
>
> → **Enable X-Ray tracing**

---

# X-Ray + API Gateway

API Gateway can participate in:

**X-Ray tracing**

This is useful when tracing requests through:

API Gateway  
↓  
Lambda  
↓  
Other Services

---

# X-Ray + EC2

Applications running on:

[[EC2]]

can also use X-Ray when appropriately:

**Instrumented and configured**

This allows tracing across:

**Traditional server-based applications**

---

# X-Ray + ECS

Containerized applications can participate in:

**Distributed tracing**

when configured with appropriate:

**X-Ray instrumentation**

This is useful for:

**Microservice architectures**

---

# X-Ray + Elastic Beanstalk

Applications deployed through:

[[Elastic Beanstalk]]

can use X-Ray to help troubleshoot:

**Application request flows**

---

# X-Ray + CloudWatch

[[CloudWatch]] and X-Ray provide complementary observability.

CloudWatch provides:

- Metrics
- Logs
- Alarms

X-Ray provides:

**Distributed traces**

### Killer Memory Trick

**CloudWatch = What is happening?**

**X-Ray = Where in the request is it happening?**

---

# Metrics vs Logs vs Traces

This distinction is extremely useful for the exam.

## Metrics

Answer:

> **Is something wrong?**

Example:

Latency = 4 seconds

Think:

**CloudWatch Metrics**

---

## Logs

Answer:

> **What did the application say?**

Example:

`Database connection timeout`

Think:

**CloudWatch Logs**

---

## Traces

Answer:

> **Where did the request slow down or fail?**

Think:

**X-Ray**

### Master Shortcut

**METRIC**
→ NUMBER

**LOG**
→ MESSAGE

**TRACE**
→ REQUEST JOURNEY

---

# X-Ray vs CloudWatch

## [[CloudWatch]]

Think:

- Metrics
- Logs
- Alarms
- Dashboards
- Operational monitoring

## X-Ray

Think:

- Distributed tracing
- Request path
- Service map
- Latency analysis
- Application dependencies

### Killer Shortcut

**CPU > 90%**
→ CloudWatch

**Which microservice caused a 4-second request?**
→ X-Ray

---

# X-Ray vs CloudTrail

## [[CloudTrail]]

Think:

**AWS API auditing**

## X-Ray

Think:

**Application request tracing**

### Example

Who deleted an EC2 instance?

→ CloudTrail

Why does checkout take 6 seconds?

→ X-Ray

---

# X-Ray vs Config

## [[Config]]

Think:

**Resource configuration**

## X-Ray

Think:

**Application request path**

### Example

Is an S3 bucket configured publicly?

→ Config

Which service slowed down an application request?

→ X-Ray

---

# X-Ray vs VPC Flow Logs

VPC Flow Logs:

**Network traffic metadata**

X-Ray:

**Application request tracing**

### Memory Trick

**Flow Logs = Network Flow**

**X-Ray = Application Flow**

---

# Permissions

Applications sending trace information require:

**Appropriate IAM permissions**

to submit:

**Tracing data**

Follow:

**Least privilege**

---

# Architecture Thinking

## Scenario 1 — Slow Checkout

Application architecture:

API Gateway  
↓  
Lambda  
↓  
Payment Service  
↓  
Database

Customers report:

**Checkout takes 8 seconds**

Need to determine:

**Which component is slow**

Choose:

**X-Ray**

---

## Scenario 2 — High CPU

EC2 CPU reaches:

95%.

Need monitoring and alerting.

Choose:

**CloudWatch**

not X-Ray.

---

## Scenario 3 — Who Changed Lambda?

Need to determine:

**Who modified a Lambda configuration**

Choose:

**CloudTrail**

not X-Ray.

---

## Scenario 4 — Serverless Latency

Application uses:

API Gateway  
↓  
Lambda  
↓  
DynamoDB

Need request-level latency tracing.

Choose:

**X-Ray**

---

## Scenario 5 — Microservice Dependencies

Company has:

30 microservices.

Need to visualize:

**Which services communicate with each other**

Choose:

**X-Ray Service Map**

---

## Scenario 6 — Search Traces by Customer Type

Need to filter traces using:

`customerType = premium`

Choose:

**Annotation**

---

## Scenario 7 — Diagnostic Information

Need to attach additional debugging information but do NOT need to:

**Search traces using it**

Choose:

**Metadata**

---

## Scenario 8 — Too Much Trace Data

Application handles:

Millions of requests.

Need to reduce:

**Tracing volume**

Choose:

**Sampling**

---

# Scenario Recognition

Immediately think:

**X-Ray**

when you see:

- Distributed tracing
- Request tracing
- Microservices
- Service dependencies
- Service map
- Request latency
- Trace
- Segment
- Subsegment
- Sampling

---

## Think Service Map When You See

- Visual application dependencies
- Microservice relationships
- Request flow visualization

---

## Think Annotation When You See

- Searchable trace attribute
- Filter traces
- Indexed tracing information

---

## Think Sampling When You See

- Reduce tracing volume
- Trace subset of requests
- Control tracing cost

---

# Exam Traps

## Trap 1 — X-Ray Is Primarily for Infrastructure Metrics

❌

Think:

**CloudWatch**

X-Ray focuses on:

**Distributed application tracing**

---

## Trap 2 — X-Ray Tells You Who Changed an AWS Resource

❌

Think:

**CloudTrail**

---

## Trap 3 — X-Ray Tracks Resource Compliance

❌

Think:

**Config**

---

## Trap 4 — Annotation and Metadata Are Identical

❌

Annotations:

**Indexed / searchable**

Metadata:

**Not indexed**

---

## Trap 5 — X-Ray Must Trace Every Request

❌

Use:

**Sampling**

---

## Trap 6 — A Segment Represents the Entire Distributed Request

❌

Trace:

**Entire request**

Segment:

**One service**

---

## Trap 7 — CloudWatch Logs and X-Ray Provide the Same Information

❌

Logs:

**Messages**

X-Ray:

**Request journey**

---

# Quick Cheat Sheet

| Exam Clue | Answer |
|---|---|
| Distributed Tracing | X-Ray |
| Request Journey | Trace |
| One Service in Trace | Segment |
| Work Inside Segment | Subsegment |
| Visual Dependencies | Service Map |
| Find Request Latency | X-Ray |
| Searchable Trace Data | Annotation |
| Non-Indexed Trace Data | Metadata |
| Reduce Trace Volume | Sampling |
| Infrastructure Metrics | CloudWatch |
| Application Logs | CloudWatch Logs |
| AWS API Audit | CloudTrail |
| Resource Compliance | Config |

---

# Observability Decision Map

Need:

**CPU / latency metric**

→ CloudWatch Metrics

Need:

**Application messages**

→ CloudWatch Logs

Need:

**Request path across services**

→ X-Ray

Need:

**Who changed AWS resource**

→ CloudTrail

Need:

**Resource configuration**

→ Config

---

# The Observability Trio

| Data Type | Think |
|---|---|
| Metrics | [[CloudWatch]] |
| Logs | [[CloudWatch]] |
| Traces | X-Ray |

### Memory Trick

> **METRICS**
> → HOW MUCH?
>
> **LOGS**
> → WHAT HAPPENED?
>
> **TRACES**
> → WHERE DID THE REQUEST GO?

---

# Final Exam Rapid-Fire

> **DISTRIBUTED TRACING**
> → X-RAY
>
> **REQUEST JOURNEY**
> → TRACE
>
> **ONE SERVICE**
> → SEGMENT
>
> **WORK INSIDE SERVICE**
> → SUBSEGMENT
>
> **DEPENDENCY MAP**
> → SERVICE MAP
>
> **SEARCHABLE TRACE ATTRIBUTE**
> → ANNOTATION
>
> **EXTRA TRACE DETAIL**
> → METADATA
>
> **REDUCE TRACE VOLUME**
> → SAMPLING
>
> **METRICS**
> → CLOUDWATCH
>
> **LOGS**
> → CLOUDWATCH LOGS
>
> **WHO DID IT**
> → CLOUDTRAIL
>
> **RESOURCE CONFIGURATION**
> → CONFIG

---

## Master Memory Trick

> [!tip] X-Ray Master Memory Trick
> Imagine a customer clicks:
>
> **BUY NOW**
>
> The request disappears into a giant AWS application:
>
> API Gateway  
> ↓  
> Lambda  
> ↓  
> Payment Service  
> ↓  
> Database
>
> The customer waits:
>
> **8 seconds**
>
> CloudWatch tells you:
>
> **"Yep, latency is high."**
>
> But you ask:
>
> **"WHERE are those 8 seconds being spent?"**
>
> X-Ray puts on:
>
> **X-RAY GOGGLES**
>
> and follows the request through every service.
>
> It discovers:
>
> API Gateway → 20 ms  
> Lambda → 100 ms  
> Payment Service → 200 ms  
> Database → **7.6 seconds**
>
> Now you know:
>
> **WHERE THE PROBLEM IS**

So remember:

> **CLOUDWATCH**
> → SOMETHING IS WRONG
>
> **LOGS**
> → HERE'S WHAT THE APP SAID
>
> **X-RAY**
> → HERE'S WHERE THE REQUEST WENT
>
> **CLOUDTRAIL**
> → HERE'S WHO CHANGED AWS
>
> **CONFIG**
> → HERE'S HOW THE RESOURCE IS CONFIGURED

And the killer SAA question:

> **"Does the question ask you to trace a request across multiple services to locate latency, errors, or dependencies?"**
>
> YES
>
> → **X-Ray**

---

## Related Notes

- [[CloudWatch]]
- [[CloudTrail]]
- [[Config]]
- [[Lambda]]
- [[API Gateway]]
- [[EC2]]
- [[ECS]]
- [[Elastic Beanstalk]]
- [[DynamoDB]]
- [[IAM]]