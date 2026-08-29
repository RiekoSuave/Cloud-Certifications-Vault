## Overview

AWS operates a:

**Global Cloud Infrastructure**

that allows customers to deploy applications and resources across:

- Multiple geographic locations
- Multiple Regions
- Multiple Availability Zones
- Edge locations

AWS Global Infrastructure is designed to provide:

- High availability
- Fault tolerance
- Low latency
- Global reach
- Disaster recovery options

> [!tip] Memory Trick
> **Region → Geographic Area**
>
> **AZ → Data Center Group**
>
> **Edge Location → Close to Users**

---

## AWS Global Infrastructure

AWS infrastructure is organized around:

**Regions**

and:

**Availability Zones**

AWS also operates:

**Points of Presence / Edge Locations**

to deliver services closer to:

**End users**

### Simple Architecture

AWS Global Infrastructure  
↓  
Regions  
↓  
Availability Zones  
↓  
Data Centers

Meanwhile:

Users  
↓  
Edge Locations  
↓  
AWS Resources

---

## AWS Regions

An AWS **Region** is:

**A cluster of data centers**

AWS has Regions:

**All around the world**

Examples include:

- `us-east-1`
- `us-east-2`
- `eu-west-1`
- `ap-southeast-2`

Each Region has:

**A unique name and code**

---

## AWS Regions Are Separate

AWS Regions are designed to be:

**Independent from one another**

Most AWS services are:

**Region-scoped**

This means when you create a resource in one Region:

**It generally exists in that Region**

unless you explicitly configure:

**Replication or another cross-Region mechanism**

### Exam Clue

> **Application must survive failure of an entire geographic Region**

Think:

**Multi-Region Architecture**

---

## How Do You Choose an AWS Region?

The course identifies four major factors.

### 1. Compliance

Some organizations must keep data:

**Within a specific geographic location**

because of:

- Government requirements
- Regulatory requirements
- Company policies

### Example

If data must remain:

**In France**

you may need to choose:

**A French AWS Region**

### Exam Clue

> **Data must remain in a particular country**

Think:

**Compliance**

---

### 2. Proximity to Customers

Deploy applications:

**Closer to users**

to reduce:

**Network latency**

### Architecture

Users  
↓  
Closest Appropriate AWS Region  
↓  
Application

### Exam Clue

> **Reduce latency for customers**

Think:

**Choose a Region closer to users**

---

### 3. Available Services

Not every AWS service is necessarily:

**Available in every Region**

Some new services may initially be available in:

**Selected Regions**

### Exam Clue

> **Application requires a specific AWS service**

Check:

**Whether that service is available in the Region**

---

### 4. Pricing

AWS service pricing can:

**Vary between Regions**

Therefore Region selection may also depend on:

**Cost**

### Memory Trick

> **Region Selection = C-P-S-P**
>
> **C**ompliance
>
> **P**roximity
>
> **S**ervice Availability
>
> **P**ricing

---

## Region Selection Cheat Sheet

| Requirement | Region Decision |
|---|---|
| Data residency | Compliance |
| Lowest user latency | Proximity |
| Specific AWS service required | Service Availability |
| Reduce infrastructure cost | Pricing |

---

## Availability Zones

Each AWS Region contains:

**Multiple Availability Zones**

The course describes most Regions as having:

**3 Availability Zones**

with a minimum of:

**3**

and a maximum of:

**6**

---

## What Is an Availability Zone?

An **Availability Zone (AZ)** consists of:

**One or more discrete data centers**

Each AZ has:

- Redundant power
- Networking
- Connectivity

Availability Zones are designed to be:

**Physically separated from each other**

so a disaster affecting one AZ is less likely to affect:

**Another AZ**

---

## Availability Zone Example

Example Region:

**Sydney — `ap-southeast-2`**

Availability Zones:

- `ap-southeast-2a`
- `ap-southeast-2b`
- `ap-southeast-2c`

### Architecture

`ap-southeast-2`  
↓  
├── `ap-southeast-2a`  
├── `ap-southeast-2b`  
└── `ap-southeast-2c`

Each AZ contains:

**One or more data centers**

---

## Availability Zones Are Connected

Availability Zones within a Region are connected using:

**High-bandwidth, ultra-low-latency networking**

This allows applications to operate across:

**Multiple AZs**

while maintaining:

**Fast communication**

### Exam Clue

> **Application must remain available if one data center location fails**

Think:

**Deploy across multiple Availability Zones**

---

## High Availability with Multiple AZs

Instead of:

Application  
↓  
One AZ

Better:

Application  
↓  
Multiple AZs

### Example

Load Balancer  
↓  
├── EC2 — AZ A  
└── EC2 — AZ B

If:

**AZ A fails**

the application can continue operating from:

**AZ B**

### Memory Trick

> **Multiple AZs = Survive AZ Failure**

---

## Region vs Availability Zone

| Region | Availability Zone |
|---|---|
| Geographic area | Isolated location inside Region |
| Contains multiple AZs | Contains one or more data centers |
| Separate from other Regions | Connected to other AZs in same Region |
| Used for geographic deployment | Used for high availability |

### Killer Shortcut

> **REGION = WHERE IN THE WORLD**
>
> **AZ = WHERE INSIDE THE REGION**

---

## AWS Points of Presence

AWS also operates:

**Points of Presence**

The course groups these into:

- Edge Locations
- Regional Caches

These locations help AWS deliver:

**Content to users with lower latency**

---

## Edge Locations

An **Edge Location** is:

**A location where content can be cached closer to users**

Edge Locations are used by services such as:

**CloudFront**

### Architecture

Origin  
↓  
Edge Location  
↓  
User

Instead of every user retrieving content from:

**The original AWS Region**

cached content can be served from:

**A nearby Edge Location**

### Exam Clue

> **Deliver content globally with low latency**

Think:

**CloudFront + Edge Locations**

---

## Edge Locations Are Not Availability Zones

This is an important distinction.

### Availability Zone

Used to:

**Run regional infrastructure**

### Edge Location

Used to:

**Deliver content/services closer to users**

### Exam Trap

> **Edge Location ≠ Availability Zone**

---

## Region vs AZ vs Edge Location

| Infrastructure | Primary Purpose |
|---|---|
| Region | Geographic deployment |
| Availability Zone | High availability / fault isolation |
| Edge Location | Low-latency content delivery |

### Memory Trick

> **REGION = GEOGRAPHY**
>
> **AZ = AVAILABILITY**
>
> **EDGE = SPEED**

---

## Global Services vs Regional Services

AWS services can have different:

**Geographic scopes**

Some services are:

**Global**

while many others are:

**Regional**

---

## Global Services

The course identifies examples such as:

- IAM
- Route 53
- CloudFront
- WAF

These services are not primarily tied to:

**A single AWS Region**

---

## Regional Services

The course identifies examples such as:

- EC2
- Elastic Beanstalk
- Lambda
- Rekognition

When using these services, you select:

**An AWS Region**

### Exam Clue

> **EC2 resource created in `us-east-1`**

Think:

**Regional Resource**

---

## Global vs Regional Cheat Sheet

| Global | Regional |
|---|---|
| IAM | EC2 |
| Route 53 | Elastic Beanstalk |
| CloudFront | Lambda |
| WAF | Rekognition |

> [!tip] Memory Trick
> **Most AWS resources live somewhere.**
>
> If you select a Region when creating it:
>
> **Think Regional**

---

## AWS Global Infrastructure and High Availability

High availability is commonly achieved by:

**Deploying across multiple Availability Zones**

### Example

Users  
↓  
Load Balancer  
↓  
├── AZ A  
│   └── Application Server  
│  
└── AZ B  
    └── Application Server

This protects against:

**Availability Zone failure**

---

## AWS Global Infrastructure and Disaster Recovery

If the requirement is:

**Survive an entire Region failure**

multiple AZs inside that same Region are:

**Not enough**

Instead think:

Primary Region  
↓  
Replication / Backup  
↓  
Secondary Region

### Killer Exam Rule

> **AZ Failure**
> → Multi-AZ
>
> **Region Failure**
> → Multi-Region

---

## AWS Global Infrastructure and Latency

Latency means:

**The time required for data to travel between locations**

To reduce latency:

### Application Workloads

Choose a:

**Region closer to users**

### Cached Content

Use:

**Edge Locations**

through services such as:

**CloudFront**

### Memory Trick

> **APP CLOSER**
> → REGION
>
> **CONTENT CLOSER**
> → EDGE

---

## Benefits of AWS Global Infrastructure

AWS Global Infrastructure helps customers:

### Deploy Globally

Applications can be deployed:

**Around the world**

without building:

**Physical data centers**

---

### Improve Availability

Applications can operate across:

**Multiple Availability Zones**

---

### Reduce Latency

Resources can be deployed:

**Closer to users**

---

### Support Disaster Recovery

Resources and data can be designed across:

**Multiple Regions**

---

### Meet Compliance Requirements

Organizations can choose Regions based on:

**Data residency requirements**

---

## CCP Exam Traps

### Trap 1 — Region and Availability Zone Are the Same

❌ Wrong

Region:

**Geographic area**

Availability Zone:

**Isolated infrastructure location inside a Region**

---

### Trap 2 — One Availability Zone Provides Multi-AZ High Availability

❌ Wrong

Multi-AZ means:

**Resources span multiple Availability Zones**

---

### Trap 3 — Multiple AZs Protect Against Complete Region Failure

❌ Wrong

All AZs belong to:

**The same Region**

Need protection from:

**Region failure**

Think:

**Multi-Region**

---

### Trap 4 — Edge Locations Run Your Normal EC2 Infrastructure

❌ Wrong

Edge Locations primarily help provide:

**Low-latency delivery closer to users**

---

### Trap 5 — Every AWS Service Is Available in Every Region

❌ Wrong

Service availability can:

**Differ by Region**

---

### Trap 6 — AWS Pricing Is Identical in Every Region

❌ Wrong

Pricing can:

**Vary by Region**

---

### Trap 7 — Always Choose the Closest Region

❌ Wrong

Proximity is only:

**One consideration**

You must also consider:

- Compliance
- Service availability
- Pricing

---

## Killer Exam Clues

> **Data must remain in a specific country**
>
> → COMPLIANCE

> **Reduce latency to application users**
>
> → REGION PROXIMITY

> **Required AWS service isn't everywhere**
>
> → SERVICE AVAILABILITY

> **Infrastructure costs differ geographically**
>
> → REGIONAL PRICING

> **Survive AZ failure**
>
> → MULTI-AZ

> **Survive Region failure**
>
> → MULTI-REGION

> **Global cached content**
>
> → EDGE LOCATIONS / CLOUDFRONT

> **One or more isolated data centers**
>
> → AVAILABILITY ZONE

---

## Quick Cheat Sheet

| Exam Phrase | Think |
|---|---|
| Geographic AWS location | Region |
| Isolated infrastructure inside Region | Availability Zone |
| One or more data centers | Availability Zone |
| High availability | Multiple AZs |
| Entire Region failure | Multi-Region |
| Data residency | Region Compliance |
| Users experiencing latency | Region Proximity |
| Required service | Regional Service Availability |
| Regional cost differences | Pricing |
| Content closer to users | Edge Location |
| CDN | CloudFront |
| Global DNS | Route 53 |
| Global identity | IAM |

---

## Final Rapid-Fire

> **REGION**
> → GEOGRAPHY
>
> **AZ**
> → ISOLATION
>
> **MULTI-AZ**
> → HIGH AVAILABILITY
>
> **MULTI-REGION**
> → REGIONAL RESILIENCE
>
> **EDGE LOCATION**
> → LOW LATENCY
>
> **CLOUDFRONT**
> → GLOBAL CONTENT
>
> **COMPLIANCE**
> → DATA LOCATION
>
> **PROXIMITY**
> → LATENCY
>
> **SERVICE AVAILABILITY**
> → CAN I USE IT THERE?
>
> **PRICING**
> → WHAT DOES IT COST THERE?

---

## Master Memory Trick

> [!tip] Global Infrastructure Master Memory Trick
> Picture AWS as:
>
> **WORLD**
> ↓
> **REGION**
> ↓
> **AZ**
> ↓
> **DATA CENTER**
>
> Then separately:
>
> **USER**
> ↓
> **EDGE LOCATION**
> ↓
> **AWS**
>
> Remember:
>
> **REGION**
> → Choose WHERE
>
> **AZ**
> → Survive FAILURE
>
> **EDGE**
> → Improve SPEED

When choosing a Region:

> **C**
> → Compliance
>
> **P**
> → Proximity
>
> **S**
> → Service Availability
>
> **P**
> → Pricing

And for resilience:

> **AZ FAILS**
> → ANOTHER AZ
>
> **REGION FAILS**
> → ANOTHER REGION

---

## Related Notes

- [[What is Cloud Computing]]
- [[Shared Responsibility Model]]
- [[Cloud Adoption Framework]]
- [[Well-Architected Framework]]