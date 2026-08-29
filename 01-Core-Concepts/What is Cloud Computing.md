## Overview

**Cloud computing** is the:

> **On-demand delivery of compute power, database storage, applications, and other IT resources through a cloud services platform with pay-as-you-go pricing.**

Instead of purchasing and maintaining your own physical infrastructure:

**AWS owns and maintains the underlying hardware**

while:

**You provision and use the resources you need.**

### Simple Architecture

Traditional IT:

Business  
↓  
Buy Hardware  
↓  
Install Hardware  
↓  
Maintain Data Center  
↓  
Run Applications

Cloud Computing:

Business  
↓  
AWS Cloud  
↓  
Provision Resources On-Demand  
↓  
Run Applications

> [!tip] Memory Trick
> **Cloud = Rent IT Resources On-Demand**

---

## What Makes Up a Traditional Server?

A server generally requires:

- **Compute** → CPU
- **Memory** → RAM
- **Storage** → Data
- **Database** → Structured data storage
- **Networking** → Routers, switches, DNS servers

Before cloud computing, organizations typically had to:

**Own or operate this infrastructure themselves.**

---

## Traditional IT Infrastructure

Traditional infrastructure commonly required organizations to operate:

**Physical Data Centers**

This meant paying for and managing:

- Data center space
- Power
- Cooling
- Hardware
- Maintenance
- Infrastructure monitoring
- Disaster planning

### Traditional Model

Company  
↓  
Data Center  
↓  
Physical Servers  
↓  
Networking  
↓  
Storage  
↓  
Applications

---

## Problems with Traditional IT

Traditional infrastructure creates several challenges.

### Data Center Costs

Organizations must pay for:

- Data center space
- Power
- Cooling
- Maintenance

---

### Hardware Takes Time

Adding or replacing hardware:

**Takes time**

A company cannot instantly create:

**New physical servers**

---

### Limited Scaling

Traditional infrastructure has:

**Finite physical capacity**

If demand suddenly increases:

**More hardware may need to be purchased and installed.**

---

### Operational Overhead

Organizations may need:

**24/7 teams**

to monitor and maintain infrastructure.

---

### Disaster Risk

Organizations must plan for events such as:

- Earthquakes
- Power outages
- Fires
- Hardware failures

This creates additional:

**Cost + complexity**

---

## Cloud Computing Model

Cloud computing changes the infrastructure model.

Instead of:

**Buying infrastructure**

you:

**Consume infrastructure as a service**

AWS provides access to resources such as:

- Servers
- Storage
- Databases
- Application services

These resources can be provisioned:

**Almost instantly**

---

## On-Demand Resources

Cloud computing allows you to provision:

**The type and size of computing resources you need**

when:

**You need them**

You can increase or decrease resources depending on:

**Demand**

### Architecture

Need Resources  
↓  
Provision AWS Resources  
↓  
Use Resources  
↓  
Demand Changes  
↓  
Adjust Resources

---

## Pay-As-You-Go

One of the fundamental ideas behind cloud computing is:

**Pay for what you use**

Instead of making large upfront investments in:

**Physical infrastructure**

you consume AWS resources as needed.

### Memory Trick

> **OWN LESS → RENT MORE → PAY FOR USE**

---

## Five Characteristics of Cloud Computing

The course identifies five important characteristics of cloud computing.

### 1. On-Demand Self-Service

Users can:

**Provision resources themselves**

without requiring:

**Human interaction from the service provider**

### Exam Clue

> **Provision resources whenever needed**

Think:

**On-Demand Self-Service**

---

### 2. Broad Network Access

Cloud resources are:

**Available over a network**

and accessible from:

**Different types of client platforms**

### Exam Clue

> **Resources accessible across networks and devices**

Think:

**Broad Network Access**

---

### 3. Multi-Tenancy and Resource Pooling

Multiple customers can:

**Share the same underlying infrastructure**

while maintaining:

**Security and privacy**

AWS can serve multiple customers using:

**Shared physical resources**

### Exam Clue

> **Multiple customers sharing cloud infrastructure**

Think:

**Multi-Tenancy / Resource Pooling**

---

### 4. Rapid Elasticity and Scalability

Cloud resources can be:

**Quickly acquired or released**

depending on:

**Demand**

Resources can therefore scale:

**Up or down as needed**

### Exam Clue

> **Rapidly adjust resources as demand changes**

Think:

**Elasticity**

---

### 5. Measured Service

Cloud usage is:

**Measured**

so customers can be charged based on:

**What they actually use**

### Exam Clue

> **Usage is tracked for billing**

Think:

**Measured Service**

---

## Scalability vs Elasticity

These concepts are related but not identical.

| Concept | Meaning |
|---|---|
| **Scalability** | Ability to accommodate larger workloads by increasing resources |
| **Elasticity** | Ability to automatically or quickly add and remove resources as demand changes |

### Scalability

Demand Increases  
↓  
Increase Resources

### Elasticity

Demand Increases  
↓  
Add Resources  
↓  
Demand Decreases  
↓  
Remove Resources

### Memory Trick

> **Scalability = HANDLE GROWTH**
>
> **Elasticity = GROW + SHRINK**

---

## Six Advantages of Cloud Computing

The course identifies six major advantages.

---

### 1. Trade CAPEX for OPEX

Instead of:

**Purchasing hardware upfront**

organizations can:

**Pay on demand**

This shifts spending away from large:

**Capital Expenses (CAPEX)**

toward:

**Operational Expenses (OPEX)**

### Memory Trick

> **CAPEX = BUY**
>
> **OPEX = USE**

---

### 2. Benefit from Massive Economies of Scale

AWS operates infrastructure at:

**Massive scale**

This allows AWS to operate more efficiently and:

**Reduce prices**

### Exam Clue

> **Lower costs because the cloud provider operates at massive scale**

Think:

**Economies of Scale**

---

### 3. Stop Guessing Capacity

Traditional IT requires organizations to predict:

**Future infrastructure requirements**

Cloud computing allows organizations to:

**Scale based on actual usage**

### Traditional

Guess Capacity  
↓  
Buy Hardware  
↓  
Hope Forecast Was Correct

### Cloud

Measure Demand  
↓  
Adjust Resources

### Exam Clue

> **Avoid overprovisioning or underprovisioning**

Think:

**Stop Guessing Capacity**

---

### 4. Increase Speed and Agility

Cloud resources can be provisioned:

**Rapidly**

This allows organizations to:

- Develop faster
- Test faster
- Launch applications faster

### Exam Clue

> **Quickly provision infrastructure**

Think:

**Speed + Agility**

---

### 5. Stop Spending Money Running and Maintaining Data Centers

AWS handles the underlying:

**Cloud infrastructure**

Organizations therefore do not need to spend as much time and money operating:

**Their own physical data centers**

### Exam Clue

> **Reduce infrastructure management**

Think:

**Move to the Cloud**

---

### 6. Go Global in Minutes

AWS provides:

**Global infrastructure**

Organizations can deploy applications closer to:

**Users around the world**

without building their own:

**Global data centers**

### Exam Clue

> **Quickly deploy applications worldwide**

Think:

**AWS Global Infrastructure**

See:

[[Global Infrastructure]]

---

## Problems Solved by the Cloud

Cloud computing provides several major benefits.

### Flexibility

Change:

**Resource types**

when needed.

---

### Cost-Effectiveness

Use:

**Pay-as-you-go pricing**

and pay for:

**What you use**

---

### Scalability

Handle larger workloads by:

- Increasing hardware capacity
- Adding additional resources

---

### Elasticity

Scale:

**Out**

and:

**In**

as needed.

---

### High Availability and Fault Tolerance

Applications can be designed across:

**Multiple data centers**

to improve:

- Availability
- Resilience

See:

[[Global Infrastructure]]

---

### Agility

Organizations can rapidly:

- Develop
- Test
- Launch

applications.

---

## Cloud Deployment Models

There are three major cloud deployment models:

1. **Private Cloud**
2. **Public Cloud**
3. **Hybrid Cloud**

---

## Private Cloud

A **Private Cloud** provides cloud services for:

**A single organization**

and is:

**Not exposed to the public**

### Benefits

- Complete control
- Security for sensitive applications
- Ability to meet specific business requirements

### Exam Clue

> **Cloud environment dedicated to one organization**

Think:

**Private Cloud**

---

## Public Cloud

A **Public Cloud** uses cloud resources:

**Owned and operated by a third-party cloud provider**

and delivered through:

**The Internet**

AWS is an example of:

**Public Cloud**

### Exam Clue

> **Third-party provider owns and operates the cloud infrastructure**

Think:

**Public Cloud**

---

## Hybrid Cloud

A **Hybrid Cloud** combines:

**On-Premises Infrastructure**

with:

**Cloud Infrastructure**

An organization can keep certain systems:

**On-Premises**

while extending other capabilities into:

**The Cloud**

### Architecture

On-Premises  
↕  
Hybrid Connectivity  
↕  
AWS Cloud

### Why Hybrid?

Organizations may want:

**Control over sensitive assets**

while gaining the:

**Flexibility + cost-effectiveness**

of the public cloud.

### Exam Clue

> **Keep some infrastructure on-premises while using AWS**

Think:

**Hybrid Cloud**

---

## Deployment Model Comparison

| Model | Key Idea |
|---|---|
| **Private Cloud** | One organization |
| **Public Cloud** | Third-party cloud provider |
| **Hybrid Cloud** | On-premises + public cloud |

### Memory Trick

> **PRIVATE = MINE**
>
> **PUBLIC = PROVIDER**
>
> **HYBRID = BOTH**

---

## Types of Cloud Computing

There are three major service models:

1. **IaaS**
2. **PaaS**
3. **SaaS**

---

## Infrastructure as a Service — IaaS

IaaS provides:

**Building blocks for cloud IT**

including:

- Networking
- Computers
- Data storage

IaaS provides the:

**Highest level of flexibility**

and most closely resembles:

**Traditional on-premises IT**

### AWS Example

**EC2**

### Exam Clue

> **Virtual servers where the customer manages much of the software stack**

Think:

**IaaS**

---

## Platform as a Service — PaaS

PaaS removes the need to manage:

**Underlying infrastructure**

This allows the organization to focus on:

**Deploying and managing applications**

### AWS Example

**Elastic Beanstalk**

### Exam Clue

> **Focus on application deployment instead of infrastructure**

Think:

**PaaS**

---

## Software as a Service — SaaS

SaaS provides:

**A completed product**

that is:

**Run and managed by the service provider**

### Examples from the Course

- Gmail
- Dropbox
- Zoom

The course also lists AWS services such as:

**Rekognition**

as a SaaS example.

### Exam Clue

> **Finished software managed by the provider**

Think:

**SaaS**

---

## IaaS vs PaaS vs SaaS

| Model | Think |
|---|---|
| **IaaS** | Manage infrastructure building blocks |
| **PaaS** | Deploy applications without managing underlying infrastructure |
| **SaaS** | Use finished software |

### Memory Trick

> **IaaS = BUILD**
>
> **PaaS = DEPLOY**
>
> **SaaS = USE**

---

## Cloud Pricing Fundamentals

AWS follows:

**Pay-as-you-go pricing**

The course highlights three fundamental pricing areas.

### Compute

Pay for:

**Compute time**

---

### Storage

Pay for:

**Data stored in the cloud**

---

### Data Transfer OUT

Generally:

**Data transfer OUT of the cloud is charged**

while the course states:

**Data transfer IN is free**

### Memory Trick

> **COMPUTE**
> → TIME
>
> **STORAGE**
> → DATA STORED
>
> **TRANSFER**
> → DATA OUT

---

## CCP Exam Traps

### Trap 1 — Cloud Means Everything Is Free

❌ Wrong

Cloud computing is:

**Pay-as-you-go**

not:

**Free**

---

### Trap 2 — Scalability and Elasticity Are Identical

❌ Not exactly

**Scalability**

→ Handle larger workloads

**Elasticity**

→ Add and remove resources based on demand

---

### Trap 3 — Hybrid Means Multiple Public Cloud Providers

❌ Wrong

Hybrid Cloud means:

**On-Premises + Cloud**

---

### Trap 4 — IaaS Means AWS Manages Everything

❌ Wrong

IaaS gives customers:

**More control and management responsibility**

than PaaS or SaaS.

---

### Trap 5 — SaaS Gives the Customer Maximum Infrastructure Control

❌ Wrong

SaaS is:

**A completed product managed by the provider**

---

## Killer Exam Clues

> **Pay only for resources consumed**
>
> → Pay-as-you-go

> **Avoid large upfront hardware purchases**
>
> → CAPEX → OPEX

> **Automatically adjust capacity**
>
> → Elasticity

> **Handle increasing workloads**
>
> → Scalability

> **Provision infrastructure quickly**
>
> → Agility

> **Lower pricing due to provider scale**
>
> → Economies of Scale

> **Single organization**
>
> → Private Cloud

> **Third-party provider**
>
> → Public Cloud

> **On-premises + AWS**
>
> → Hybrid Cloud

> **Infrastructure building blocks**
>
> → IaaS

> **Focus on deploying applications**
>
> → PaaS

> **Finished managed application**
>
> → SaaS

---

## Quick Cheat Sheet

| Exam Phrase | Think |
|---|---|
| On-demand resources | Cloud Computing |
| Pay for usage | Pay-as-you-go |
| Avoid upfront hardware | OPEX |
| Provider operates at huge scale | Economies of Scale |
| Stop predicting hardware needs | Stop Guessing Capacity |
| Quickly provision resources | Agility |
| Increase resources for growth | Scalability |
| Add/remove resources with demand | Elasticity |
| One organization's cloud | Private Cloud |
| Third-party cloud provider | Public Cloud |
| On-prem + cloud | Hybrid Cloud |
| Infrastructure building blocks | IaaS |
| Application platform | PaaS |
| Finished application | SaaS |
| Compute pricing | Compute time |
| Storage pricing | Data stored |
| Transfer pricing | Data transfer OUT |

---

## Master Memory Trick

> [!tip] Cloud Computing Master Memory Trick
> Think:
>
> **OLD IT**
>
> BUY  
> ↓  
> INSTALL  
> ↓  
> MAINTAIN  
> ↓  
> GUESS CAPACITY
>
> **CLOUD**
>
> REQUEST  
> ↓  
> PROVISION  
> ↓  
> USE  
> ↓  
> PAY
>
> Cloud computing turns:
>
> **OWNING INFRASTRUCTURE**
>
> into:
>
> **CONSUMING INFRASTRUCTURE**

For deployment models:

> **PRIVATE**
> → MINE
>
> **PUBLIC**
> → PROVIDER
>
> **HYBRID**
> → BOTH

For service models:

> **IaaS**
> → BUILD
>
> **PaaS**
> → DEPLOY
>
> **SaaS**
> → USE

And for cloud benefits:

> **PAY**
> → OPEX
>
> **SCALE**
> → DEMAND
>
> **ELASTIC**
> → GROW + SHRINK
>
> **AGILE**
> → MOVE FAST
>
> **GLOBAL**
> → DEPLOY WORLDWIDE

---

## Related Notes

- [[Global Infrastructure]]
- [[Shared Responsibility Model]]
- [[Cloud Adoption Framework]]
- [[Well-Architected Framework]]