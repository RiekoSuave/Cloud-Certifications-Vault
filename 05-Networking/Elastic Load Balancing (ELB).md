See also: [High Availability, Scalability, Elasticity](<High Availability, Scalability, Elasticity>)

See also: [VPC](05-Networking/VPC.md)

See also: [Route 53](<05-Networking/Route 53.md>)

## What Problem Does It Solve?

Distributes incoming traffic across multiple resources to improve availability, scalability, and fault tolerance.

Elastic Load Balancing helps prevent individual servers from becoming a single point of failure.

### Memory Trick

ELB = Spread Traffic Around

---

## Type

Managed Load Balancer

---

## What Is Elastic Load Balancing (ELB)?

Elastic Load Balancing is an AWS managed service that automatically distributes incoming traffic across multiple targets.

Targets can include:

- EC2 Instances
- Auto Scaling Groups
- Containers
- Applications

AWS manages much of the underlying load balancer infrastructure for you.

---

## Why Use a Load Balancer?

A load balancer can:

- Spread traffic across multiple downstream instances
- Provide a single point of access to an application
- Handle failures of downstream instances
- Perform health checks
- Support HTTPS / SSL termination
- Improve availability across Availability Zones

---

## Traffic Distribution

Instead of sending all traffic to one server:

Users

↓

ELB

↓

Multiple Targets

The load balancer distributes incoming requests across available targets.

### Memory Trick

ELB = Traffic Distributor

---

## Single Point of Access

ELB provides a single DNS endpoint for your application.

Users don't need to know the addresses of individual EC2 instances.

Basic Architecture:

Users

↓

ELB DNS Name

↓

ELB

↓

EC2 Instances

### Exam Clue

Need one endpoint for multiple servers?

→ ELB

---

## Health Checks

ELB regularly checks the health of registered targets.

If an instance becomes unhealthy:

- ELB detects the problem
- Stops routing traffic to the unhealthy instance
- Continues routing traffic to healthy instances

### Memory Trick

Health Check = Is This Server Healthy?

---

## High Availability

ELB can distribute traffic across resources in multiple Availability Zones.

Example:

ELB

↓

Availability Zone A → EC2

Availability Zone B → EC2

This helps applications remain available if resources in one Availability Zone experience problems.

See:

[High Availability, Scalability, Elasticity](<High Availability, Scalability, Elasticity>)

---

## SSL Termination

ELB can handle HTTPS encryption for applications.

This is called:

SSL Termination

Instead of every backend server handling the external HTTPS connection, the load balancer can handle that work.

Benefits include:

- Simplified certificate management
- Reduced workload on backend servers

### Memory Trick

SSL Termination = ELB Handles HTTPS

---

## Types of AWS Load Balancers

Your course identifies three major modern load balancer types:

- Application Load Balancer
- Network Load Balancer
- Gateway Load Balancer

---

## Application Load Balancer (ALB)

Operates at:

Layer 7

Designed for:

- HTTP
- HTTPS

Commonly associated with:

- Web applications
- Application-level traffic

### Memory Trick

ALB = Application / HTTP

---

## Network Load Balancer (NLB)

Operates at:

Layer 4

Designed for extremely high-performance network traffic.

Your notes associate NLB with:

- TCP
- Ultra-high performance
- Low latency

### Memory Trick

NLB = Network / Performance

---

## Gateway Load Balancer (GWLB)

Operates at:

Layer 3

Designed for integrating network appliances.

Think:

- Firewalls
- Security appliances

### Memory Trick

GWLB = Gateway Security

---

## ALB vs NLB vs GWLB

| Load Balancer | Layer | Think |
|---|---|---|
| ALB | Layer 7 | HTTP / HTTPS applications |
| NLB | Layer 4 | High-performance network traffic |
| GWLB | Layer 3 | Security/network appliances |

### Quick Memory Trick

ALB = Application

NLB = Network

GWLB = Gateway Security

---

## ELB and Auto Scaling Groups

ELB and Auto Scaling solve different problems.

### ELB

Distributes traffic.

### Auto Scaling Group

Adjusts the number of EC2 instances.

Together:

ASG

→ Makes sure enough instances exist

ELB

→ Distributes traffic between those instances

### Memory Trick

ASG = How Many Servers?

ELB = Where Does Traffic Go?

---

## ELB vs Auto Scaling

| Service | Primary Purpose |
|---|---|
| ELB | Distribute traffic |
| Auto Scaling | Adjust capacity |
| ELB + ASG | Scalability + High Availability |

---

## ELB vs Route 53

### ELB

Distributes application traffic across targets.

### Route 53

Provides DNS and routing.

### Memory Trick

Route 53 = Find the Destination

ELB = Distribute the Traffic

See:

[Route 53](<05-Networking/Route 53.md>)

---

## ELB vs CloudFront

### ELB

Distributes traffic between application resources.

### CloudFront

Delivers and caches content closer to users through edge locations.

### Memory Trick

ELB = Distribute Traffic

CloudFront = Deliver Content Globally

See:

[CloudFront](05-Networking/CloudFront.md)

---

## Common Use Cases

- Web applications
- Multi-server applications
- Highly available applications
- Applications using Auto Scaling
- Distributing traffic across EC2 instances

---

## Scenario Questions

A company wants to distribute incoming traffic across multiple EC2 instances.

→ Elastic Load Balancer

---

A company wants a single DNS endpoint in front of multiple application servers.

→ Elastic Load Balancer

---

One EC2 instance becomes unhealthy and traffic should automatically stop being sent to it.

→ ELB Health Checks

---

A web application needs HTTP/HTTPS load balancing.

→ Application Load Balancer

---

An application needs ultra-high-performance network load balancing.

→ Network Load Balancer

---

A company needs a load balancer for network security appliances.

→ Gateway Load Balancer

---

A company needs servers automatically added or removed based on demand.

→ Auto Scaling Group

NOT ELB

---

## Don't Confuse These

ELB = Distribute Traffic

ASG = Adjust Number of Servers

Route 53 = DNS

CloudFront = CDN / Content Delivery

ALB = HTTP / HTTPS

NLB = High-Performance Network Traffic

GWLB = Security Appliances

---

## Exam Keywords

Load Balancing

Traffic Distribution

Health Checks

Single DNS Endpoint

High Availability

Multi-AZ

SSL Termination

ALB

NLB

GWLB

---

## Memory Tricks

ELB = Spread Traffic Around

ALB = Application

NLB = Network

GWLB = Gateway Security

ASG = How Many Servers?

ELB = Where Does Traffic Go?

Route 53 = DNS

CloudFront = Content Delivery