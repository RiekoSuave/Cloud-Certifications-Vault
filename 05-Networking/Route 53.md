See also: [CloudFront](05-Networking/CloudFront.md)

See also: [Elastic Load Balancing (ELB)](<Elastic Load Balancing (ELB)>)

See also: [Global Accelerator](<05-Networking/Global Accelerator.md>)

## What Problem Does It Solve?

Provides DNS management and routes users to application endpoints.

Route 53 helps users find and reach applications using human-readable domain names instead of needing to remember IP addresses.

### Memory Trick

Route 53 = AWS DNS

---

## Type

Managed DNS Service

---

## What Is Route 53?

Route 53 is a managed:

Domain Name System (DNS)

service.

DNS helps clients understand how to reach a server through URLs.

Basic Idea:

User enters domain name

↓

DNS

↓

Find destination

↓

Connect to application

### Memory Trick

DNS = Internet Phone Book

---

## What Does DNS Do?

DNS translates human-readable domain names into information computers can use to locate resources.

Think:

example.com

↓

DNS

↓

Destination

Without DNS, users would need to know the underlying network destination instead of simply using a domain name.

---

## Route 53 Capabilities

Your course associates Route 53 with:

- DNS management
- Domain registration
- DNS routing
- Health checks
- Routing policies

---

## Domain Registration

Route 53 can be used for:

Domain registration

Example:

example.com

Once a domain exists, DNS records can determine where traffic for that domain should be sent.

---

## DNS Records

DNS uses:

Records

to help determine how clients should reach resources.

Your course specifically introduces the:

A Record

as part of the Route 53 material.

### Memory Trick

DNS Record = Where Should This Name Go?

---

## Health Checks

Route 53 supports:

Health Checks

Health checks can help determine whether an endpoint is healthy.

This can be useful when routing users to available application resources.

### Memory Trick

Health Check = Is the Endpoint Healthy?

---

## Routing Policies

Route 53 supports different:

Routing Policies

These determine how Route 53 responds to DNS queries and routes users toward endpoints.

Your course notes that routing policies are important to recognize at a high level.

We'll expand the individual routing policies when your SAA material introduces them in more depth.

### Memory Trick

Routing Policy = How Route 53 Chooses

---

## Global Applications

Your course associates Route 53 with:

Global DNS

Route 53 can help route users toward deployments based on application requirements.

Your Journal specifically highlights:

- Routing users toward the closest deployment with low latency
- Disaster recovery strategies

### Memory Trick

Route 53 = Global DNS Routing

---

## Route 53 vs ELB

These solve different problems.

### Route 53

DNS routing.

Helps users locate the appropriate endpoint.

### Elastic Load Balancing

Distributes traffic across application targets.

### Memory Trick

Route 53 = Find the Destination

ELB = Distribute the Traffic

See:

[Elastic Load Balancing (ELB)](<Elastic Load Balancing (ELB)>)

---

## Route 53 vs CloudFront

### Route 53

Provides DNS and routing.

### CloudFront

Provides content delivery through edge locations.

### Memory Trick

Route 53 = DNS

CloudFront = CDN

See:

[CloudFront](05-Networking/CloudFront.md)

---

## Route 53 vs Global Accelerator

### Route 53

Think:

DNS-based global routing

### Global Accelerator

Think:

Improving global application availability and performance using the AWS global network.

### Memory Trick

Route 53 = DNS Routing

Global Accelerator = Global Application Performance

See:

[Global Accelerator](<05-Networking/Global Accelerator.md>)

---

## Common Use Cases

- DNS management
- Websites
- Domain registration
- Routing users to application endpoints
- Health-based routing
- Global applications
- Disaster recovery strategies

---

## Scenario Questions

A company needs a managed DNS service.

→ Route 53

---

A company needs to register and manage a domain.

→ Route 53

---

Users need to reach an application using a domain name.

→ Route 53

---

A company wants DNS routing based on endpoint health.

→ Route 53

---

A company needs to distribute incoming traffic across multiple EC2 instances.

→ Elastic Load Balancing

NOT Route 53

---

A company needs cached content delivered from edge locations.

→ CloudFront

NOT Route 53

---

## Don't Confuse These

Route 53 = DNS

ELB = Load Balancing

CloudFront = Content Delivery Network

Global Accelerator = Global Application Performance

---

## Exam Keywords

DNS

Domain Name System

Domain Registration

DNS Records

A Record

Health Checks

Routing Policies

Global DNS

Domains

Routing

---

## Quick Cheat Sheet

Route 53 = AWS DNS

DNS = Domain Name → Destination

Route 53 = Domain Registration

Route 53 = Health Checks

Route 53 = Routing Policies

Route 53 = Global DNS

ELB = Distribute Traffic

CloudFront = Deliver Content

Global Accelerator = Improve Global Application Performance