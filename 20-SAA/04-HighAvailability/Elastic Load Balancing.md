## What Problem Does It Solve?

When an application runs on multiple EC2 instances, users need a way to:

DISTRIBUTE TRAFFIC

across those instances.

Without a Load Balancer:

USERS

↓

ONE EC2 INSTANCE

↓

OVERLOADED / FAILURE

With a Load Balancer:

USERS

↓

LOAD BALANCER

↓

EC2 #1

EC2 #2

EC2 #3

### Memory Trick

LOAD BALANCER = TRAFFIC DISTRIBUTOR

---

## What Is Elastic Load Balancing?

Elastic Load Balancing distributes incoming application traffic across multiple:

DOWNSTREAM INSTANCES

such as:

EC2 INSTANCES

Think:

CLIENTS

↓

LOAD BALANCER

↓

EC2 INSTANCES

The goal is to prevent one server from handling all incoming traffic.

### Memory Trick

ELB

=

SPREAD THE LOAD

---

## Why Use a Load Balancer?

A Load Balancer can:

- Spread traffic across multiple downstream instances
- Expose a single DNS endpoint for your application
- Handle failures of downstream instances
- Perform health checks
- Provide SSL termination
- Provide High Availability across Availability Zones
- Separate public traffic from backend EC2 instances

Think:

USERS

↓

ONE ENTRY POINT

↓

LOAD BALANCER

↓

MANY SERVERS

---

## Single DNS Endpoint

Users do not need to know the IP addresses of individual EC2 instances.

Instead:

USER

↓

LOAD BALANCER DNS NAME

↓

EC2 INSTANCES

Think:

MANY BACKEND SERVERS

↓

ONE FRONT DOOR

### Memory Trick

ELB = ONE DNS ENTRY POINT

---

## Load Balancing Across EC2 Instances

Imagine three EC2 instances:

EC2 #1

EC2 #2

EC2 #3

Without a Load Balancer:

CLIENT

↓

MUST KNOW WHICH EC2 TO CONTACT

With a Load Balancer:

CLIENT

↓

ELB

↓

EC2 #1 / EC2 #2 / EC2 #3

The Load Balancer decides where traffic should go.

---

## Load Balancing + Horizontal Scaling

Remember:

HORIZONTAL SCALING

=

ADD MORE INSTANCES

Think:

EC2

↓

EC2 EC2 EC2

But adding instances creates another problem:

HOW DOES TRAFFIC REACH THEM?

↓

LOAD BALANCER

Think:

HORIZONTAL SCALING

+

LOAD BALANCER

↓

SCALABLE APPLICATION

---

## Load Balancing + High Availability

Load Balancers can distribute traffic across:

MULTIPLE AVAILABILITY ZONES

Think:

USERS

↓

LOAD BALANCER

↓

AZ-A

EC2

+

AZ-B

EC2

If an instance or Availability Zone has problems:

TRAFFIC

↓

HEALTHY RESOURCES

### Memory Trick

ELB + MULTI-AZ

=

HIGH AVAILABILITY

---

## Handling EC2 Failures

Imagine:

LOAD BALANCER

↓

EC2 #1

EC2 #2

EC2 #3

If:

EC2 #2 FAILS

the Load Balancer can stop sending traffic to that unhealthy instance.

Think:

EC2 #2

↓

UNHEALTHY

↓

NO NEW TRAFFIC

Traffic continues to:

EC2 #1

and

EC2 #3

This improves:

APPLICATION AVAILABILITY

---

## Load Balancer Health Checks

Load Balancers perform:

HEALTH CHECKS

to determine whether backend instances can successfully handle traffic.

Think:

LOAD BALANCER

↓

ARE YOU HEALTHY?

↓

EC2

If:

HEALTH CHECK PASSES

↓

SEND TRAFFIC

If:

HEALTH CHECK FAILS

↓

STOP SENDING TRAFFIC

### Memory Trick

HEALTH CHECK

=

CAN THIS SERVER RECEIVE TRAFFIC?

---

## Health Check Protocol

Health checks are commonly performed using:

HTTP

with a:

PORT

and

ROUTE

Example:

PROTOCOL

↓

HTTP

PORT

↓

4567

ENDPOINT

↓

/health

Think:

ELB

↓

HTTP : 4567 /health

↓

EC2

---

## Health Check Response

If the health check endpoint returns a successful response:

INSTANCE

=

HEALTHY

If the instance does not respond correctly:

INSTANCE

=

UNHEALTHY

Think:

/health

↓

SUCCESS

↓

KEEP SENDING TRAFFIC

or:

/health

↓

FAILURE

↓

STOP SENDING TRAFFIC

---

## SSL / TLS Termination

A Load Balancer can also handle:

SSL / TLS

for incoming connections.

Think:

USER

↓

HTTPS

↓

LOAD BALANCER

↓

BACKEND APPLICATION

This allows the Load Balancer to handle certificate-related work instead of requiring every backend server to independently handle the public SSL connection.

### Memory Trick

SSL TERMINATION

=

ELB HANDLES HTTPS

---

## Load Balancers Are Managed by AWS

Elastic Load Balancing is:

FULLY MANAGED

AWS handles the underlying Load Balancer infrastructure.

Think:

YOU

↓

CONFIGURE LOAD BALANCER

AWS

↓

MANAGES INFRASTRUCTURE

AWS handles things such as:

- Availability
- Maintenance
- Upgrades
- Underlying infrastructure

### Memory Trick

ELB = AWS MANAGED

---

## Why Not Build Your Own Load Balancer?

You could technically run your own load balancing software on EC2.

But then you would be responsible for:

INSTALLATION

↓

SCALING

↓

MAINTENANCE

↓

HIGH AVAILABILITY

↓

UPGRADES

With ELB:

AWS

↓

MANAGES LOAD BALANCER

For SAA architecture questions:

MANAGED AWS LOAD BALANCER

is usually preferred over building your own.

---

## Load Balancer Security Groups

Load Balancers use:

SECURITY GROUPS

Think:

INTERNET

↓

LOAD BALANCER SECURITY GROUP

↓

LOAD BALANCER

↓

EC2 SECURITY GROUP

A common architecture is:

USER

↓

HTTP / HTTPS

↓

LOAD BALANCER

↓

EC2

---

## Security Group Referencing

A powerful architecture pattern is allowing EC2 traffic only from:

THE LOAD BALANCER SECURITY GROUP

Think:

INTERNET

↓

LOAD BALANCER SG

↓

ELB

↓

EC2 SG

The EC2 Security Group can say:

ALLOW TRAFFIC

FROM

LOAD BALANCER SECURITY GROUP

This prevents users from directly accessing the backend EC2 instances through the application port.

### Memory Trick

USER

↓

ELB

↓

EC2

NOT:

USER

↓

EC2 DIRECTLY

---

## ELB Architecture Thinking

A common architecture is:

INTERNET

↓

LOAD BALANCER

↓

AZ-A

EC2 #1

EC2 #2

+

AZ-B

EC2 #3

EC2 #4

The Load Balancer provides:

ONE ENTRY POINT

↓

TRAFFIC DISTRIBUTION

↓

HEALTH CHECKS

↓

FAILURE HANDLING

↓

MULTI-AZ AVAILABILITY

---

## ELB + Auto Scaling

Load Balancers are commonly combined with:

[[Auto Scaling Groups]]

Think:

TRAFFIC ↑

↓

AUTO SCALING GROUP

↓

ADD EC2

↓

LOAD BALANCER

↓

DISTRIBUTE TRAFFIC

When traffic decreases:

TRAFFIC ↓

↓

ASG REMOVES EC2

The Load Balancer continues routing traffic to the remaining healthy instances.

### Memory Trick

ELB

=

DISTRIBUTE

ASG

=

SCALE

---

## Types of AWS Load Balancers

AWS provides multiple generations and types of Load Balancers.

Your course introduces:

CLASSIC LOAD BALANCER

↓

CLB

APPLICATION LOAD BALANCER

↓

ALB

NETWORK LOAD BALANCER

↓

NLB

GATEWAY LOAD BALANCER

↓

GWLB

Think:

CLB

=

OLD GENERATION

ALB / NLB / GWLB

=

NEWER GENERATION

We'll separate these into their appropriate notes as we continue through the section.

---

## Layer 4 vs Layer 7 Preview

An important distinction is:

LAYER 7

↓

HTTP / HTTPS

and:

LAYER 4

↓

TCP / UDP

Think:

HTTP ROUTING

↓

APPLICATION LOAD BALANCER

TCP / UDP PERFORMANCE

↓

NETWORK LOAD BALANCER

We'll cover the details in:

[[Application Load Balancer]]

and:

[[Network Load Balancer]]

---

## Scenario Recognition

Need to distribute traffic across multiple EC2 instances?

→ Elastic Load Balancing

---

Need one DNS endpoint in front of multiple EC2 instances?

→ Load Balancer

---

Need to stop sending traffic to unhealthy EC2 instances?

→ Load Balancer Health Checks

---

Need an application to span multiple Availability Zones?

→ Load Balancer + Multi-AZ architecture

---

Need to horizontally scale EC2 while distributing traffic?

→ ELB + Auto Scaling Group

---

Need SSL/TLS termination before traffic reaches backend servers?

→ Load Balancer

---

Need backend EC2 instances accessible only through the Load Balancer?

→ EC2 Security Group references Load Balancer Security Group

---

Need AWS to manage the load balancing infrastructure?

→ Elastic Load Balancing

---

Need HTTP/HTTPS intelligent routing?

→ Application Load Balancer

---

Need high-performance TCP/UDP load balancing?

→ Network Load Balancer

---

## Exam Traps

ELB

=

DISTRIBUTE TRAFFIC

ELB

≠

AUTO SCALING

ELB

=

SEND TRAFFIC TO INSTANCES

ASG

=

ADD / REMOVE INSTANCES

---

LOAD BALANCER

=

ONE DNS ENDPOINT

---

UNHEALTHY INSTANCE

=

STOP RECEIVING TRAFFIC

---

HEALTH CHECK

=

DETERMINES BACKEND HEALTH

---

ELB

=

AWS MANAGED

---

MULTI-AZ ELB ARCHITECTURE

=

HIGH AVAILABILITY

---

LOAD BALANCER SECURITY GROUP

↓

CAN BE REFERENCED BY

↓

EC2 SECURITY GROUP

---

ALB

=

LAYER 7

NLB

=

LAYER 4

---

## Quick Cheat Sheet

ELB

=

ELASTIC LOAD BALANCING

PURPOSE

=

DISTRIBUTE TRAFFIC

FRONT END

=

ONE DNS ENDPOINT

BACK END

=

MULTIPLE TARGETS

UNHEALTHY TARGET

=

NO TRAFFIC

HEALTH CHECK

=

CHECK BACKEND HEALTH

MULTI-AZ

=

HIGH AVAILABILITY

SSL / TLS TERMINATION

=

SUPPORTED

MANAGEMENT

=

AWS MANAGED

ELB

=

DISTRIBUTE

ASG

=

SCALE

ALB

=

HTTP / HTTPS

NLB

=

TCP / UDP

---

## Master Memory Trick

USERS

↓

ELB

↓

HEALTHY EC2 INSTANCES

Think:

ELB

=

ONE FRONT DOOR

↓

CHECK HEALTH

↓

SPREAD TRAFFIC

↓

MULTIPLE SERVERS

↓

MULTIPLE AZs

And:

ELB

=

DISTRIBUTE

ASG

=

SCALE

---

## Related Notes

- [[Scalability & High Availability]]
- [[EC2]]
- [[EC2 Security Groups]]
- [[Application Load Balancer]]
- [[Network Load Balancer]]
- [[Gateway Load Balancer]]
- [[Load Balancer Stickiness]]
- [[Cross-Zone Load Balancing]]
- [[Auto Scaling Groups]]
- [[SAA High Availability Cheat Sheet]]