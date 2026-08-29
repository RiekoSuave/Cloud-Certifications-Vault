## What Problem Does It Solve?

Some applications do not need:

SMART HTTP ROUTING

Instead, they need:

EXTREMELY HIGH PERFORMANCE

↓

VERY LOW LATENCY

↓

TCP / UDP TRAFFIC

↓

STATIC IP ADDRESSES

The:

NETWORK LOAD BALANCER

or:

NLB

solves this problem.

### Memory Trick

NLB

=

NETWORK SPEED

---

## What Is a Network Load Balancer?

Network Load Balancer operates at:

LAYER 4

of the OSI model.

Layer 4 deals with:

TCP

UDP

and:

TLS

Think:

CLIENT

↓

TCP / UDP

↓

NLB

↓

TARGETS

### Memory Trick

NLB = LAYER 4

---

## NLB vs ALB Layer

This is one of the most important Load Balancer distinctions.

### Application Load Balancer

LAYER 7

↓

HTTP / HTTPS

↓

APPLICATION-AWARE ROUTING

### Network Load Balancer

LAYER 4

↓

TCP / UDP

↓

NETWORK CONNECTION ROUTING

Think:

HTTP REQUEST DETAILS?

↓

ALB

RAW NETWORK TRAFFIC?

↓

NLB

### Memory Trick

ALB = APPLICATION

NLB = NETWORK

---

## NLB Performance

Network Load Balancer is designed for:

EXTREME PERFORMANCE

Your course emphasizes that NLB can handle:

MILLIONS OF REQUESTS PER SECOND

while maintaining:

ULTRA-LOW LATENCY

Think:

MASSIVE TRAFFIC

↓

NLB

↓

VERY LOW LATENCY

### Memory Trick

NLB

=

MILLIONS + LOW LATENCY

---

## NLB Architecture

A typical architecture looks like:

CLIENTS

↓

NETWORK LOAD BALANCER

↓

TARGET GROUP

↓

EC2 #1

EC2 #2

EC2 #3

Think:

NETWORK CONNECTIONS

↓

NLB

↓

HEALTHY TARGETS

---

## NLB Target Groups

Like ALB, Network Load Balancer uses:

TARGET GROUPS

Think:

NLB

↓

TARGET GROUP

↓

BACKEND TARGETS

NLB Target Groups can contain resources such as:

EC2 INSTANCES

↓

IP ADDRESSES

↓

APPLICATION LOAD BALANCER

The exact supported target depends on the Target Group configuration.

### Memory Trick

NLB

↓

TARGET GROUP

↓

NETWORK TARGET

---

## NLB and TCP

NLB is commonly used for:

TCP TRAFFIC

Think:

CLIENT

↓

TCP CONNECTION

↓

NLB

↓

BACKEND SERVER

Use NLB when the application needs:

LAYER 4

rather than application-level HTTP routing.

---

## NLB and UDP

Network Load Balancer also supports:

UDP

Think:

CLIENT

↓

UDP

↓

NLB

↓

TARGET

This is an important difference from:

[[Application Load Balancer]]

which focuses on:

HTTP / HTTPS

### Memory Trick

TCP / UDP

=

NLB

---

## NLB and TLS

Network Load Balancer can also support:

TLS

Think:

CLIENT

↓

TLS

↓

NLB

↓

TARGET

This allows NLB to provide high-performance encrypted network connections.

---

## Static IP Addresses

One of the most important NLB features for the SAA exam is:

STATIC IP

A Network Load Balancer has:

ONE STATIC IP

PER AVAILABILITY ZONE

Think:

AZ-A

↓

NLB STATIC IP

AZ-B

↓

NLB STATIC IP

### Memory Trick

NLB = STATIC IP

---

## Elastic IP Support

Network Load Balancer also supports:

ELASTIC IP

for each enabled Availability Zone.

Think:

NEED KNOWN PUBLIC IP

↓

NLB

↓

ELASTIC IP

This is especially useful when clients or firewalls require:

IP WHITELISTING

### Memory Trick

FIXED IP REQUIRED?

↓

NLB

---

## NLB vs ALB Addressing

### ALB

FIXED DNS NAME

but:

NO FIXED STATIC IP ADDRESS

### NLB

FIXED DNS NAME

+

STATIC IP PER AZ

and can use:

ELASTIC IP

Think:

SMART HTTP ROUTING

↓

ALB

STATIC IP

↓

NLB

---

## Source IP Preservation

With NLB, the backend can receive the:

CLIENT SOURCE IP

Think:

CLIENT IP

↓

NLB

↓

TARGET

↓

CLIENT IP PRESERVED

This differs from the common ALB behavior where the application uses:

X-FORWARDED-FOR

to determine the original client IP.

### Memory Trick

NLB

=

SOURCE IP PRESERVED

ALB

=

X-FORWARDED-FOR

---

## NLB Health Checks

Network Load Balancer performs:

HEALTH CHECKS

on registered targets.

Health checks can use protocols such as:

TCP

HTTP

HTTPS

Think:

NLB

↓

IS TARGET HEALTHY?

↓

YES

↓

SEND TRAFFIC

or:

NO

↓

STOP SENDING TRAFFIC

### Memory Trick

NLB

=

TRAFFIC ONLY TO HEALTHY TARGETS

---

## NLB Across Availability Zones

Network Load Balancer can operate across:

MULTIPLE AVAILABILITY ZONES

Think:

CLIENTS

↓

NLB

↓

AZ-A

TARGETS

+

AZ-B

TARGETS

This contributes to:

HIGH AVAILABILITY

---

## NLB and Target Availability

If a target becomes:

UNHEALTHY

NLB stops routing new traffic to that target.

Think:

TARGET FAILS

↓

HEALTH CHECK FAILS

↓

NLB REMOVES TARGET FROM TRAFFIC

↓

OTHER HEALTHY TARGETS CONTINUE

---

## NLB and Security Groups

Network Load Balancers support:

SECURITY GROUPS

Think:

CLIENT

↓

NLB SECURITY GROUP

↓

NLB

↓

TARGET SECURITY GROUP

This allows you to control which traffic can reach the NLB and helps restrict backend targets to traffic coming through the Load Balancer.

### Memory Trick

NLB NETWORK ACCESS

=

SECURITY GROUP

---

## NLB and Application Load Balancer

An interesting architecture is:

NLB

↓

ALB

↓

APPLICATION TARGETS

Why?

NLB provides features such as:

STATIC IP ADDRESSES

while ALB provides:

LAYER 7 HTTP ROUTING

Think:

NLB

=

STATIC IP + LAYER 4

↓

ALB

=

SMART HTTP ROUTING

↓

APPLICATION

### Memory Trick

NEED NLB FEATURES + ALB FEATURES?

↓

NLB → ALB

---

## When Would You Choose NLB?

Choose NLB when the requirement emphasizes:

EXTREME PERFORMANCE

↓

TCP / UDP

↓

LOW LATENCY

↓

STATIC IP

↓

ELASTIC IP

Think:

NETWORK-LEVEL REQUIREMENTS

↓

NLB

---

## ALB vs NLB

### ALB

LAYER

=

7

PROTOCOL

=

HTTP / HTTPS

ROUTING

=

PATH / HOST / HTTP INFORMATION

STATIC IP

=

NO

BEST FOR

=

WEB APPLICATIONS / MICROSERVICES

---

### NLB

LAYER

=

4

PROTOCOL

=

TCP / UDP / TLS

ROUTING

=

NETWORK CONNECTIONS

STATIC IP

=

YES

BEST FOR

=

EXTREME PERFORMANCE / LOW LATENCY

---

## Architecture Thinking

Imagine an application requires:

MILLIONS OF CONNECTIONS

and customers must whitelist:

KNOWN IP ADDRESSES

Think:

CLIENTS

↓

KNOWN STATIC IP

↓

NLB

↓

AZ-A TARGETS

+

AZ-B TARGETS

The clues:

MILLIONS OF REQUESTS

+

ULTRA-LOW LATENCY

+

STATIC IP

↓

NETWORK LOAD BALANCER

---

## Scenario Recognition

Need Layer 4 load balancing?

→ Network Load Balancer

---

Need TCP traffic load balanced?

→ Network Load Balancer

---

Need UDP traffic load balanced?

→ Network Load Balancer

---

Need millions of requests per second?

→ Network Load Balancer

---

Need ultra-low latency?

→ Network Load Balancer

---

Need a static IP address for a Load Balancer?

→ Network Load Balancer

---

Need one static IP per Availability Zone?

→ Network Load Balancer

---

Need Elastic IP support for a Load Balancer?

→ Network Load Balancer

---

Need customers to whitelist your Load Balancer IP addresses?

→ Network Load Balancer

---

Need original client source IP preserved?

→ Network Load Balancer

---

Need path-based routing?

→ Application Load Balancer

NOT NLB

---

Need host-based HTTP routing?

→ Application Load Balancer

NOT NLB

---

Need static IP plus advanced HTTP routing?

→ NLB in front of ALB

---

## Exam Traps

NLB

=

LAYER 4

ALB

=

LAYER 7

---

NLB

=

TCP / UDP / TLS

ALB

=

HTTP / HTTPS

---

NLB

=

EXTREME PERFORMANCE

---

NLB

=

MILLIONS OF REQUESTS PER SECOND

---

NLB

=

ULTRA-LOW LATENCY

---

NLB

=

STATIC IP PER AZ

---

NLB

=

ELASTIC IP SUPPORT

---

ALB

≠

STATIC IP

---

PATH-BASED ROUTING

≠

NLB

PATH-BASED ROUTING

=

ALB

---

HOST-BASED ROUTING

≠

NLB

HOST-BASED ROUTING

=

ALB

---

NLB

=

CLIENT SOURCE IP PRESERVED

ALB

=

X-FORWARDED-FOR

---

## Quick Cheat Sheet

NLB

=

NETWORK LOAD BALANCER

OSI LAYER

=

LAYER 4

PROTOCOLS

=

TCP / UDP / TLS

PERFORMANCE

=

EXTREME

LATENCY

=

ULTRA-LOW

TRAFFIC

=

MILLIONS OF REQUESTS PER SECOND

STATIC IP

=

YES

STATIC IP PER AZ

=

YES

ELASTIC IP

=

SUPPORTED

SOURCE IP

=

PRESERVED

TARGET GROUPS

=

YES

HEALTH CHECKS

=

YES

MULTI-AZ

=

YES

SECURITY GROUPS

=

YES

PATH ROUTING

=

NO

HOST ROUTING

=

NO

SMART HTTP ROUTING

=

ALB

---

## Master Memory Trick

NLB

=

NETWORK

↓

LAYER 4

↓

TCP / UDP / TLS

↓

MILLIONS OF REQUESTS

↓

ULTRA-LOW LATENCY

↓

STATIC IP

Think:

NEED SMART HTTP?

↓

ALB

NEED RAW SPEED + STATIC IP?

↓

NLB

---

## Related Notes

- [[Scalability & High Availability]]
- [[Elastic Load Balancing]]
- [[Application Load Balancer]]
- [[Gateway Load Balancer]]
- [[Load Balancer Stickiness]]
- [[Cross-Zone Load Balancing]]
- [[Auto Scaling Groups]]
- [[Elastic IP]]
- [[EC2 Security Groups]]
- [[SAA High Availability Cheat Sheet]]