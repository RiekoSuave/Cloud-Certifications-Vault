## Purpose

Use this note:

**The night before and day of the SAA exam**

This is NOT another study guide.

It is a checklist for:

- Final preparation
- Exam strategy
- Time management
- Avoiding careless mistakes

> [!tip] Memory Trick
> **Prepare → Recognize → Eliminate → Choose → Move**

---

# Night Before

- [ ] Confirm exam date and time
- [ ] Confirm testing location or online testing requirements
- [ ] Confirm required identification
- [ ] Confirm transportation if testing in person
- [ ] Set alarms
- [ ] Charge necessary devices
- [ ] Prepare testing area if taking exam online
- [ ] Avoid trying to relearn the entire SAA course

### Final Study Priority

Review:

1. [[SAA Weak Areas Tracker]]
2. [[SAA Exam Traps]]
3. [[SAA Scenario Recognition Cheat Sheet]]
4. [[SAA Final Review Cheat Sheet]]

Focus on:

**Recognition**

not:

**Cramming new material**

---

# Final Weak-Area Check

Before stopping for the night, review:

## 🔴 High Priority

- [ ] Weak Area 1
- [ ] Weak Area 2
- [ ] Weak Area 3

## Most-Missed Comparisons

- [ ] Multi-AZ vs Read Replica
- [ ] SQS vs SNS vs EventBridge
- [ ] CloudFront vs Global Accelerator
- [ ] Security Group vs NACL
- [ ] Peering vs Transit Gateway vs PrivateLink
- [ ] VPN vs Direct Connect
- [ ] CloudWatch vs CloudTrail vs Config
- [ ] GuardDuty vs Inspector vs Macie
- [ ] RPO vs RTO
- [ ] Pilot Light vs Warm Standby vs Multi-Site

---

# Morning of Exam

- [ ] Wake up with enough time
- [ ] Eat something
- [ ] Hydrate
- [ ] Avoid excessive last-minute studying
- [ ] Review only short cheat sheets
- [ ] Arrive / check in early

### Killer Rule

> **Do not walk into the exam mentally exhausted from cramming**

---

# Before Starting

Remind yourself:

> **I do not need to know every AWS fact.**
>
> **I need to recognize the architecture being tested.**

For each question:

**Requirement**  
↓  
**Clue**  
↓  
**Pattern**  
↓  
**Eliminate**  
↓  
**Answer**

---

# First Question to Ask

Before looking for a service:

> **What problem is AWS asking me to solve?**

Examples:

- Availability?
- Scaling?
- Performance?
- Security?
- Cost?
- Decoupling?
- Networking?
- Disaster recovery?
- Operational overhead?

### Killer Exam Rule

**Problem first. Service second.**

---

# Find the Optimization Word

Look carefully for:

- MOST cost-effective
- LEAST operational overhead
- MOST resilient
- MOST secure
- LOWEST latency
- MINIMUM changes

These words determine:

**Which technically valid answer is best**

---

# Find the Failure Domain

If failure is involved, ask:

**What can fail?**

Instance  
→ Replace instance

AZ  
→ Multi-AZ

Region  
→ Multi-Region

### Memory Trick

> **Match redundancy to the failure domain**

---

# Find the Bottleneck

If performance is involved, ask:

**What is overloaded?**

Compute  
→ Scale compute

Database reads  
→ Read Replica / Cache

Backend workers  
→ SQS + scale workers

Static origin  
→ CloudFront

Repeated database queries  
→ Cache

### Killer Rule

> **Scale the bottleneck — not everything**

---

# Read Every Word of the Requirement

Watch for phrases such as:

**without modifying the application**

**without downtime**

**private connectivity**

**least operational overhead**

**most cost-effective**

**must preserve order**

**must survive Region failure**

One phrase can eliminate:

**Most answer choices**

---

# Eliminate Before Selecting

For each answer ask:

> **What is wrong with this architecture?**

Look for:

- Impossible AWS behavior
- Wrong service purpose
- Missing availability
- Wrong failure domain
- Public connectivity when private is required
- Excessive cost
- Excessive management
- Wrong RPO/RTO
- Unnecessary complexity

### Memory Trick

> **Find the Fatal Flaw**

---

# Classic Fatal Flaws

Security Group explicit deny  
→ ❌

VPC Peering transitive routing  
→ ❌

Multi-AZ for read scaling  
→ ❌

NAT Gateway in private subnet for public Internet egress  
→ ❌

Spot-only architecture for non-interruptible workload  
→ ❌

Single-AZ architecture when AZ failure must be tolerated  
→ ❌

Pilot Light described as full application stack running  
→ ❌

Direct Connect assumed encrypted by default  
→ ❌

---

# Two Answers Both Look Correct

Do NOT panic.

Ask:

> **What exact requirement separates them?**

Then check:

Cost  
→ Which is cheaper while still correct?

Operations  
→ Which requires less management?

Availability  
→ Which survives the required failure?

Performance  
→ Which solves the actual bottleneck?

Security  
→ Which satisfies the specific security requirement?

### Killer Rule

> **The optimization word breaks the tie**

---

# Service Recognition Rapid-Fire

**High Availability**
→ Multi-AZ

**Read Scaling**
→ Read Replica

**Repeated Reads**
→ Cache

**Buffer**
→ SQS

**Fan-Out**
→ SNS

**Event Routing**
→ EventBridge

**Workflow**
→ Step Functions

**Global Cache**
→ CloudFront

**Network Acceleration**
→ Global Accelerator

**Object Storage**
→ S3

**Block Storage**
→ EBS

**Shared Linux Files**
→ EFS

**Relational**
→ RDS / Aurora

**NoSQL**
→ DynamoDB

**Private S3**
→ Gateway Endpoint

**Two VPCs**
→ Peering

**Many VPCs**
→ Transit Gateway

**One Private Service**
→ PrivateLink

**Quick Hybrid**
→ Site-to-Site VPN

**Dedicated Hybrid**
→ Direct Connect

**Remote User**
→ Client VPN

**Explicit Deny**
→ NACL

**Encryption Keys**
→ KMS

**Secrets**
→ Secrets Manager

**SQL Injection**
→ WAF

**DDoS**
→ Shield

**Threat**
→ GuardDuty

**Vulnerability**
→ Inspector

**PII**
→ Macie

**API Audit**
→ CloudTrail

**Monitoring**
→ CloudWatch

**Data Loss**
→ RPO

**Downtime**
→ RTO

---

# DR Rapid-Fire

Backup only  
→ Backup and Restore

Core running  
→ Pilot Light

Full stack small  
→ Warm Standby

Full stack full  
→ Multi-Site

### Memory Trick

> **BACKUP**
> → BUILD
>
> **PILOT**
> → START
>
> **WARM**
> → SCALE
>
> **MULTI-SITE**
> → ROUTE

---

# Messaging Rapid-Fire

Need:

**Hold work**

→ SQS

Need:

**Send to many**

→ SNS

Need:

**Send to many + preserve independently**

→ SNS + SQS

Need:

**Route events**

→ EventBridge

Need:

**Coordinate steps**

→ Step Functions

Need:

**Strict message order**

→ FIFO

Need:

**Failed messages**

→ DLQ

---

# Networking Rapid-Fire

Internet  
→ IGW

Private IPv4 outbound Internet  
→ NAT Gateway

Private S3 / DynamoDB  
→ Gateway Endpoint

Private supported AWS service  
→ Interface Endpoint

Two VPCs  
→ Peering

Many VPCs  
→ Transit Gateway

One service  
→ PrivateLink

On-prem network quickly  
→ VPN

Dedicated on-prem connection  
→ Direct Connect

Remote employee  
→ Client VPN

Hybrid DNS  
→ Route 53 Resolver

---

# Security Rapid-Fire

AWS Permissions  
→ IAM

Temporary Credentials  
→ STS

Encryption Keys  
→ KMS

Secrets + Rotation  
→ Secrets Manager

TLS Certificate  
→ ACM

Web Attacks  
→ WAF

DDoS  
→ Shield

Threat Detection  
→ GuardDuty

Vulnerabilities  
→ Inspector

Sensitive S3 Data  
→ Macie

Security Findings  
→ Security Hub

Configuration Compliance  
→ Config

API Activity  
→ CloudTrail

---

# Don't Overthink Simple Questions

Sometimes:

**S3 means S3**

Not every question contains:

**A hidden trick**

If one answer clearly satisfies every requirement:

**Do not invent a reason it must be wrong**

---

# Don't Choose the Coolest Service

The newest or most advanced service is not automatically:

**The correct answer**

Choose based on:

**Requirements**

not:

**How impressive the architecture sounds**

---

# Don't Overengineer

If:

**Two services solve the requirement**

do not automatically choose:

**Six services**

### Killer Rule

> **Simple + Correct Beats Complex + Correct**

especially when the question asks for:

**Least operational overhead**

---

# Flagging Strategy

Flag a question when:

- Two answers remain plausible
- You cannot remember an important AWS limitation
- The scenario requires lengthy reasoning

Do NOT flag simply because:

**The question looks long**

---

# When Stuck

Use this sequence:

1. What is being tested?
2. What is the primary requirement?
3. What is the optimization word?
4. What is the failure domain?
5. What is the bottleneck?
6. Which answers contain impossible AWS behavior?
7. Which answer requires unnecessary complexity?
8. Which remaining answer best satisfies everything?

---

# Do Not Let One Question Drain Time

If you are stuck:

**Make the best decision**

Flag it.

Move on.

Return later.

### Killer Rule

> **One difficult question is worth the same as one easier question**

---

# Guessed Answers

If forced to guess:

First eliminate:

**Anything clearly impossible**

Then choose between:

**The remaining plausible answers**

Never leave reasoning at:

**"I recognize this service name."**

---

# Changing Answers

Do not change an answer merely because:

**You feel nervous about it**

Change it when you identify:

**A concrete reason the original answer violates the requirements**

### Memory Trick

> **New Evidence → Change**
>
> **Nerves → Don't**

---

# Final Review Before Submission

If time remains:

Review:

1. Flagged questions
2. Questions where two answers were close
3. Questions containing MOST / LEAST
4. Questions involving RPO/RTO
5. Networking questions with directionality

Do NOT randomly change:

**Previously confident answers**

---

# Final Mental Checklist

Before selecting an answer:

- [ ] Does it actually work?
- [ ] Does it satisfy the primary requirement?
- [ ] Does it meet availability requirements?
- [ ] Does it meet security requirements?
- [ ] Does it meet performance requirements?
- [ ] Does it meet RPO/RTO?
- [ ] Does it match the optimization word?
- [ ] Is there a simpler correct solution?

---

# Final 30-Second Memory Dump

> **MULTI-AZ**
> → SURVIVE
>
> **READ REPLICA**
> → READ
>
> **CACHE**
> → REPEAT
>
> **SQS**
> → HOLD
>
> **SNS**
> → BROADCAST
>
> **EVENTBRIDGE**
> → ROUTE
>
> **STEP FUNCTIONS**
> → ORCHESTRATE
>
> **CLOUDFRONT**
> → CACHE GLOBAL
>
> **PEERING**
> → TWO
>
> **TGW**
> → MANY
>
> **PRIVATELINK**
> → SERVICE
>
> **VPN**
> → QUICK
>
> **DX**
> → DEDICATED
>
> **SG**
> → STATEFUL
>
> **NACL**
> → STATELESS + DENY
>
> **CLOUDTRAIL**
> → WHO
>
> **CLOUDWATCH**
> → HOW
>
> **RPO**
> → DATA
>
> **RTO**
> → TIME

---

## Master Memory Trick

> [!tip] Exam Day Master Memory Trick
> You have already studied:
>
> **The services**
>
> Exam day is about:
>
> **Recognizing the problem**
>
> So when you see a long scenario:
>
> **DON'T CHASE EVERY DETAIL**
>
> Find:
>
> **THE REQUIREMENT**
>
> Then:
>
> **THE CLUE**
>
> Then:
>
> **THE PATTERN**
>
> Then:
>
> **THE FATAL FLAW**
>
> Then:
>
> **THE BEST ANSWER**

Remember:

> **REQUIREMENT**
> → WHAT MUST HAPPEN?
>
> **BOTTLENECK**
> → WHAT IS STRUGGLING?
>
> **FAILURE DOMAIN**
> → WHAT MUST SURVIVE?
>
> **OPTIMIZATION**
> → WHAT DOES MOST / LEAST REFER TO?
>
> **ELIMINATION**
> → WHAT CANNOT WORK?
>
> **DECISION**
> → WHAT IS THE SIMPLEST CORRECT DESIGN?

Final rule:

> **Don't ask which answer sounds the most AWS-like.**
>
> Ask:
>
> **Which answer satisfies every requirement with the fewest compromises?**

---

## Related Notes

- [[SAA Weak Areas Tracker]]
- [[SAA Practice Exam Review Template]]
- [[SAA Exam Strategy]]
- [[SAA Exam Traps]]
- [[SAA Scenario Recognition Cheat Sheet]]
- [[SAA Final Review Cheat Sheet]]
- [[18-Architecture Cheat Sheet]]