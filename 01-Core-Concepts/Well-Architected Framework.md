## Overview

The AWS Well-Architected Framework helps you:

**Build secure, high-performing, resilient, efficient, and sustainable cloud architectures**

It provides:

- General architectural principles
- Cloud design best practices
- Six architectural pillars
- A framework for reviewing workloads

The six pillars are:

1. **Operational Excellence**
2. **Security**
3. **Reliability**
4. **Performance Efficiency**
5. **Cost Optimization**
6. **Sustainability**

> [!tip] Memory Trick
> **O-S-R-P-C-S**
>
> **O**perational Excellence  
> **S**ecurity  
> **R**eliability  
> **P**erformance Efficiency  
> **C**ost Optimization  
> **S**ustainability

---

## General Guiding Principles

The course highlights several general principles for good AWS architecture.

### Stop Guessing Capacity

Do not permanently provision resources based on:

**What you think future demand might be**

Instead:

**Measure demand and adjust capacity**

### Exam Clue

> **Avoid overprovisioning and underprovisioning**
>
> → Stop Guessing Capacity

---

### Test Systems at Production Scale

Cloud environments make it easier to:

**Test workloads at realistic production scale**

This helps reveal:

- Performance issues
- Scaling limits
- Failure conditions

before:

**Real production traffic exposes them**

---

### Automate Architectural Experimentation

Use automation to make:

**Infrastructure experimentation easier**

Instead of manually rebuilding environments:

**Automate provisioning and changes**

---

### Allow for Evolutionary Architectures

Applications and requirements change over time.

Architectures should therefore be able to:

**Evolve**

rather than remain:

**Rigid**

### Memory Trick

> **Cloud Architecture Is Never "Finished"**

---

### Drive Architecture Using Data

Architecture decisions should be based on:

**Measured information**

rather than:

**Guesswork**

Examples may include:

- Performance
- Reliability
- Capacity
- Cost

---

### Improve Through Game Days

A:

**Game Day**

simulates events or failures so teams can:

**Practice how systems and people respond**

Example:

Simulate:

**Flash-sale traffic**

to test:

- Scaling
- Monitoring
- Operations

### Killer Exam Clue

> **Simulate failures or extreme production events to improve architecture**
>
> → **Game Day**

---

## AWS Cloud Design Principles

The course highlights several broader AWS architecture best practices.

---

## Scalability

Architectures should support:

**Vertical and horizontal scaling**

### Vertical Scaling

Increase:

**The size of a resource**

### Horizontal Scaling

Increase:

**The number of resources**

### Memory Trick

> **VERTICAL**
> → BIGGER
>
> **HORIZONTAL**
> → MORE

---

## Disposable Resources

Servers should be:

**Disposable and easily configurable**

Instead of treating one server as:

**A permanent unique machine**

architecture should allow resources to be:

- Recreated
- Replaced
- Automated

### Killer Exam Principle

> **Cloud resources should be replaceable**

---

## Automation

AWS architecture should make use of:

**Automation**

Examples from the course include:

- Serverless
- Infrastructure as a Service
- Auto Scaling

### Core Idea

> **Automate repeatable infrastructure tasks whenever possible**

---

## Loose Coupling

Applications should be broken into:

**Smaller loosely coupled components**

instead of growing into:

**Large monolithic applications**

### Why?

A change or failure in one component should not:

**Cascade into other components**

### Architecture

Tightly Coupled:

Component A  
↓  
Component B  
↓  
Component C  
↓  
One Failure Can Spread

Loosely Coupled:

Component A  
↔  
Component B  
↔  
Component C

Each component can fail or change with:

**Less impact on the others**

### Killer Exam Clue

> **Failure in one component should not cascade throughout the application**
>
> → **Loose Coupling**

---

## Services, Not Servers

The course emphasizes:

**Do not think only in terms of EC2 servers**

AWS provides:

- Managed services
- Managed databases
- Serverless services

These can reduce:

**Infrastructure management**

### Memory Trick

> **Don't Ask "Which Server?"**
>
> Ask:
>
> **"Is There a Managed AWS Service?"**

---

# The Six Pillars

The Well-Architected Framework contains:

**Six Pillars**

The course emphasizes that these are:

**A synergy**

rather than simply:

**Trade-offs to balance against one another**

---

# 1. Operational Excellence

Operational Excellence includes the ability to:

**Run and monitor systems to deliver business value**

while:

**Continuously improving supporting processes and procedures**

### Memory Trick

> **Operational Excellence = Run + Improve**

---

## Operational Excellence Design Principles

### Perform Operations as Code

Treat operational procedures as:

**Code**

Think:

**Infrastructure as Code**

This allows infrastructure and operational processes to become:

- Repeatable
- Automated
- Versionable

---

### Make Frequent, Small, Reversible Changes

Prefer:

**Small changes**

instead of:

**Large risky changes**

If something fails:

**The change can be reversed more easily**

### Memory Trick

> **Small Changes = Smaller Blast Radius**

---

### Refine Operations Procedures Frequently

Operations procedures should be:

**Continuously improved**

Teams should also remain:

**Familiar with those procedures**

---

### Anticipate Failure

Do not assume:

**Everything will always work**

Architecture and operations should prepare for:

**Failure**

---

### Learn from Operational Failures

Failures should become:

**Learning opportunities**

Use them to improve:

- Procedures
- Systems
- Monitoring
- Automation

---

### Use Managed Services

Managed services can:

**Reduce operational burden**

### Killer Exam Clue

> **Reduce the amount of infrastructure your team must operate**
>
> → **Managed Services**

---

### Implement Observability

Use observability to gain:

**Actionable insights**

into areas such as:

- Performance
- Reliability
- Cost

---

## Operational Excellence Services

The course associates this pillar with services such as:

- [[CloudFormation]]
- [[Config]]
- [[CloudTrail]]
- [[CloudWatch]]
- X-Ray
- CodeBuild
- CodeCommit
- CodeDeploy
- CodePipeline

### Operational Excellence Lifecycle

Think:

**Prepare**

↓  

**Operate**

↓  

**Evolve**

---

# 2. Security

The Security pillar focuses on:

**Protecting information, systems, and assets**

while still:

**Delivering business value**

Security decisions should use:

**Risk assessments and mitigation strategies**

### Memory Trick

> **Security = Protect**

---

## Security Design Principles

### Implement a Strong Identity Foundation

Centralize:

**Privilege management**

Reduce or eliminate reliance on:

**Long-term credentials**

Use:

**Least Privilege**

Think:

[[IAM]]

### Killer Exam Clue

> **Users should receive only the permissions they need**
>
> → **Least Privilege**

---

### Enable Traceability

Integrate:

**Logs and metrics**

so systems can:

- Detect activity
- Respond
- Take action

Think:

- [[CloudTrail]]
- [[CloudWatch]]
- [[Config]]

---

### Apply Security at All Layers

Security should exist throughout:

- Edge network
- VPC
- Subnet
- Load Balancer
- Instance
- Operating system
- Application

### Memory Trick

> **Security Is Layered**

---

### Automate Security Best Practices

Where possible:

**Automate security controls**

rather than relying entirely on:

**Manual processes**

---

### Protect Data in Transit and at Rest

Protect data using techniques such as:

- Encryption
- Tokenization
- Access control

### Killer Exam Clue

> **Protect stored data and network data**
>
> → **Encryption at Rest + In Transit**

---

### Keep People Away from Data

Reduce or eliminate:

**Direct human access**

or:

**Manual processing of data**

where possible.

---

### Prepare for Security Events

Organizations should:

- Run incident-response simulations
- Detect events quickly
- Investigate efficiently
- Recover rapidly

See:

[[Shared Responsibility Model]]

---

## Security Services

The course associates Security with services such as:

- [[IAM]]
- STS
- MFA
- Organizations
- [[Config]]
- [[CloudTrail]]
- [[CloudWatch]]
- [[CloudFront]]
- VPC
- Shield
- WAF
- Inspector
- KMS
- S3
- ELB
- EBS
- RDS
- CloudFormation

---

# 3. Reliability

Reliability is the ability of a system to:

**Recover from infrastructure or service disruptions**

while also being able to:

**Dynamically acquire resources to meet demand**

and mitigate disruptions such as:

- Misconfigurations
- Temporary network problems

### Memory Trick

> **Reliability = Recover + Continue**

---

## Reliability Design Principles

### Test Recovery Procedures

Use automation to:

**Simulate failures**

or recreate scenarios that previously caused:

**Failures**

### Killer Exam Clue

> **Test whether disaster/failure recovery actually works**
>
> → **Test Recovery Procedures**

---

### Automatically Recover from Failure

Architectures should:

**Detect and remediate failure automatically**

when possible.

### Memory Trick

> **Failure Happens → Recover Automatically**

---

### Scale Horizontally

Distribute requests across:

**Multiple smaller resources**

rather than relying on:

**One large resource**

This reduces:

**Common points of failure**

---

### Stop Guessing Capacity

Maintain:

**The appropriate level of resources**

to meet demand without:

- Overprovisioning
- Underprovisioning

Think:

**Auto Scaling**

---

### Manage Change Through Automation

Infrastructure changes should use:

**Automation**

to improve:

- Repeatability
- Reliability

---

## Reliability Services

The course associates Reliability with services such as:

- [[IAM]]
- VPC
- Service Quotas
- Trusted Advisor
- [[CloudWatch]]
- [[CloudTrail]]
- [[Config]]
- Auto Scaling
- Backups
- [[CloudFormation]]
- [[S3]]
- S3 Glacier
- [[Route 53]]

---

# 4. Performance Efficiency

Performance Efficiency means:

**Using computing resources efficiently to meet system requirements**

and maintaining that efficiency as:

- Demand changes
- Technology evolves

### Memory Trick

> **Performance Efficiency = Right Resource, Right Time**

---

## Performance Efficiency Design Principles

### Democratize Advanced Technologies

AWS turns advanced technology into:

**Managed services**

This allows organizations to focus more on:

**Product development**

instead of building complex technology themselves.

---

### Go Global in Minutes

AWS makes it easier to deploy workloads in:

**Multiple Regions**

See:

[[Global Infrastructure]]

---

### Use Serverless Architectures

Serverless architectures help avoid:

**The burden of managing servers**

### Killer Exam Clue

> **Need to reduce server administration**
>
> → Consider **Serverless**

---

### Experiment More Often

Cloud computing makes:

**Comparative testing**

easier.

Organizations can experiment with:

**Different architectures and services**

---

### Mechanical Sympathy

The course describes this as:

**Being aware of the available AWS services**

so you can select technology that:

**Fits the workload**

### Memory Trick

> **Know the Services → Choose the Right Tool**

---

## Performance Efficiency Services

The course associates this pillar with services such as:

- Auto Scaling
- EBS
- S3
- Lambda
- RDS
- CloudFormation
- CloudWatch
- ElastiCache
- Snowball
- CloudFront

---

# 5. Cost Optimization

Cost Optimization means:

**Running systems that deliver business value at the lowest price point**

### Memory Trick

> **Cost Optimization = Spend Only What Creates Value**

---

## Cost Optimization Design Principles

### Adopt a Consumption Model

Pay for:

**What you use**

rather than buying:

**Large amounts of infrastructure upfront**

### Killer Exam Clue

> **Pay only for consumed resources**
>
> → **Consumption Model**

---

### Measure Overall Efficiency

Use monitoring such as:

**CloudWatch**

to understand:

**Resource efficiency**

---

### Stop Spending Money on Data Center Operations

AWS handles:

**The infrastructure layer**

allowing customers to focus more on:

**Business projects**

---

### Analyze and Attribute Expenditure

Understand:

**Who and what is generating cost**

The course specifically calls out:

**Tags**

to help identify:

- Usage
- Costs
- Return on investment

### Killer Exam Clue

> **Determine which project or department owns AWS spending**
>
> → **Tags**

---

### Use Managed and Application-Level Services

Managed services operate at:

**Cloud scale**

and can reduce:

**Total cost of ownership**

---

## Cost Optimization Areas

The course groups this pillar into:

- Expenditure Awareness
- Cost-Effective Resources
- Matching Supply and Demand
- Optimizing Over Time

---

## Cost Optimization Services

Examples from the course include:

- AWS Budgets
- Cost and Usage Report
- Cost Explorer
- Reserved Instance Reporting
- Spot Instances
- Reserved Instances
- S3 Glacier
- Trusted Advisor
- Auto Scaling
- Lambda

---

# 6. Sustainability

Sustainability focuses on:

**Minimizing the environmental impact of running cloud workloads**

### Memory Trick

> **Sustainability = Do More With Less Environmental Impact**

---

## Sustainability Design Principles

### Understand Your Impact

Establish:

**Performance indicators**

and evaluate:

**Improvements**

---

### Establish Sustainability Goals

Set:

**Long-term sustainability goals**

for workloads.

The course also mentions modeling:

**Return on investment**

---

### Maximize Utilization

Right-size workloads to:

**Improve energy efficiency**

and reduce:

**Idle resources**

### Killer Exam Clue

> **Reduce unused infrastructure and maximize resource utilization**
>
> → **Right-Sizing**

---

### Adopt More Efficient Hardware and Software

Design workloads so they can take advantage of:

**Newer and more efficient technologies**

over time.

---

### Use Managed Services

Shared and managed services can reduce:

**The amount of infrastructure required**

Examples include automating:

- Moving infrequently accessed data to cold storage
- Adjusting compute capacity

---

### Reduce Downstream Impact

Design services to reduce the:

**Energy or resources required by customers**

and reduce unnecessary requirements for:

**Customer device upgrades**

---

## Sustainability Services and Patterns

The course associates Sustainability with examples including:

- EC2 Auto Scaling
- Lambda
- Fargate
- Cost Explorer
- Graviton-based EC2
- T-family EC2
- Spot Instances
- EFS-IA
- S3 Glacier
- Cold HDD EBS
- S3 Lifecycle Configurations
- S3 Intelligent-Tiering
- Data Lifecycle Manager
- RDS Read Replicas
- Aurora Global Database
- DynamoDB Global Tables
- CloudFront

---

# Six Pillars Comparison

| Pillar | Main Question |
|---|---|
| Operational Excellence | How do we run and improve the system? |
| Security | How do we protect the system and data? |
| Reliability | How does the system recover from failure? |
| Performance Efficiency | Are we using the right resources efficiently? |
| Cost Optimization | Are we delivering value at the lowest price point? |
| Sustainability | How do we minimize environmental impact? |

---

## Pillar Recognition

If you see:

**Infrastructure as Code**

→ Operational Excellence

If you see:

**Least Privilege**

→ Security

If you see:

**Automatic Failure Recovery**

→ Reliability

If you see:

**Choose the right technology for changing demand**

→ Performance Efficiency

If you see:

**Pay only for what you use**

→ Cost Optimization

If you see:

**Reduce idle resources and environmental impact**

→ Sustainability

---

# AWS Well-Architected Tool

The AWS Well-Architected Tool is a:

**Free tool**

used to review architectures against:

**The six Well-Architected Framework pillars**

and help adopt:

**Architectural best practices**

### How It Works

1. Select a workload
2. Answer questions
3. Review answers against the six pillars
4. Receive advice and recommendations

The tool can provide:

- Videos
- Documentation
- Reports
- Dashboard results

### Killer Exam Clue

> **Need to review an AWS workload against the six Well-Architected pillars**
>
> → **AWS Well-Architected Tool**

---

# Framework vs Tool

## Well-Architected Framework

Provides:

**Architectural principles and six pillars**

## Well-Architected Tool

Provides:

**A way to review workloads against those principles**

### Memory Trick

> **FRAMEWORK = RULES**
>
> **TOOL = REVIEW**

---

# CCP Exam Traps

## Trap 1 — The Framework Has Five Pillars

❌

It has:

**Six**

---

## Trap 2 — Sustainability Is Not a Pillar

❌

Sustainability is:

**The sixth pillar**

---

## Trap 3 — Cost Optimization Means Always Choosing the Cheapest Resource

❌

It means:

**Deliver business value at the lowest appropriate price point**

---

## Trap 4 — Reliability Means Only Backups

❌

Reliability also includes:

- Recovering from failures
- Scaling
- Managing change
- Testing recovery

---

## Trap 5 — Security Is Only IAM

❌

Security applies at:

**All layers**

---

## Trap 6 — Operational Excellence Is Only Monitoring

❌

It also includes:

- Operations as code
- Small reversible changes
- Learning from failures
- Managed services
- Observability

---

## Trap 7 — Performance Efficiency Means Maximum Performance at Any Cost

❌

It means:

**Using resources efficiently to meet system requirements**

---

## Trap 8 — Well-Architected Tool Automatically Fixes Architecture

❌

The tool:

**Reviews workloads and provides guidance**

---

# Killer Exam Clues

> **Operations as Code**
>
> → OPERATIONAL EXCELLENCE

> **Small Reversible Changes**
>
> → OPERATIONAL EXCELLENCE

> **Least Privilege**
>
> → SECURITY

> **Protect Data at Rest and in Transit**
>
> → SECURITY

> **Automatically Recover**
>
> → RELIABILITY

> **Test Recovery**
>
> → RELIABILITY

> **Serverless / Right Technology**
>
> → PERFORMANCE EFFICIENCY

> **Pay Only for What You Use**
>
> → COST OPTIMIZATION

> **Tags for Cost Attribution**
>
> → COST OPTIMIZATION

> **Right-Size to Reduce Idle Resources**
>
> → SUSTAINABILITY

> **Review Architecture Against Six Pillars**
>
> → AWS WELL-ARCHITECTED TOOL

---

# Quick Cheat Sheet

| Exam Phrase | Pillar |
|---|---|
| Operations as Code | Operational Excellence |
| Reversible Changes | Operational Excellence |
| Learn from Failures | Operational Excellence |
| Least Privilege | Security |
| Encryption | Security |
| Traceability | Security |
| Automatic Recovery | Reliability |
| Test Recovery | Reliability |
| Horizontal Scaling | Reliability |
| Right Technology | Performance Efficiency |
| Serverless | Performance Efficiency |
| Global Deployment | Performance Efficiency |
| Pay for Usage | Cost Optimization |
| Track Spending | Cost Optimization |
| Match Supply and Demand | Cost Optimization |
| Environmental Impact | Sustainability |
| Right-Size Resources | Sustainability |
| Reduce Idle Capacity | Sustainability |

---

# Final Rapid-Fire

> **RUN + IMPROVE**
> → OPERATIONAL EXCELLENCE
>
> **PROTECT**
> → SECURITY
>
> **RECOVER**
> → RELIABILITY
>
> **USE RESOURCES WELL**
> → PERFORMANCE EFFICIENCY
>
> **SPEND WELL**
> → COST OPTIMIZATION
>
> **REDUCE ENVIRONMENTAL IMPACT**
> → SUSTAINABILITY
>
> **FRAMEWORK**
> → SIX PILLARS
>
> **WELL-ARCHITECTED TOOL**
> → REVIEW WORKLOADS

---

## Master Memory Trick

> [!tip] Well-Architected Framework Master Memory Trick
> Imagine you're running:
>
> **A business**
>
> First:
>
> **Can we operate it well?**
>
> → Operational Excellence
>
> **Can we protect it?**
>
> → Security
>
> **Can it survive problems?**
>
> → Reliability
>
> **Does it perform efficiently?**
>
> → Performance Efficiency
>
> **Are we spending wisely?**
>
> → Cost Optimization
>
> **Are we reducing environmental impact?**
>
> → Sustainability

So remember:

> **OPERATE**
> → OPERATIONAL EXCELLENCE
>
> **PROTECT**
> → SECURITY
>
> **RECOVER**
> → RELIABILITY
>
> **PERFORM**
> → PERFORMANCE EFFICIENCY
>
> **SAVE**
> → COST OPTIMIZATION
>
> **SUSTAIN**
> → SUSTAINABILITY

And if AWS asks:

> **"How can I review my workload against these six pillars?"**
>
> → **AWS Well-Architected Tool**

---

## Related Notes

- [[What is Cloud Computing]]
- [[Global Infrastructure]]
- [[Shared Responsibility Model]]
- [[Cloud Adoption Framework]]
- [[CloudFormation]]
- [[Config]]
- [[CloudTrail]]
- [[CloudWatch]]
- [[IAM]]