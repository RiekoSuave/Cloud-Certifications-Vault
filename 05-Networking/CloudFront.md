See also: [Route 53](<05-Networking/Route 53.md>)

See also: [Global Accelerator](<05-Networking/Global Accelerator.md>)

See also: [S3](S3)

See also: [Shield and WAF](<Shield and WAF>)

## What Problem Does It Solve?

Delivers content to users with lower latency by caching content closer to them.

CloudFront improves application performance by using AWS Edge Locations around the world.

### Memory Trick

CloudFront = Fast Content Delivery

---

## Type

Content Delivery Network (CDN)

---

## What Is CloudFront?

CloudFront is AWS's:

Content Delivery Network (CDN)

It improves read performance by caching content at AWS Edge Locations closer to users.

Basic Idea:

Origin

↓

CloudFront

↓

Edge Location

↓

User

### Memory Trick

CloudFront = Cache Content Close to Users

---

## Edge Locations

CloudFront uses:

Edge Locations

around the world.

Instead of every user retrieving content directly from the original server, CloudFront can cache copies of content closer to users.

Example:

Origin in AWS Region

↓

CloudFront Edge Location

↓

Nearby User

Benefits:

- Lower latency
- Faster content delivery
- Improved read performance

### Memory Trick

Edge Location = Content Close to User

---

## Content Caching

CloudFront caches content at Edge Locations.

Basic Flow:

User requests content

↓

CloudFront checks Edge Location

↓

Cached content available?

↓

Deliver content to user

This reduces the need to repeatedly retrieve the same content from the origin.

### Memory Trick

CloudFront = Cache at the Edge

---

## CloudFront Origins

An origin is the location where the original content is stored.

Your course identifies several possible origins.

### S3 Bucket

CloudFront can distribute content stored in S3.

Example:

S3 Bucket

↓

CloudFront

↓

Edge Locations

↓

Users

See:

[S3](S3)

---

### VPC Origins

Your course identifies VPC origins such as:

- Application Load Balancer
- Network Load Balancer
- EC2 Instances

---

### Custom HTTP Origins

CloudFront can also use custom HTTP origins.

Your course gives:

S3 Website

as an example.

---

## Origin Access Control (OAC)

Your course introduces:

Origin Access Control

OAC

for securing access between CloudFront and an S3 origin.

The basic idea is:

Users

↓

CloudFront

↓

OAC

↓

S3

This helps keep access to the S3 origin controlled through CloudFront.

### Memory Trick

OAC = Control Access to S3 Through CloudFront

---

## CloudFront and Security

Your course associates CloudFront with protection against network and application attacks.

CloudFront integrates with:

- AWS Shield
- AWS WAF

This can help protect applications against attacks such as:

DDoS attacks

See:

[Shield and WAF](<Shield and WAF>)

### Memory Trick

CloudFront + Shield + WAF = Edge Protection

---

## CloudFront vs S3

These services solve different problems.

### S3

Stores objects.

### CloudFront

Delivers and caches content closer to users.

### Memory Trick

S3 = Store Content

CloudFront = Deliver Content

---

## CloudFront vs S3 Cross-Region Replication

Your course makes an important distinction between these two.

### CloudFront

- Global Edge Network
- Files are cached for a TTL
- Great for static content that must be available everywhere

### S3 Cross-Region Replication

- Must be configured for each Region
- Files are updated in near real-time
- Read-only replication
- Great for dynamic content that needs low latency in selected Regions

### Memory Trick

CloudFront = Cache Globally

S3 CRR = Replicate Between Regions

---

## CloudFront vs Global Accelerator

### CloudFront

Think:

Content Delivery

Caching

Edge Locations

### Global Accelerator

Think:

Global Application Performance

AWS Global Network

### Memory Trick

CloudFront = Content

Global Accelerator = Application

See:

[Global Accelerator](<05-Networking/Global Accelerator.md>)

---

## CloudFront vs Route 53

### CloudFront

Delivers content through Edge Locations.

### Route 53

Provides DNS and routing.

### Memory Trick

CloudFront = Deliver Content

Route 53 = Find Destination

See:

[Route 53](<05-Networking/Route 53.md>)

---

## Common Use Cases

- Websites
- Static content
- Videos
- Global content delivery
- S3 content distribution
- Reducing latency
- Improving read performance

---

## Scenario Questions

A company wants to cache content closer to users around the world.

→ CloudFront

---

A website needs a Content Delivery Network.

→ CloudFront

---

A company wants to reduce latency when delivering static content globally.

→ CloudFront

---

A company wants to securely distribute content from an S3 bucket through CloudFront.

→ CloudFront with Origin Access Control

---

A company needs to store objects.

→ S3

NOT CloudFront

---

A company needs DNS management and routing.

→ Route 53

NOT CloudFront

---

A company needs to improve global application performance rather than cache content.

→ Global Accelerator

---

## Don't Confuse These

CloudFront = CDN

Edge Location = Cache Close to Users

S3 = Object Storage

OAC = Control Access to S3 Origin

Route 53 = DNS

Global Accelerator = Global Application Performance

Shield = DDoS Protection

WAF = Web Application Firewall

---

## Exam Keywords

CloudFront

CDN

Content Delivery Network

Edge Locations

Caching

Low Latency

Origin

S3 Origin

Origin Access Control

OAC

DDoS Protection

Static Content

---

## Quick Cheat Sheet

CloudFront = AWS CDN

CloudFront = Fast Content Delivery

Edge Locations = Cache Close to Users

Origin = Original Content Source

S3 = Store Content

CloudFront = Deliver Content

OAC = Secure S3 Origin Access

CloudFront + Shield + WAF = Edge Protection

CloudFront = Cache Globally

S3 CRR = Replicate Between Regions

Route 53 = DNS

Global Accelerator = Global Application Performance