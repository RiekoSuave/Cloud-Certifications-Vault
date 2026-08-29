## What Problem Does It Solve?

Sometimes you need to inspect network traffic using:

THIRD-PARTY NETWORK APPLIANCES

Examples include:

FIREWALLS

↓

INTRUSION DETECTION / PREVENTION SYSTEMS

↓

DEEP PACKET INSPECTION

↓

TRAFFIC MONITORING

The problem is:

HOW DO YOU SEND NETWORK TRAFFIC THROUGH THESE APPLIANCES AT SCALE?

The:

GATEWAY LOAD BALANCER

or:

GWLB

solves this problem.

### Memory Trick

GWLB

=

LOAD BALANCE NETWORK APPLIANCES

---

## What Is a Gateway Load Balancer?

Gateway Load Balancer is designed to:

DEPLOY

↓

SCALE

↓

MANAGE

a fleet of:

THIRD-PARTY NETWORK VIRTUAL APPLIANCES

Think:

NETWORK TRAFFIC

↓

GWLB

↓

FIREWALL / IDS / IPS

↓

DESTINATION

### Memory Trick

GWLB = SECURITY APPLIANCE LOAD BALANCER

---

## GWLB Main Use Cases

Gateway Load Balancer is commonly used with:

FIREWALLS

↓

INTRUSION DETECTION SYSTEMS

↓

INTRUSION PREVENTION SYSTEMS

↓

DEEP PACKET INSPECTION SYSTEMS

↓

OTHER NETWORK VIRTUAL APPLIANCES

Think:

TRAFFIC NEEDS INSPECTION

↓

GWLB

↓

SECURITY APPLIANCES

---

## GWLB Architecture

A simplified architecture looks like:

USER

↓

NETWORK TRAFFIC

↓

GWLB

↓

VIRTUAL APPLIANCE

↓

APPLICATION

Think:

TRAFFIC

↓

INSPECT

↓

FORWARD

The network appliance can:

INSPECT

↓

ALLOW

↓

REJECT

or otherwise process the traffic.

---

## GWLB Has Two Main Functions

Gateway Load Balancer combines:

TRANSPARENT NETWORK GATEWAY

and:

LOAD BALANCER

Think:

GWLB

=

GATEWAY

+

LOAD BALANCER

### Gateway Function

GWLB provides:

A SINGLE ENTRY / EXIT POINT

for network traffic.

### Load Balancer Function

GWLB distributes traffic across:

MULTIPLE VIRTUAL APPLIANCES

### Memory Trick

GWLB

=

ROUTE TRAFFIC + BALANCE APPLIANCES

---

## Layer 3

Gateway Load Balancer operates at:

LAYER 3

of the OSI model.

Layer 3 is the:

NETWORK LAYER

Think:

GWLB

↓

IP PACKETS

↓

NETWORK APPLIANCES

### Memory Trick

GWLB = LAYER 3

---

## Load Balancer Layer Comparison

This is an important SAA distinction.

### Application Load Balancer

LAYER 7

↓

HTTP / HTTPS

### Network Load Balancer

LAYER 4

↓

TCP / UDP

### Gateway Load Balancer

LAYER 3

↓

IP PACKETS

Think:

ALB

=

APPLICATION

NLB

=

NETWORK CONNECTION

GWLB

=

NETWORK APPLIANCE TRAFFIC

---

## GENEVE Protocol

Gateway Load Balancer uses:

GENEVE

GENEVE stands for:

GENERIC NETWORK VIRTUALIZATION ENCAPSULATION

Your course emphasizes that GWLB uses:

PORT 6081

Think:

GWLB

↓

GENEVE

↓

PORT 6081

### Memory Trick

GWLB

=

GENEVE 6081

---

## Why GENEVE?

GWLB needs to send network traffic to:

VIRTUAL APPLIANCES

while preserving information about the original traffic.

GENEVE encapsulates the traffic so it can pass through the appliance infrastructure.

Think:

ORIGINAL PACKET

↓

GENEVE ENCAPSULATION

↓

NETWORK APPLIANCE

↓

PROCESS TRAFFIC

For the exam, remember:

GWLB

=

GENEVE

=

PORT 6081

---

## Gateway Load Balancer Target Groups

GWLB distributes traffic across:

TARGET GROUPS

The targets are typically:

VIRTUAL APPLIANCES

Think:

GWLB

↓

TARGET GROUP

↓

FIREWALL #1

FIREWALL #2

FIREWALL #3

This allows the appliance layer to:

SCALE HORIZONTALLY

---

## Scaling Network Appliances

Without GWLB:

TRAFFIC

↓

ONE FIREWALL APPLIANCE

↓

BOTTLENECK / FAILURE

With GWLB:

TRAFFIC

↓

GWLB

↓

FIREWALL #1

FIREWALL #2

FIREWALL #3

Think:

MORE TRAFFIC

↓

MORE APPLIANCES

↓

GWLB DISTRIBUTES TRAFFIC

### Memory Trick

GWLB

=

SCALE THE FIREWALL FLEET

---

## High Availability for Network Appliances

GWLB can distribute traffic across multiple:

VIRTUAL APPLIANCES

This removes dependence on:

ONE APPLIANCE

Think:

APPLIANCE #1 FAILS

↓

GWLB

↓

OTHER HEALTHY APPLIANCES

This helps create:

HIGHLY AVAILABLE

network inspection architectures.

---

## GWLB Health Checks

Gateway Load Balancer can perform:

HEALTH CHECKS

on its appliance targets.

Think:

GWLB

↓

IS APPLIANCE HEALTHY?

↓

YES

↓

SEND TRAFFIC

or:

NO

↓

STOP SENDING TRAFFIC

### Memory Trick

UNHEALTHY FIREWALL

=

NO TRAFFIC

---

## Transparent Traffic Inspection

A major benefit of GWLB is that network appliances can be inserted:

TRANSPARENTLY

into the traffic path.

Think:

APPLICATION TRAFFIC

↓

GWLB

↓

SECURITY APPLIANCE

↓

APPLICATION

The application does not need to understand how the appliance fleet is being scaled behind GWLB.

### Memory Trick

GWLB

=

TRANSPARENT INSPECTION

---

## Gateway Load Balancer Endpoint

Traffic reaches a Gateway Load Balancer architecture using:

GATEWAY LOAD BALANCER ENDPOINTS

or:

GWLBe

Think:

APPLICATION VPC

↓

GWLB ENDPOINT

↓

GWLB

↓

SECURITY APPLIANCES

A GWLB Endpoint is powered by:

AWS PRIVATELINK

### Memory Trick

GWLBe

=

PRIVATE ENTRY TO GWLB

---

## GWLB Endpoint Architecture

Think:

APPLICATION VPC

↓

GWLB ENDPOINT

↓

GWLB

↓

SECURITY VPC

↓

FIREWALL APPLIANCES

This architecture allows centralized security appliances to inspect traffic from other network environments.

---

## Centralized Network Inspection

GWLB is useful when an organization wants:

CENTRALIZED TRAFFIC INSPECTION

Think:

VPC #1

↘

VPC #2

→ GWLB → FIREWALL FLEET

VPC #3

↗

Instead of deploying separate inspection appliances everywhere:

CENTRALIZE

↓

SCALE

↓

INSPECT

### Memory Trick

GWLB

=

CENTRALIZED APPLIANCE FLEET

---

## Third-Party Virtual Appliances

The SAA course emphasizes GWLB for:

THIRD-PARTY VIRTUAL APPLIANCES

These can come from networking and security vendors.

Think:

AWS TRAFFIC

↓

GWLB

↓

VENDOR SECURITY APPLIANCE

GWLB manages the traffic distribution while the appliance performs the specialized network function.

---

## ALB vs NLB vs GWLB

### ALB

LAYER

=

7

TRAFFIC

=

HTTP / HTTPS

BEST FOR

=

WEB APPLICATIONS

SMART ROUTING

=

YES

Think:

WEBSITE

↓

ALB

---

### NLB

LAYER

=

4

TRAFFIC

=

TCP / UDP

BEST FOR

=

EXTREME PERFORMANCE

STATIC IP

=

YES

Think:

NETWORK PERFORMANCE

↓

NLB

---

### GWLB

LAYER

=

3

TRAFFIC

=

IP PACKETS

PROTOCOL

=

GENEVE PORT 6081

BEST FOR

=

NETWORK VIRTUAL APPLIANCES

Think:

FIREWALL / IDS / IPS

↓

GWLB

---

## Architecture Thinking

Imagine a company requires:

ALL APPLICATION TRAFFIC

to pass through:

THIRD-PARTY FIREWALLS

The architecture could be:

APPLICATION TRAFFIC

↓

GWLB ENDPOINT

↓

GATEWAY LOAD BALANCER

↓

FIREWALL TARGET GROUP

↓

FIREWALL #1

FIREWALL #2

FIREWALL #3

↓

INSPECTED TRAFFIC

Think:

GWLB

=

THE TRAFFIC DISTRIBUTOR FOR SECURITY APPLIANCES

---

## Scenario Recognition

Need to deploy and scale third-party virtual firewalls?

→ Gateway Load Balancer

---

Need traffic distributed across multiple security appliances?

→ Gateway Load Balancer

---

Need intrusion detection appliances inserted into the network path?

→ Gateway Load Balancer

---

Need intrusion prevention appliances?

→ Gateway Load Balancer

---

Need deep packet inspection?

→ Gateway Load Balancer

---

Need transparent network traffic inspection?

→ Gateway Load Balancer

---

Need centralized virtual network appliances?

→ Gateway Load Balancer

---

Need Layer 3 Load Balancing?

→ Gateway Load Balancer

---

Need GENEVE protocol?

→ Gateway Load Balancer

---

Need port 6081?

→ Gateway Load Balancer

---

Need HTTP path-based routing?

→ Application Load Balancer

NOT GWLB

---

Need extreme TCP/UDP performance with static IP?

→ Network Load Balancer

NOT GWLB

---

## Exam Traps

GWLB

=

GATEWAY LOAD BALANCER

---

GWLB

=

LAYER 3

---

GWLB

=

NETWORK VIRTUAL APPLIANCES

---

GWLB

=

FIREWALLS

IDS

IPS

DEEP PACKET INSPECTION

---

GWLB

=

GENEVE

---

GENEVE

=

PORT 6081

---

GWLB

=

GATEWAY + LOAD BALANCER

---

GWLB

≠

WEB APPLICATION LOAD BALANCER

HTTP / HTTPS ROUTING

=

ALB

---

GWLB

≠

HIGH-PERFORMANCE TCP / UDP LOAD BALANCER

TCP / UDP + STATIC IP

=

NLB

---

GWLBe

=

GATEWAY LOAD BALANCER ENDPOINT

---

GWLB ENDPOINT

=

AWS PRIVATELINK

---

## Quick Cheat Sheet

GWLB

=

GATEWAY LOAD BALANCER

OSI LAYER

=

LAYER 3

PURPOSE

=

LOAD BALANCE NETWORK APPLIANCES

APPLIANCES

=

FIREWALL

IDS

IPS

DEEP PACKET INSPECTION

PROTOCOL

=

GENEVE

PORT

=

6081

FUNCTION

=

GATEWAY + LOAD BALANCER

TRAFFIC INSPECTION

=

TRANSPARENT

TARGETS

=

VIRTUAL APPLIANCES

HEALTH CHECKS

=

YES

GWLBe

=

GWLB ENDPOINT

GWLBe TECHNOLOGY

=

PRIVATELINK

ALB

=

LAYER 7

NLB

=

LAYER 4

GWLB

=

LAYER 3

---

## Master Memory Trick

ALB

=

WEB TRAFFIC

↓

LAYER 7

NLB

=

NETWORK PERFORMANCE

↓

LAYER 4

GWLB

=

NETWORK SECURITY APPLIANCES

↓

LAYER 3

And:

GWLB

↓

GENEVE

↓

6081

Think:

TRAFFIC NEEDS FIREWALL INSPECTION?

↓

GWLB

↓

BALANCE ACROSS FIREWALL FLEET

↓

HEALTHY APPLIANCES

↓

INSPECT TRAFFIC

---

## Related Notes

- [[Scalability & High Availability]]
- [[Elastic Load Balancing]]
- [[Application Load Balancer]]
- [[Network Load Balancer]]
- [[Load Balancer Stickiness]]
- [[Cross-Zone Load Balancing]]
- [[Auto Scaling Groups]]
- [[05-Networking/VPC]]
- [[AWS PrivateLink]]
- [[SAA High Availability Cheat Sheet]]