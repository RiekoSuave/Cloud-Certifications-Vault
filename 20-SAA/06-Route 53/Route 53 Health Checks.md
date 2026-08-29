## What Problem Does It Solve?

[[Route 53 Health Checks]] let Route 53 determine whether an endpoint or application is **healthy enough to receive DNS traffic**.

They solve the problem of:

> **"Should Route 53 keep returning this resource, or should it fail traffic over somewhere else?"**

Health checks are a major part of **automated DNS failover**.

Think:

Resource  
↓  
[[Route 53 Health Checks]]  
↓  
Healthy?  
├── Yes → Can be returned in DNS  
└── No → Avoid / Fail Over

> [!tip] Memory Trick
> **Health Check = Can Route 53 trust this endpoint?**

---

## Core Health Check Types

Route 53 supports three important health check patterns:

1. **Endpoint Health Checks**
2. **Calculated Health Checks**
3. **CloudWatch Alarm Health Checks**

These solve different architecture problems.

---

## 1. Endpoint Health Checks

An Endpoint Health Check directly monitors a resource such as:

- Application
- Server
- Public AWS resource
- Public endpoint

Important:

**HTTP Route 53 health checks are for public resources.**

Route 53 health checkers operate from outside your VPC.

So they must be able to reach the endpoint over the network.

---

## Endpoint Health Check Architecture

Example:

Global Route 53 Health Checkers  
↓  
HTTP / HTTPS / TCP  
↓  
Public Endpoint  
↓  
Healthy or Unhealthy

Route 53 uses health checkers from multiple global locations to evaluate the endpoint.

The SAA slides describe roughly:

**15 global health checkers**

checking endpoint health.

---

## Supported Health Check Protocols

Route 53 Endpoint Health Checks support:

- HTTP
- HTTPS
- TCP

Example:

Health Checker  
↓ HTTP GET  
/health  
↓  
Application

The application response determines whether the endpoint passes the health check.

---

## HTTP Status Codes

For HTTP and HTTPS health checks, Route 53 considers the check successful when the endpoint responds with:

**2xx or 3xx status codes**

Examples:

200 OK → Healthy

301 Redirect → Healthy

404 Not Found → Unhealthy

500 Server Error → Unhealthy

### Memory Trick

**2xx / 3xx = Good**

**4xx / 5xx = Bad**

---

## Health Check Intervals

The default health check interval is:

**30 seconds**

You can configure:

**10-second health checks**

but the faster interval has a higher cost.

### Architecture Thinking

30 seconds:

- Lower cost
- Standard monitoring

10 seconds:

- Faster detection
- Higher cost

> [!tip] Memory Trick
> **Faster health checking costs more.**

---

## Healthy / Unhealthy Threshold

The default threshold is:

**3 consecutive checks**

before changing the endpoint's health state.

This reduces the chance that one temporary network error immediately causes failover.

Think:

Failure  
↓  
Failure  
↓  
Failure  
↓  
Endpoint marked unhealthy

---

## Global Health Checker Consensus

Route 53 uses multiple health checkers around the world.

The SAA slides state:

If more than **18% of health checkers** report the endpoint as healthy, Route 53 considers the endpoint healthy.

Otherwise:

**Unhealthy**

The exact percentage is less important than the architecture lesson:

> Route 53 uses multiple distributed health checkers rather than trusting a single probe.

---

## Choose Health Checker Locations

You can select which locations Route 53 uses to perform health checks.

This can be useful if you care about reachability from specific parts of the world.

Example:

North America Health Checker  
Europe Health Checker  
South America Health Checker  
↓  
Application Endpoint

---

## Response String Matching

Route 53 Health Checks can do more than just look at HTTP status codes.

They can also inspect the response body.

Route 53 can search the first:

**5120 bytes**

of the response for specific text.

Example:

GET /health

Application returns:

Application Healthy

Route 53 can check for the expected string.

### Why This Matters

An endpoint might return:

200 OK

while the application itself is not truly functioning correctly.

Content checking gives you a deeper application-level health signal.

---

## Firewall and Security Group Requirement

Your endpoint must allow incoming connections from:

**Route 53 Health Checker IP address ranges**

Otherwise:

Route 53 Health Checker  
↓  
Firewall blocks request  
↓  
Health check fails

even though the application itself may actually be healthy.

### Exam Trap

If a public endpoint works for users but Route 53 Health Checks consistently fail:

Check whether:

**Security Groups / firewalls allow Route 53 health checker traffic**

---

## Health Checks and Automated DNS Failover

Health checks integrate with:

[[Route 53 Routing Policies]]

Route 53 can avoid returning unhealthy resources.

Architecture:

Client  
↓ DNS Query  
[[Route 53]]  
↓  
Check Resource Health  
↓  
Return Healthy Endpoint  
↓  
Client Connects

This enables:

**Automated DNS Failover**

---

## 2. Calculated Health Checks

[[Route 53 Calculated Health Checks]] combine the results of multiple individual health checks into:

**One parent health check**

Example:

Child Health Check A  
Child Health Check B  
Child Health Check C  
↓  
Calculated Parent Health Check

The parent health check determines overall application health.

---

## Calculated Health Check Logic

Calculated Health Checks support:

- AND
- OR
- NOT

This lets you create more advanced health logic.

### AND

All required child checks must be healthy.

Example:

Web Server Healthy  
AND  
Database Healthy

↓

Application Healthy

---

### OR

One of several health checks can be enough.

Example:

Server A Healthy  
OR  
Server B Healthy

↓

Service Healthy

---

### NOT

You can invert the result of another health check.

This gives more flexibility when building health logic.

---

## Child Health Check Limit

A Calculated Health Check can monitor up to:

**256 child health checks**

You can also configure:

> How many child health checks must pass before the parent is considered healthy?

Example:

10 child health checks

Requirement:

At least 7 must be healthy

↓  

Parent = Healthy

---

## Calculated Health Check Use Case — Maintenance

The Maarek slides specifically highlight maintenance as a use case.

Suppose you have:

Server A  
Server B  
Server C

You need to take Server C down for maintenance.

If your health logic is designed properly, taking one server offline does not automatically make the entire application appear unhealthy.

### Architecture Thinking

Calculated Health Checks let you define:

> **"How much failure is acceptable before the whole application is considered unhealthy?"**

---

## 3. CloudWatch Alarm Health Checks

Route 53 can create a health check that monitors:

[[CloudWatch Alarms]]

This is extremely useful because CloudWatch can monitor things that Route 53's public health checkers cannot directly reach.

Examples from the SAA slides include:

- [[04-Databases/DynamoDB]] throttles
- [[RDS]] alarms
- Custom metrics
- Other CloudWatch-monitored conditions

Architecture:

Resource / Application  
↓  
[[07-Monitoring/CloudWatch]] Metric  
↓  
[[CloudWatch Alarm]]  
↓  
[[Route 53 Health Checks]]  
↓  
DNS Routing Decision

> [!tip] Memory Trick
> **Can't probe it directly? Monitor it with CloudWatch.**

---

## Health Checks for Private Resources

This is a major SAA exam concept.

Route 53 Health Checkers are:

**Outside your VPC**

Therefore, they cannot directly access:

- Private EC2 endpoints
- Private VPC resources
- Private internal load balancers
- On-premises private resources

Example:

Route 53 Health Checker  
↓  
Internet  
X  
Private Subnet

The health checker cannot directly reach the private endpoint.

---

## Monitoring Private Endpoints

For private resources, use:

[[07-Monitoring/CloudWatch]]

Architecture:

Private Resource  
↓  
[[07-Monitoring/CloudWatch]] Metric  
↓  
[[CloudWatch Alarm]]  
↓  
Route 53 Health Check monitors Alarm  
↓  
DNS Failover Decision

This gives Route 53 an indirect way to determine whether the private resource is healthy.

### Master Private Resource Rule

> **Public endpoint → Route 53 can check directly**
>
> **Private endpoint → CloudWatch Alarm → Route 53 Health Check**

---

## Architecture Thinking

### Scenario 1 — Public Website Health

A public web server is reachable over HTTPS.

Route 53 should stop returning it if the application becomes unhealthy.

**Choose → Route 53 Endpoint Health Check**

Protocol:

HTTPS

---

### Scenario 2 — Primary Region Failure

A company has:

Primary Region  
Secondary Region

Route 53 should automatically switch to the secondary Region when the primary application's health check fails.

Architecture:

Primary  
↓  
[[Route 53 Health Checks]]  
↓ unhealthy  
[[Route 53 Failover Routing]]  
↓  
Secondary

---

### Scenario 3 — Private RDS Database

A database is inside a private subnet.

Route 53 health checkers cannot directly connect to it.

The company still wants DNS failover based on database health.

**Choose → CloudWatch Metric + CloudWatch Alarm + Route 53 Health Check**

---

### Scenario 4 — DynamoDB Throttling

A company wants DNS failover if an application's [[04-Databases/DynamoDB]] table begins experiencing excessive throttling.

Route 53 cannot perform an HTTP check against DynamoDB throttling.

Instead:

[[04-Databases/DynamoDB]] Metric  
↓  
[[CloudWatch Alarm]]  
↓  
[[Route 53 Health Checks]]

---

### Scenario 5 — Multiple Components Determine Health

An application consists of several critical components.

The application should be considered healthy only if enough components are healthy.

**Choose → Calculated Health Check**

---

## Endpoint vs Calculated vs CloudWatch

| Requirement | Health Check Type |
|---|---|
| Public HTTP endpoint | Endpoint |
| Public HTTPS endpoint | Endpoint |
| TCP endpoint | Endpoint |
| Combine several checks | Calculated |
| AND / OR / NOT logic | Calculated |
| Private resource | CloudWatch Alarm |
| RDS metric | CloudWatch Alarm |
| DynamoDB throttling | CloudWatch Alarm |
| Custom metric | CloudWatch Alarm |

---

## Route 53 Health Checks vs ELB Health Checks

These solve similar-looking but different problems.

### Route 53 Health Checks

Operate at:

**DNS level**

Purpose:

Determine whether Route 53 should return an endpoint.

---

### [[Elastic Load Balancing]] Health Checks

Operate inside the load balancer architecture.

Purpose:

Determine which backend targets should receive traffic.

Example:

[[Route 53]]  
↓  
[[Application Load Balancer]]  
↓  
EC2 A  
EC2 B  
EC2 C

Route 53 might check:

**Is the ALB endpoint healthy?**

The ALB checks:

**Which EC2 instances behind me are healthy?**

### Memory Trick

**Route 53 Health Check = Endpoint health**

**ELB Health Check = Target health**

---

## Health Checks and TTL

Health checks do not eliminate DNS caching.

Even if Route 53 stops returning an unhealthy endpoint, clients may temporarily retain previous DNS answers according to:

[[Route 53 TTL]]

Therefore:

Health Detection  
↓  
Route 53 changes DNS response  
↓  
Existing cached records may remain temporarily

This is an important architectural limitation of DNS-based failover.

---

## Scenario Recognition

### Immediately Think Route 53 Health Checks When You See

- Automated DNS failover
- Endpoint health
- Primary / secondary
- Remove unhealthy DNS destination
- HTTP health check
- HTTPS health check
- TCP health check
- Calculated health
- CloudWatch alarm + DNS
- Private endpoint health
- Multiple child health checks

### Strong Exam Pattern

**Private endpoint + Route 53 health → CloudWatch Alarm**

---

## Exam Traps

### Trap 1 — Route 53 HTTP Health Checks Can Directly Reach Private Endpoints

False.

Route 53 health checkers are outside the VPC.

They cannot directly access private VPC resources.

Use:

**CloudWatch Metric → CloudWatch Alarm → Route 53 Health Check**

---

### Trap 2 — 404 Means Healthy Because the Server Responded

False.

HTTP/HTTPS health checks pass for:

**2xx and 3xx**

4xx and 5xx responses fail.

---

### Trap 3 — Firewall Rules Don't Matter

False.

Your endpoint must allow requests from Route 53 Health Checker IP ranges.

Otherwise health checks fail.

---

### Trap 4 — Calculated Health Check Monitors an Endpoint Directly

Not necessarily.

Calculated Health Checks combine:

**Other Health Checks**

into a parent result.

---

### Trap 5 — Route 53 Health Checks Replace ELB Health Checks

False.

They operate at different levels.

**Route 53 → DNS endpoint health**

**ELB → Backend target health**

---

### Trap 6 — Faster Health Checks Are Free

False.

The 10-second interval costs more than the standard 30-second interval.

---

## Quick Cheat Sheet

| Feature | Route 53 Health Checks |
|---|---|
| Primary Purpose | Automated DNS failover |
| Direct HTTP Checks | Public Resources |
| HTTP | ✅ |
| HTTPS | ✅ |
| TCP | ✅ |
| Default Interval | 30 sec |
| Fast Interval | 10 sec |
| 10-sec Higher Cost | ✅ |
| Default Threshold | 3 |
| HTTP Success Codes | 2xx / 3xx |
| Response String Check | First 5120 bytes |
| Global Health Checkers | ✅ |
| Calculated Health Checks | ✅ |
| Child Checks | Up to 256 |
| AND / OR / NOT | ✅ |
| CloudWatch Alarm Checks | ✅ |
| Direct Private Resource Check | ❌ |
| Private Resource via CloudWatch | ✅ |

---

## Master Memory Trick

> [!tip] Master Memory Trick
> **Route 53 Health Checks = DNS Gatekeeper**
>
> Before Route 53 sends users somewhere, ask:
>
> **"Is that endpoint healthy?"**

Remember the three types:

**Endpoint = Check it directly**

**Calculated = Combine checks**

**CloudWatch = Check what Route 53 can't directly see**

And the biggest exam rule:

> **Public → Direct Health Check**
>
> **Private → CloudWatch Alarm**

---

## Related Notes

- [[Route 53]]
- [[Route 53 Routing Policies]]
- [[Route 53 Failover Routing]]
- [[Route 53 Latency Routing]]
- [[Route 53 Weighted Routing]]
- [[Route 53 IP-Based Routing]]
- [[Route 53 TTL]]
- [[07-Monitoring/CloudWatch]]
- [[CloudWatch Alarms]]
- [[Application Load Balancer]]
- [[Elastic Load Balancing]]
- [[04-Databases/DynamoDB]]
- [[RDS]]
- [[05-Networking/VPC]]