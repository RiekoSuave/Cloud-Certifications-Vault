## What Problem Does It Solve?

This note helps answer:

HOW DO I BUILD AN APPLICATION THAT:

SCALES

↓

STAYS AVAILABLE

↓

DISTRIBUTES TRAFFIC

↓

REPLACES FAILED INSTANCES

Think:

MORE USERS?

↓

SCALE

INSTANCE FAILS?

↓

REPLACE

AZ FAILS?

↓

USE MULTI-AZ

TRAFFIC NEEDS DISTRIBUTION?

↓

LOAD BALANCER

### Memory Trick

HIGH AVAILABILITY

=

KEEP THE APPLICATION RUNNING

---

## Master High Availability Map

Need:

HANDLE MORE LOAD

↓

SCALABILITY

Need:

BIGGER INSTANCE

↓

VERTICAL SCALING

Need:

MORE INSTANCES

↓

HORIZONTAL SCALING

Need:

SURVIVE AZ FAILURE

↓

HIGH AVAILABILITY

Need:

AUTOMATIC CAPACITY CHANGES

↓

AUTO SCALING GROUP

Need:

DISTRIBUTE TRAFFIC

↓

ELASTIC LOAD BALANCING

Need:

HTTP / HTTPS SMART ROUTING

↓

APPLICATION LOAD BALANCER

Need:

TCP / UDP + STATIC IP

↓

NETWORK LOAD BALANCER

Need:

NETWORK APPLIANCE INSPECTION

↓

GATEWAY LOAD BALANCER

---

## Scalability

Scalability means:

HANDLE GREATER LOAD

Think:

LOAD ↑

↓

CAPACITY ↑

There are two major types:

VERTICAL

and:

HORIZONTAL

### Memory Trick

SCALABILITY

=

HANDLE MORE

---

## Vertical Scaling

Vertical Scaling means:

MAKE ONE INSTANCE BIGGER

Think:

t2.micro

↓

t2.large

Think:

MORE CPU

+

MORE RAM

### Memory Trick

VERTICAL

=

SCALE UP

---

## Horizontal Scaling

Horizontal Scaling means:

ADD MORE INSTANCES

Think:

1 EC2

↓

3 EC2

↓

10 EC2

### Memory Trick

HORIZONTAL

=

SCALE OUT

---

## Vertical vs Horizontal

VERTICAL

=

BIGGER SERVER

HORIZONTAL

=

MORE SERVERS

Think:

DATABASE

↓

OFTEN VERTICAL

WEB APPLICATION

↓

OFTEN HORIZONTAL

---

## High Availability

High Availability means:

RUN APPLICATION ACROSS MULTIPLE AVAILABILITY ZONES

Think:

AZ-A

↓

APPLICATION

+

AZ-B

↓

APPLICATION

If:

AZ-A FAILS

↓

AZ-B CONTINUES

### Memory Trick

HIGH AVAILABILITY

=

SURVIVE AZ FAILURE

---

## Scalability vs High Availability

SCALABILITY

=

HANDLE LOAD

HIGH AVAILABILITY

=

SURVIVE FAILURE

Think:

MORE USERS

↓

SCALABILITY

DATA CENTER FAILURE

↓

HIGH AVAILABILITY

---

## Elasticity

Elasticity means:

AUTOMATICALLY MATCH CAPACITY TO DEMAND

Think:

TRAFFIC ↑

↓

ADD RESOURCES

TRAFFIC ↓

↓

REMOVE RESOURCES

### Memory Trick

ELASTICITY

=

AUTO GROW + SHRINK

---

## Agility

Agility means:

CREATE IT RESOURCES QUICKLY

Think:

WEEKS

↓

BECOME

↓

MINUTES

### Memory Trick

AGILITY

=

MOVE FAST

---

## Elastic Load Balancing

ELB provides:

TRAFFIC DISTRIBUTION

Think:

USERS

↓

LOAD BALANCER

↓

EC2 #1

EC2 #2

EC2 #3

ELB provides:

- Single DNS endpoint
- Health checks
- Failure handling
- Multi-AZ traffic distribution
- SSL/TLS termination

### Memory Trick

ELB

=

DISTRIBUTE

---

## ELB vs ASG

Do not confuse:

ELB

and:

ASG

### ELB

DISTRIBUTES TRAFFIC

### ASG

CHANGES NUMBER OF EC2 INSTANCES

Think:

ELB

=

WHERE TRAFFIC GOES

ASG

=

HOW MANY SERVERS EXIST

### Memory Trick

ELB

=

DISTRIBUTE

ASG

=

SCALE

---

## Load Balancer Health Checks

Load Balancers monitor:

TARGET HEALTH

Think:

HEALTHY TARGET

↓

SEND TRAFFIC

UNHEALTHY TARGET

↓

STOP TRAFFIC

Example:

HTTP

↓

/health

↓

TARGET

### Memory Trick

HEALTH CHECK

=

CAN THIS TARGET SERVE TRAFFIC?

---

## Application Load Balancer

Application Load Balancer operates at:

LAYER 7

Think:

HTTP

HTTPS

↓

ALB

ALB supports:

SMART HTTP ROUTING

including:

PATH

↓

HOSTNAME

↓

QUERY STRING

↓

HTTP HEADER

### Memory Trick

ALB

=

SMART HTTP ROUTER

---

## ALB Path-Based Routing

Example:

/users

↓

USER TARGET GROUP

/products

↓

PRODUCT TARGET GROUP

Think:

URL PATH

↓

CHOOSE APPLICATION

### Memory Trick

PATH ROUTING

=

ALB

---

## ALB Host-Based Routing

Example:

shop.example.com

↓

SHOP TARGET GROUP

api.example.com

↓

API TARGET GROUP

Think:

HOSTNAME

↓

CHOOSE APPLICATION

### Memory Trick

HOST ROUTING

=

ALB

---

## ALB Target Groups

ALB routes traffic to:

TARGET GROUPS

Targets can include:

EC2

↓

ECS TASKS

↓

LAMBDA

↓

PRIVATE IP ADDRESSES

Think:

ALB

↓

TARGET GROUP

↓

APPLICATION TARGETS

---

## ALB Client IP

The original client IP is provided through:

X-FORWARDED-FOR

Think:

CLIENT IP

↓

ALB

↓

X-FORWARDED-FOR

↓

APPLICATION

### Memory Trick

ALB CLIENT IP

=

X-FORWARDED-FOR

---

## Network Load Balancer

Network Load Balancer operates at:

LAYER 4

Think:

TCP

UDP

TLS

↓

NLB

NLB is designed for:

EXTREME PERFORMANCE

+

ULTRA-LOW LATENCY

### Memory Trick

NLB

=

NETWORK SPEED

---

## NLB Static IP

NLB provides:

STATIC IP

per:

AVAILABILITY ZONE

It can also use:

ELASTIC IP

Think:

NEED FIXED IP?

↓

NLB

### Memory Trick

NLB

=

STATIC IP

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

SMART HTTP

STATIC IP

=

NO

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

NETWORK CONNECTION

STATIC IP

=

YES

### Memory Trick

ALB

=

SMART

NLB

=

FAST

---

## Gateway Load Balancer

Gateway Load Balancer operates at:

LAYER 3

It is designed for:

NETWORK VIRTUAL APPLIANCES

such as:

FIREWALLS

↓

IDS

↓

IPS

↓

DEEP PACKET INSPECTION

Think:

NETWORK TRAFFIC

↓

GWLB

↓

SECURITY APPLIANCE

### Memory Trick

GWLB

=

SECURITY APPLIANCE LOAD BALANCER

---

## GWLB Protocol

GWLB uses:

GENEVE

on:

PORT 6081

Think:

GWLB

↓

GENEVE

↓

6081

### Memory Trick

GWLB

=

GENEVE 6081

---

## ALB vs NLB vs GWLB

ALB

=

LAYER 7

↓

HTTP / HTTPS

NLB

=

LAYER 4

↓

TCP / UDP

GWLB

=

LAYER 3

↓

NETWORK APPLIANCES

### Master Memory Trick

7

=

APPLICATION

4

=

NETWORK CONNECTION

3

=

NETWORK APPLIANCE

---

## Load Balancer Stickiness

Stickiness means:

SAME CLIENT

↓

SAME TARGET

Think:

USER

↓

ALB

↓

EC2 #1

↓

COOKIE

↓

USER RETURNS

↓

EC2 #1 AGAIN

### Memory Trick

STICKINESS

=

SAME USER → SAME SERVER

---

## Stickiness Uses Cookies

Stickiness is based on:

COOKIES

Think:

COOKIE

↓

REMEMBERS TARGET

ALB stickiness is configured at:

TARGET GROUP

level.

---

## Stickiness Tradeoff

Benefit:

SESSION CONSISTENCY

Possible problem:

LOAD IMBALANCE

Think:

STICKY USERS

↓

UNEQUAL TRAFFIC

### Exam Thinking

Stateless applications are generally easier to:

SCALE HORIZONTALLY

---

## Cross-Zone Load Balancing

Cross-Zone Load Balancing distributes traffic across:

ALL TARGETS

in enabled AZs.

Think:

AZ-A

2 TARGETS

AZ-B

8 TARGETS

With Cross-Zone:

100% TRAFFIC

↓

ALL 10 TARGETS

### Memory Trick

CROSS-ZONE

=

BALANCE ACROSS TARGETS

---

## Cross-Zone Defaults

### ALB

ENABLED BY DEFAULT

No inter-AZ charge for Cross-Zone traffic.

---

### NLB

DISABLED BY DEFAULT

Can enable it.

Inter-AZ data charges can apply.

---

### GWLB

DISABLED BY DEFAULT

### Memory Trick

ALB

=

ON

NLB

=

OFF

GWLB

=

OFF

---

## Multi-AZ vs Cross-Zone

Do not confuse:

MULTI-AZ

and:

CROSS-ZONE

### Multi-AZ

WHERE RESOURCES EXIST

### Cross-Zone

HOW TRAFFIC IS DISTRIBUTED

Think:

MULTI-AZ

=

AVAILABILITY

CROSS-ZONE

=

TRAFFIC BALANCE

---

## SSL / TLS Certificates

SSL/TLS Certificates provide:

ENCRYPTION IN TRANSIT

Think:

CLIENT

↓

HTTPS

↓

LOAD BALANCER

### Memory Trick

TLS

=

ENCRYPT TRAFFIC

---

## AWS Certificate Manager

Load Balancer certificates can be managed using:

[AWS Certificate Manager](<AWS Certificate Manager>)

or:

ACM

Think:

ACM

↓

CERTIFICATE

↓

LOAD BALANCER

---

## HTTPS Listener

An HTTPS Listener requires:

DEFAULT CERTIFICATE

Think:

HTTPS : 443

↓

LISTENER

↓

CERTIFICATE

### Memory Trick

HTTPS LISTENER

=

CERTIFICATE REQUIRED

---

## SNI

SNI stands for:

SERVER NAME INDICATION

SNI allows:

MULTIPLE SSL/TLS CERTIFICATES

on:

ONE LOAD BALANCER

Think:

DOMAIN A

↓

CERT A

DOMAIN B

↓

CERT B

↓

ONE ALB / NLB

### Memory Trick

SNI

=

SELECT CORRECT CERTIFICATE

---

## SNI Support

ALB

=

YES

NLB

=

YES

CLB

=

NO

Think:

NEWER LOAD BALANCERS

↓

SNI

OLDER CLB

↓

NO SNI

---

## Connection Draining

For Classic Load Balancer:

CONNECTION DRAINING

For ALB / NLB:

DEREGISTRATION DELAY

Purpose:

ALLOW IN-FLIGHT REQUESTS TO FINISH

Think:

TARGET LEAVING

↓

STOP NEW REQUESTS

↓

FINISH CURRENT REQUESTS

↓

REMOVE TARGET

### Memory Trick

DRAINING

=

FINISH BEFORE LEAVING

---

## Deregistration Delay

Default:

300 SECONDS

Range:

1 TO 3600 SECONDS

Think:

SHORT REQUESTS

↓

LOWER VALUE

LONG REQUESTS

↓

HIGHER VALUE

### Memory Trick

DEFAULT

=

5 MINUTES

---

## Auto Scaling Groups

ASG automatically:

ADDS

and:

REMOVES

EC2 instances.

Think:

TRAFFIC ↑

↓

SCALE OUT

TRAFFIC ↓

↓

SCALE IN

### Memory Trick

ASG

=

AUTOMATIC EC2 CAPACITY

---

## ASG Capacity Settings

ASG has:

MINIMUM

↓

DESIRED

↓

MAXIMUM

Think:

MIN

=

FLOOR

DESIRED

=

TARGET

MAX

=

CEILING

---

## Launch Template

ASG uses a:

LAUNCH TEMPLATE

to define new EC2 instances.

Think:

AMI

↓

INSTANCE TYPE

↓

USER DATA

↓

EBS

↓

SECURITY GROUP

↓

IAM ROLE

↓

LAUNCH TEMPLATE

↓

ASG

### Memory Trick

LAUNCH TEMPLATE

=

EC2 BLUEPRINT

---

## ASG Self-Healing

If an instance becomes:

UNHEALTHY

ASG can:

TERMINATE IT

↓

LAUNCH REPLACEMENT

Think:

FAILED EC2

↓

REPLACE

### Memory Trick

ASG

=

SELF-HEALING FLEET

---

## ASG + Load Balancer

ASG can automatically register new instances with:

LOAD BALANCER TARGET GROUP

Think:

ASG

↓

LAUNCH EC2

↓

REGISTER TARGET

↓

LOAD BALANCER

↓

SEND TRAFFIC

---

## ASG Scaling Policies

Main scaling strategies:

TARGET TRACKING

↓

STEP SCALING

↓

SCHEDULED SCALING

↓

PREDICTIVE SCALING

---

## Target Tracking

Target Tracking tries to maintain:

A TARGET METRIC

Example:

CPU

=

40%

Think:

TOO HIGH

↓

SCALE OUT

TOO LOW

↓

SCALE IN

### Memory Trick

TARGET TRACKING

=

THERMOSTAT

---

## Step Scaling

Step Scaling reacts to:

CLOUDWATCH ALARM

Example:

CPU > 70%

↓

ADD 2

CPU < 30%

↓

REMOVE 1

### Memory Trick

STEP

=

IF THIS → DO THAT

---

## Scheduled Scaling

Scheduled Scaling is for:

KNOWN TRAFFIC TIMES

Example:

FRIDAY

↓

5 PM

↓

INCREASE CAPACITY

### Memory Trick

SCHEDULED

=

I KNOW WHEN

---

## Predictive Scaling

Predictive Scaling:

FORECASTS FUTURE LOAD

Think:

HISTORICAL TRAFFIC

↓

PREDICTION

↓

SCALE AHEAD OF TIME

### Memory Trick

PREDICTIVE

=

AWS FORECASTS

---

## Scaling Metrics

Good metrics from the course include:

CPUUtilization

↓

RequestCountPerTarget

↓

Average Network In / Out

↓

Custom CloudWatch Metric

Think:

CPU-BOUND

↓

CPU

REQUEST-BOUND

↓

REQUEST COUNT

NETWORK-BOUND

↓

NETWORK

CUSTOM WORKLOAD

↓

CUSTOM METRIC

---

## CPUUtilization

CPUUtilization measures:

AVERAGE CPU

across the Auto Scaling Group.

Think:

CPU ↑

↓

MORE COMPUTE LOAD

↓

SCALE OUT

### Memory Trick

CPU-BOUND

=

CPUUtilization

---

## RequestCountPerTarget

RequestCountPerTarget measures:

REQUESTS PER BACKEND TARGET

Think:

TOO MANY REQUESTS PER EC2

↓

ADD EC2

### Memory Trick

REQUEST-BOUND

=

RequestCountPerTarget

---

## Network In / Out

Use:

AVERAGE NETWORK IN / OUT

when the application is:

NETWORK-BOUND

Think:

NETWORK BOTTLENECK

↓

NETWORK METRIC

---

## Custom Metric

If standard metrics do not represent demand:

PUSH CUSTOM METRIC

to:

CLOUDWATCH

Think:

APPLICATION-SPECIFIC LOAD

↓

CUSTOM METRIC

↓

ASG

### Memory Trick

SCALE ON THE ACTUAL BOTTLENECK

---

## Scaling Cooldown

After a scaling action:

ASG

↓

COOLDOWN

↓

WAIT FOR METRICS TO STABILIZE

Default:

300 SECONDS

### Memory Trick

COOLDOWN

=

DON'T OVERREACT

---

## Cooldown vs Deregistration Delay

### Cooldown

WAIT AFTER SCALING

↓

METRICS STABILIZE

### Deregistration Delay

WAIT WHILE TARGET LEAVES

↓

REQUESTS FINISH

Think:

COOLDOWN

=

SCALING STABILITY

DRAINING

=

REQUEST COMPLETION

---

## Highest-Value Scenario Recognition

Need application to survive an AZ failure?

→ Multi-AZ High Availability

---

Need one server to become more powerful?

→ Vertical Scaling

---

Need more application servers?

→ Horizontal Scaling

---

Need traffic distributed across EC2 instances?

→ Elastic Load Balancing

---

Need HTTP path or hostname routing?

→ ALB

---

Need Layer 7 routing?

→ ALB

---

Need TCP / UDP with extreme performance?

→ NLB

---

Need static Load Balancer IP?

→ NLB

---

Need third-party virtual firewalls?

→ GWLB

---

Need GENEVE port 6081?

→ GWLB

---

Need same client sent to same server?

→ Stickiness

---

Need even traffic across targets in multiple AZs?

→ Cross-Zone Load Balancing

---

Need multiple TLS certificates on one Load Balancer?

→ SNI

---

Need SSL/TLS certificate management?

→ ACM

---

Need existing requests to finish before EC2 removal?

→ Deregistration Delay

---

Need EC2 capacity automatically adjusted?

→ ASG

---

Need average CPU maintained around 40%?

→ Target Tracking

---

Need CPU > 70% to add 2 instances?

→ Step Scaling

---

Need more capacity every Friday at 5 PM?

→ Scheduled Scaling

---

Need AWS to forecast recurring demand?

→ Predictive Scaling

---

Need scaling for a network-bound workload?

→ Network In / Out metric

---

Need workload-specific scaling signal?

→ Custom CloudWatch Metric

---

## Highest-Value Exam Traps

SCALABILITY

≠

HIGH AVAILABILITY

---

VERTICAL

=

BIGGER

HORIZONTAL

=

MORE

---

ELB

≠

ASG

ELB

=

DISTRIBUTE

ASG

=

SCALE

---

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

ALB

=

NO STATIC IP

NLB

=

STATIC IP

---

PATH / HOST ROUTING

=

ALB

NOT NLB

---

GENEVE 6081

=

GWLB

---

STICKINESS

=

COOKIE + SAME TARGET

---

STICKINESS

CAN CAUSE

LOAD IMBALANCE

---

CROSS-ZONE

≠

MULTI-AZ

---

ALB CROSS-ZONE

=

ON BY DEFAULT

NLB CROSS-ZONE

=

OFF BY DEFAULT

---

SNI

=

MULTIPLE CERTIFICATES

---

ALB / NLB

=

SNI YES

CLB

=

SNI NO

---

DEREGISTRATION DELAY

=

FINISH ACTIVE REQUESTS

---

SCALING COOLDOWN

=

WAIT FOR METRICS TO STABILIZE

---

TARGET TRACKING

=

MAINTAIN TARGET

STEP SCALING

=

THRESHOLD → ACTION

SCHEDULED

=

KNOWN TIME

PREDICTIVE

=

FORECAST

---

## 10-Second Decision Tree

Need:

BIGGER SERVER?

↓

VERTICAL SCALING

MORE SERVERS?

↓

HORIZONTAL SCALING

SURVIVE AZ FAILURE?

↓

MULTI-AZ

DISTRIBUTE TRAFFIC?

↓

ELB

SMART HTTP ROUTING?

↓

ALB

TCP / UDP + STATIC IP?

↓

NLB

FIREWALL / IDS / IPS FLEET?

↓

GWLB

SAME USER → SAME SERVER?

↓

STICKINESS

MULTIPLE CERTIFICATES?

↓

SNI

GRACEFUL TARGET REMOVAL?

↓

DEREGISTRATION DELAY

AUTOMATIC EC2 CAPACITY?

↓

ASG

KEEP CPU AROUND TARGET?

↓

TARGET TRACKING

KNOWN SCALING TIME?

↓

SCHEDULED

FORECAST DEMAND?

↓

PREDICTIVE

---

## Quick Cheat Sheet

SCALABILITY

=

HANDLE LOAD

HIGH AVAILABILITY

=

SURVIVE FAILURE

VERTICAL

=

BIGGER

HORIZONTAL

=

MORE

ELASTICITY

=

AUTO GROW + SHRINK

ELB

=

DISTRIBUTE

ASG

=

SCALE

ALB

=

LAYER 7

NLB

=

LAYER 4

GWLB

=

LAYER 3

ALB

=

HTTP / HTTPS

NLB

=

TCP / UDP / TLS

GWLB

=

NETWORK APPLIANCES

NLB

=

STATIC IP

GWLB

=

GENEVE 6081

STICKINESS

=

SAME CLIENT → SAME TARGET

CROSS-ZONE

=

BALANCE ACROSS AZ TARGETS

TLS

=

ENCRYPT IN TRANSIT

ACM

=

CERTIFICATE MANAGEMENT

SNI

=

MULTIPLE CERTIFICATES

DEREGISTRATION DELAY

=

FINISH REQUESTS

ASG MIN

=

FLOOR

ASG DESIRED

=

TARGET

ASG MAX

=

CEILING

TARGET TRACKING

=

THERMOSTAT

STEP SCALING

=

IF THIS → DO THAT

SCHEDULED

=

KNOWN TIME

PREDICTIVE

=

FORECAST

COOLDOWN

=

WAIT AFTER SCALING

---

## Master Memory Trick

USERS

↓

LOAD BALANCER

↓

HEALTHY TARGETS

↓

AUTO SCALING GROUP

↓

EC2 ACROSS MULTIPLE AZs

Think:

ALB

=

SMART

NLB

=

FAST

GWLB

=

INSPECT

ELB

=

DISTRIBUTE

ASG

=

SCALE

CLOUDWATCH

=

WATCH

MULTI-AZ

=

SURVIVE FAILURE

And:

TARGET TRACKING

=

THERMOSTAT

STEP

=

REACT

SCHEDULED

=

PLAN

PREDICTIVE

=

FORECAST

### Final Architecture Memory

TRAFFIC ↑

↓

CLOUDWATCH SEES LOAD

↓

ASG ADDS EC2

↓

LOAD BALANCER DISTRIBUTES TRAFFIC

↓

MULTIPLE AZs PROVIDE HIGH AVAILABILITY

↓

HEALTH CHECKS REMOVE BAD TARGETS

↓

APPLICATION STAYS AVAILABLE

---

## Related Notes

- [Scalability & High Availability](<Scalability & High Availability>)
- [Elastic Load Balancing](<Elastic Load Balancing>)
- [Application Load Balancer](<Application Load Balancer>)
- [Network Load Balancer](<Network Load Balancer>)
- [Gateway Load Balancer](<Gateway Load Balancer>)
- [Load Balancer Stickiness](<Load Balancer Stickiness>)
- [Cross-Zone Load Balancing](<Cross-Zone Load Balancing>)
- [Load Balancer SSL Certificates](<Load Balancer SSL Certificates>)
- [Connection Draining - Deregistration Delay](<Connection Draining - Deregistration Delay>)
- [Auto Scaling Groups](<Auto Scaling Groups>)
- [Auto Scaling Group Scaling Policies](<Auto Scaling Group Scaling Policies>)
- [Auto Scaling Group Scaling Metrics](<Auto Scaling Group Scaling Metrics>)
- [CloudWatch](07-Monitoring/CloudWatch.md)
- [EC2](EC2)