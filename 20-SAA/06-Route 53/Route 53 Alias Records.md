## What Problem Does It Solve?

[[Route 53 Alias Records]] solve the problem of pointing a DNS name directly to a **supported AWS resource**, especially when:

- The AWS resource exposes a DNS hostname
- The resource's underlying IP addresses may change
- You need to use the **zone apex**
- You want AWS-native DNS integration

Example:

example.com  
↓  
[[Route 53]] Alias Record  
↓  
[[Application Load Balancer]]

Alias Records are a **Route 53 extension to standard DNS functionality**.

> [!tip] Memory Trick
> **Alias = AWS-aware DNS**
>
> If the destination is a supported AWS resource:
>
> **Think Alias**

---

## How Alias Records Work

Many AWS services expose a hostname instead of giving you a permanent static IP address.

Example:

my-alb-123456789.us-east-1.elb.amazonaws.com

But users should access:

example.com

Instead of manually tracking the IP addresses behind the AWS resource, Route 53 can create an Alias Record:

example.com  
↓  
Alias  
↓  
my-alb-123456789.us-east-1.elb.amazonaws.com  
↓  
[[Application Load Balancer]]

Route 53 automatically recognizes changes in the resource's underlying IP addresses.

### Architecture Thinking

Think:

**Your Domain → Alias → AWS Resource**

AWS manages the resource endpoint underneath.

---

## Alias Records Automatically Track AWS Resource IP Changes

This is an important architecture advantage.

AWS-managed resources such as a [[Application Load Balancer]] can have changing IP addresses behind their DNS hostname.

You should not build an architecture like:

example.com  
↓  
Hard-Coded IP  
↓  
ALB

because the underlying AWS-managed IP addresses may change.

Instead:

example.com  
↓  
[[Route 53]] Alias  
↓  
ALB DNS Name  
↓  
AWS-managed IP addresses

Route 53 handles those changes automatically.

> [!tip] Architecture Rule
> **AWS resource with changing IPs → Point to the resource, not its temporary IPs**

---

## Alias Records Work at the Zone Apex

Unlike [[CNAME]], Alias Records can be used at the:

**Zone Apex**

Example hosted zone:

example.com

Zone apex:

example.com

This is valid:

example.com  
↓  
Alias  
↓  
[[Application Load Balancer]]

A standard CNAME cannot do this.

### Memory Trick

**CNAME = No Apex**

**Alias = Apex Allowed**

---

## Alias Record Types

An Alias Record is not a completely separate DNS record type.

For AWS resources, Alias Records are created as:

- **A records** for IPv4
- **AAAA records** for IPv6

Example:

Record Name:

example.com

Type:

A

Alias:

Enabled

Target:

my-alb-123456789.us-east-1.elb.amazonaws.com

### Exam Trap

Do not think:

**Alias is another record type like A, AAAA, or CNAME**

Instead think:

> **Alias is Route 53 functionality added to an A or AAAA record.**

---

## Alias Records and TTL

With standard DNS records, you normally configure a:

[[Route 53 TTL]]

But with an Alias Record:

**You cannot manually configure the TTL.**

The TTL behavior is controlled by the AWS target resource.

### Memory Trick

**Alias = AWS manages the destination and TTL behavior**

---

## Supported Alias Targets

For the SAA exam, know the major AWS resources that Alias Records can point to.

### Elastic Load Balancers

Alias Records can point to:

- [[Application Load Balancer]]
- [[Network Load Balancer]]
- Classic Load Balancers

Architecture:

example.com  
↓  
[[Route 53]] Alias  
↓  
[[Elastic Load Balancing]]

This is one of the most common exam scenarios.

---

### CloudFront Distributions

Alias Records can point to:

[[05-Networking/CloudFront]]

Example:

example.com  
↓  
Alias  
↓  
[[05-Networking/CloudFront]] Distribution

Common use case:

Public website  
↓  
[[Route 53]]  
↓  
[[05-Networking/CloudFront]]  
↓  
Origin

---

### API Gateway

Alias Records can point to:

[[API Gateway]]

Example:

api.example.com  
↓  
[[Route 53]] Alias  
↓  
[[API Gateway]]

This can be used when exposing APIs behind a friendly custom domain name.

---

### Elastic Beanstalk Environments

Alias Records can point to:

[[Elastic Beanstalk]]

Architecture:

app.example.com  
↓  
[[Route 53]] Alias  
↓  
[[Elastic Beanstalk]]

---

### S3 Websites

Alias Records can point to:

[[S3]] static website endpoints.

Example:

example.com  
↓  
[[Route 53]] Alias  
↓  
[[S3]] Website

This is useful when hosting a static website from S3.

> [!warning] Exam Detail
> This refers to an **S3 Website endpoint**, not just any S3 bucket use case.

---

### VPC Interface Endpoints

Alias Records can point to:

[[VPC Interface Endpoints]]

This allows DNS names to map to private AWS service endpoints inside a VPC.

---

### Global Accelerator

Alias Records can point to:

[[05-Networking/Global Accelerator]]

Example:

example.com  
↓  
[[Route 53]] Alias  
↓  
[[05-Networking/Global Accelerator]]

---

### Another Route 53 Record

An Alias Record can also point to:

**Another Route 53 record in the same Hosted Zone**

Example:

example.com  
↓  
Alias  
↓  
www.example.com

provided that the target is another compatible Route 53 record in the same hosted zone.

---

## Supported Alias Targets — Quick Memory List

Think:

**L C A B S V G R**

- **L** → Load Balancer
- **C** → CloudFront
- **A** → API Gateway
- **B** → Elastic Beanstalk
- **S** → S3 Website
- **V** → VPC Interface Endpoint
- **G** → Global Accelerator
- **R** → Route 53 Record in same Hosted Zone

You do not necessarily need to memorize the acronym itself, but recognize these services when they appear in scenarios.

---

## Critical Limitation — EC2 DNS Names

This is a classic exam trap.

You **cannot create a Route 53 Alias Record directly to an [[EC2]] DNS name**.

Example:

❌ example.com  
↓  
Alias  
↓  
ec2-12-34-56-78.compute.amazonaws.com

This is **not supported**.

### What Should You Do Instead?

If you need a stable endpoint in front of EC2 instances, a common architecture is:

Users  
↓  
[[Route 53]] Alias  
↓  
[[Application Load Balancer]]  
↓  
[[EC2]] Instances

This is much better architecturally because:

- The load balancer is a supported Alias target
- EC2 instances can scale in and out
- Instance IP addresses can change
- The load balancer provides a stable AWS-managed endpoint

> [!tip] Master Exam Shortcut
> **Alias → ELB**
>
> **Not directly → EC2 DNS name**

---

## Architecture Thinking

### Scenario 1 — Root Domain to ALB

A company wants:

example.com

to point to an [[Application Load Balancer]].

The ALB's IP addresses may change.

**Choose → Route 53 Alias Record**

Why?

- ALB is a supported Alias target
- Alias works at the zone apex
- Route 53 tracks AWS-managed IP changes

---

### Scenario 2 — Root Domain to CloudFront

A company hosts a global application using [[05-Networking/CloudFront]].

Users should access:

example.com

**Choose → Route 53 Alias Record**

Architecture:

Users  
↓  
example.com  
↓  
[[Route 53]] Alias  
↓  
[[05-Networking/CloudFront]]

---

### Scenario 3 — API Custom Domain

A company has an API hosted through [[API Gateway]].

Users should call:

api.example.com

**Choose → Route 53 Alias Record**

Architecture:

Client  
↓  
api.example.com  
↓  
[[Route 53]]  
↓  
[[API Gateway]]

---

### Scenario 4 — Static Website

A company hosts a static website using an [[S3]] Website endpoint.

They want:

example.com

to point directly to the website.

**Choose → Route 53 Alias Record**

---

### Scenario 5 — EC2 DNS Name

A company asks whether:

example.com

can use a Route 53 Alias directly to:

ec2-12-34-56-78.compute.amazonaws.com

**Answer → No**

Instead, consider placing an:

[[Application Load Balancer]]

in front of the EC2 instances.

---

## Alias vs A Record

This distinction matters.

### Standard A Record

Maps:

Hostname  
↓  
IPv4 Address

Example:

example.com  
↓  
192.0.2.10

You provide the actual IP address.

---

### Alias A Record

Maps:

Hostname  
↓  
AWS Resource

Example:

example.com  
↓  
Alias A Record  
↓  
[[Application Load Balancer]]

AWS handles the underlying resource addresses.

### Exam Decision

**Known static IPv4 address → A Record**

**Supported AWS resource → Alias A Record**

---

## Alias vs CNAME

| Feature | CNAME | Alias |
|---|---|---|
| Hostname → Hostname | ✅ | AWS targets |
| Zone Apex | ❌ | ✅ |
| AWS Resource Integration | Limited | ✅ Native |
| Tracks AWS Resource IP Changes | Indirectly | ✅ |
| Manual TTL | ✅ | ❌ |
| ELB Target | Possible via hostname on non-apex | ✅ Preferred |
| CloudFront Target | Possible on non-apex | ✅ Preferred |
| EC2 DNS Name | Possible as CNAME on non-apex | ❌ Alias not supported |

---

## Scenario Recognition

### Immediately Think Alias When You See

- Zone apex
- Root domain
- Load Balancer
- CloudFront
- API Gateway
- Elastic Beanstalk
- S3 static website
- VPC Interface Endpoint
- Global Accelerator
- AWS-managed endpoint
- AWS resource IP addresses may change

### Immediately Watch for a Trap When You See

- EC2 DNS hostname
- Hard-coded ELB IP address
- CNAME at root domain
- Manual TTL on Alias

---

## Exam Traps

### Trap 1 — Alias Directly to EC2 DNS Name

Not supported.

You cannot create:

Alias → EC2 DNS Name

A common better design is:

[[Route 53]]  
↓  
Alias  
↓  
[[Application Load Balancer]]  
↓  
[[EC2]]

---

### Trap 2 — Hard-Coding Load Balancer IP Addresses

Do not manually discover and store the IP addresses behind an AWS load balancer.

They may change.

Use:

**Alias → Load Balancer DNS endpoint**

---

### Trap 3 — Alias Has Its Own DNS Type

Alias is not another standard DNS record type.

It is Route 53 functionality used with:

- A
- AAAA

---

### Trap 4 — Manually Configure Alias TTL

You cannot manually set TTL on Alias Records.

AWS controls the TTL behavior.

---

### Trap 5 — CNAME Is Required for AWS Hostnames

Not necessarily.

For supported AWS resources in Route 53:

**Alias is usually preferred**

especially because it works at the zone apex.

---

### Trap 6 — Any AWS Resource Can Be an Alias Target

False.

Only supported AWS resources can be Alias targets.

For example:

✅ [[Application Load Balancer]]

✅ [[05-Networking/CloudFront]]

✅ [[API Gateway]]

❌ EC2 DNS hostname

---

## Quick Cheat Sheet

| Feature | Alias Record |
|---|---|
| Purpose | Hostname → AWS Resource |
| Route 53 Extension | ✅ |
| Zone Apex | ✅ |
| Subdomains | ✅ |
| A Record | ✅ |
| AAAA Record | ✅ |
| Manual TTL | ❌ |
| Tracks AWS Resource IP Changes | ✅ |
| ELB | ✅ |
| CloudFront | ✅ |
| API Gateway | ✅ |
| Elastic Beanstalk | ✅ |
| S3 Website | ✅ |
| VPC Interface Endpoint | ✅ |
| Global Accelerator | ✅ |
| Same Hosted Zone Record | ✅ |
| EC2 DNS Name | ❌ |

---

## Master Memory Trick

> [!tip] Master Memory Trick
> **Alias = AWS Resource Shortcut**
>
> Think:
>
> **Domain → AWS Resource**
>
> without worrying about changing AWS-managed IP addresses.

Remember:

**Alias = Apex Allowed**

**Alias = AWS-Aware**

**Alias = Automatic IP Tracking**

**Alias = No Manual TTL**

And the big exam trap:

> **Alias can point to ELB, but not directly to an EC2 DNS name.**

---

## Related Notes

- [[Route 53]]
- [[Route 53 TTL]]
- [[Route 53 CNAME vs Alias]]
- [[Route 53 Routing Policies]]
- [[Application Load Balancer]]
- [[Network Load Balancer]]
- [[05-Networking/CloudFront]]
- [[API Gateway]]
- [[Elastic Beanstalk]]
- [[S3]]
- [[VPC Interface Endpoints]]
- [[05-Networking/Global Accelerator]]
- [[EC2]]