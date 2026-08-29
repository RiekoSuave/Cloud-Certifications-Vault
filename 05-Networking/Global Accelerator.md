See also: [CloudFront](05-Networking/CloudFront.md)

See also: [Route 53](<05-Networking/Route 53.md>)

See also: [Elastic Load Balancing (ELB)](<Elastic Load Balancing (ELB)>)

## What Problem Does It Solve?

Improves the performance and availability of global applications.

Global Accelerator helps reduce inconsistent internet performance by routing traffic through the AWS global network.

### Memory Trick

Global Accelerator = Faster Global Apps

---

## Type

Networking Optimization Service

---

## What Is Global Accelerator?

Global Accelerator improves global application performance by directing user traffic through the AWS global network.

Basic Idea:

User

↓

Global Accelerator

↓

AWS Global Network

↓

Application Endpoint

Instead of relying entirely on the public internet path, traffic can take advantage of the AWS global network.

### Memory Trick

Global Accelerator = Fast Lane Through AWS

---

## AWS Global Network

A major concept behind Global Accelerator is the use of the:

AWS Global Network

Traffic enters the AWS network and is routed toward the application endpoint.

This can help improve:

- Performance
- Latency
- Availability
- Consistency

### Memory Trick

Global Accelerator = Use AWS Backbone

---

## Static IP Addresses

Global Accelerator provides:

Static IP Addresses

These provide fixed entry points for applications.

### Memory Trick

Global Accelerator = Static Entry Points

---

## Global Applications

Global Accelerator is useful for applications serving users across multiple geographic locations.

Think:

Users Around the World

↓

Global Accelerator

↓

AWS Global Network

↓

Application

### Memory Trick

Global Users + Application Performance

→ Global Accelerator

---

## Global Accelerator vs CloudFront

This is the most important comparison.

### Global Accelerator

Improves:

Application Performance

Uses:

AWS Global Network

Think:

Network Traffic

### CloudFront

Improves:

Content Delivery

Uses:

Edge Locations and Caching

Think:

Cached Content

| Global Accelerator | CloudFront |
|---|---|
| Application performance | Content delivery |
| AWS global network | Edge locations |
| Static IP addresses | Content caching |
| Network optimization | CDN |

### Memory Trick

Global Accelerator = Application

CloudFront = Content

See:

[CloudFront](05-Networking/CloudFront.md)

---

## Global Accelerator vs Route 53

### Global Accelerator

Improves global application performance using the AWS global network.

### Route 53

Provides DNS and routing.

### Memory Trick

Global Accelerator = Improve the Connection

Route 53 = Find the Destination

See:

[Route 53](<05-Networking/Route 53.md>)

---

## Global Accelerator vs ELB

### Global Accelerator

Helps direct global traffic toward application endpoints using the AWS global network.

### Elastic Load Balancing

Distributes incoming traffic across application targets.

### Memory Trick

Global Accelerator = Global Traffic Performance

ELB = Distribute Traffic

See:

[Elastic Load Balancing (ELB)](<Elastic Load Balancing (ELB)>)

---

## Common Use Cases

- Global applications
- Applications requiring low latency
- Improving global network performance
- Applications requiring static IP addresses

---

## Scenario Questions

A company wants to improve the performance of a global application using the AWS global network.

→ Global Accelerator

---

A company needs static IP addresses as entry points for a global application.

→ Global Accelerator

---

A company wants to reduce inconsistent internet performance for users around the world.

→ Global Accelerator

---

A company wants to cache static content closer to users.

→ CloudFront

NOT Global Accelerator

---

A company needs DNS management and routing.

→ Route 53

NOT Global Accelerator

---

A company needs to distribute traffic across multiple EC2 instances.

→ Elastic Load Balancing

NOT Global Accelerator

---

## Don't Confuse These

Global Accelerator = Global Application Performance

CloudFront = Content Delivery Network

Route 53 = DNS

ELB = Distribute Application Traffic

Global Accelerator = Static IP Addresses

CloudFront = Edge Caching

---

## Exam Keywords

Global Accelerator

AWS Global Network

Global Applications

Low Latency

Static IP Addresses

Application Performance

Network Optimization

---

## Quick Cheat Sheet

Global Accelerator = Faster Global Apps

Global Accelerator = AWS Global Network

Global Accelerator = Static IP Addresses

CloudFront = Content Delivery

CloudFront = Edge Caching

Route 53 = DNS

ELB = Distribute Traffic

Global Accelerator = Application

CloudFront = Content