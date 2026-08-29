## What Problem Does It Solve?

Applications do not always receive the same amount of traffic.

Sometimes:

FEW USERS

Sometimes:

THOUSANDS OF USERS

Your architecture must be able to:

HANDLE INCREASED LOAD

and remain:

AVAILABLE

when infrastructure fails.

Think:

MORE TRAFFIC

↓

MORE CAPACITY

and:

SERVER / AZ FAILURE

↓

APPLICATION STILL WORKS

### Memory Trick

SCALABILITY

=

HANDLE MORE LOAD

HIGH AVAILABILITY

=

SURVIVE FAILURES

---

## What Is Scalability?

Scalability means:

AN APPLICATION CAN HANDLE GREATER LOAD

by adapting its resources.

Think:

APPLICATION LOAD ↑

↓

RESOURCES ↑

↓

APPLICATION CONTINUES WORKING

There are two major types:

VERTICAL SCALING

and

HORIZONTAL SCALING

### Memory Trick

SCALABILITY

=

GROW UP

or

GROW OUT

---

## Vertical Scaling

Vertical Scaling means:

INCREASE THE SIZE OF THE INSTANCE

Think:

SMALL EC2

↓

BIGGER EC2

↓

MORE CPU + RAM

Example:

t2.micro

↓

t2.large

Think:

ONE SERVER

↓

MAKE IT STRONGER

### Memory Trick

VERTICAL

=

SCALE UP

---

## Vertical Scaling Example

Imagine a database server needs more:

CPU

and

RAM

You could change:

SMALL INSTANCE

↓

LARGER INSTANCE

Think:

8 GB RAM

↓

32 GB RAM

↓

128 GB RAM

The number of servers stays:

THE SAME

The server becomes:

MORE POWERFUL

---

## Vertical Scaling Use Cases

Vertical scaling is common for:

NON-DISTRIBUTED SYSTEMS

such as:

DATABASES

Examples include:

[RDS](https://chatgpt.com/c/RDS)

and:

[ElastiCache](https://chatgpt.com/c/ElastiCache)

These systems can often benefit from moving to a larger instance size.

Think:

DATABASE NEEDS MORE POWER

↓

SCALE UP

---

## Vertical Scaling Limitation

Vertical scaling has:

A HARDWARE LIMIT

You cannot make one server infinitely powerful.

Think:

SMALL

↓

MEDIUM

↓

LARGE

↓

VERY LARGE

↓

MAXIMUM INSTANCE SIZE

This is one reason large distributed architectures often use:

HORIZONTAL SCALING

---

## Horizontal Scaling

Horizontal Scaling means:

INCREASE THE NUMBER OF INSTANCES

Think:

ONE EC2

↓

TWO EC2

↓

FOUR EC2

↓

TEN EC2

Instead of making one machine stronger:

ADD MORE MACHINES

### Memory Trick

HORIZONTAL

=

SCALE OUT

---

## Horizontal Scaling Example

Imagine a website receiving increasing traffic.

Instead of:

ONE HUGE EC2 INSTANCE

you can use:

EC2

EC2

EC2

EC2

Traffic can then be distributed across them using:

[Elastic Load Balancing](https://chatgpt.com/c/Elastic%20Load%20Balancing)

Think:

USERS

↓

LOAD BALANCER

↓

EC2 EC2 EC2

### Memory Trick

SCALE OUT

=

ADD SERVERS

---

## Horizontal Scaling and Distributed Systems

Horizontal scaling is especially useful for:

DISTRIBUTED APPLICATIONS

Examples include:

WEB APPLICATIONS

and:

MODERN CLOUD APPLICATIONS

Think:

MORE USERS

↓

ADD MORE EC2 INSTANCES

↓

DISTRIBUTE TRAFFIC

This is one of the core ideas behind:

[Auto Scaling Groups](https://chatgpt.com/c/Auto%20Scaling%20Groups)

---

## Scale Up vs Scale Out

### Scale Up

ONE SERVER

↓

BIGGER SERVER

Think:

VERTICAL

### Scale Out

ONE SERVER

↓

MANY SERVERS

Think:

HORIZONTAL

### Memory Trick

UP

=

BIGGER

OUT

=

MORE

---

## What Is High Availability?

High Availability means:

RUNNING YOUR APPLICATION ACROSS MULTIPLE LOCATIONS

so that failure of one location does not take down the application.

For AWS, this commonly means:

MULTIPLE AVAILABILITY ZONES

Think:

AZ-A

↓

APPLICATION

AZ-B

↓

APPLICATION

If:

AZ-A FAILS

↓

AZ-B STILL RUNS

### Memory Trick

HIGH AVAILABILITY

=

SURVIVE AZ FAILURE

---

## High Availability Architecture

A common highly available architecture is:

USERS

↓

LOAD BALANCER

↓

AZ-A

EC2

AZ-B

EC2

Think:

ONE AZ FAILS

↓

OTHER AZ CONTINUES

This removes dependence on:

ONE AVAILABILITY ZONE

---

## High Availability vs Scalability

These concepts are related but:

NOT THE SAME

### Scalability

Question:

CAN THE APPLICATION HANDLE MORE LOAD?

Think:

TRAFFIC ↑

↓

CAPACITY ↑

### High Availability

Question:

CAN THE APPLICATION SURVIVE FAILURE?

Think:

AZ FAILS

↓

APPLICATION STILL AVAILABLE

### Memory Trick

SCALABILITY

=

LOAD

HIGH AVAILABILITY

=

FAILURE

---

## Horizontal Scaling vs High Availability

Horizontal scaling might mean:

MORE INSTANCES

but those instances could still exist inside:

ONE AZ

Example:

AZ-A

↓

EC2 EC2 EC2

This provides:

SCALABILITY

but does not fully protect against:

AZ FAILURE

For High Availability:

AZ-A

↓

EC2 EC2

AZ-B

↓

EC2 EC2

### Exam Trap

MORE EC2 INSTANCES

does not automatically mean:

HIGH AVAILABILITY

You must think about:

MULTIPLE AZs

---

## High Availability and Load Balancers

Load balancers are commonly used to distribute traffic across:

MULTIPLE EC2 INSTANCES

and:

MULTIPLE AVAILABILITY ZONES

Think:

USERS

↓

[Elastic Load Balancing](https://chatgpt.com/c/Elastic%20Load%20Balancing)

↓

AZ-A EC2

AZ-B EC2

This provides both:

SCALABILITY

and

HIGH AVAILABILITY

---

## High Availability and Auto Scaling

[Auto Scaling Groups](https://chatgpt.com/c/Auto%20Scaling%20Groups)

can automatically:

ADD INSTANCES

and:

REMOVE INSTANCES

based on demand.

Think:

TRAFFIC ↑

↓

ADD EC2

TRAFFIC ↓

↓

REMOVE EC2

An Auto Scaling Group can also distribute EC2 instances across:

MULTIPLE AZs

Think:

SCALING

MULTI-AZ

↓

RESILIENT ARCHITECTURE

---

## What Is Elasticity?

Elasticity means:

AUTOMATICALLY MATCHING RESOURCES TO DEMAND

Think:

TRAFFIC ↑

↓

RESOURCES ↑

and:

TRAFFIC ↓

↓

RESOURCES ↓

The important concept is:

AUTOMATIC

### Memory Trick

ELASTICITY

=

AUTO SCALE WITH DEMAND

---

## Scalability vs Elasticity

### Scalability

Can the system:

HANDLE MORE LOAD?

### Elasticity

Can the system:

AUTOMATICALLY ADD AND REMOVE RESOURCES

as load changes?

Think:

SCALABILITY

=

ABILITY TO GROW

ELASTICITY

=

GROW + SHRINK AUTOMATICALLY

---

## Elasticity Example

Imagine an online store.

Normal traffic:

2 EC2 INSTANCES

Black Friday:

20 EC2 INSTANCES

After Black Friday:

2 EC2 INSTANCES

Think:

2

↓

20

↓

2

automatically.

This is:

ELASTICITY

---

## What Is Agility?

Cloud Agility means:

RESOURCES CAN BE CREATED QUICKLY

Instead of waiting weeks or months to purchase physical infrastructure:

REQUEST AWS RESOURCE

↓

RESOURCE AVAILABLE QUICKLY

Think:

IDEA

↓

DEPLOY

↓

TEST

↓

CHANGE

### Memory Trick

AGILITY

=

MOVE FAST

---

## Scalability vs Availability vs Elasticity vs Agility

SCALABILITY

=

HANDLE MORE LOAD

HIGH AVAILABILITY

=

SURVIVE FAILURE

ELASTICITY

=

AUTOMATICALLY MATCH DEMAND

AGILITY

=

DEPLOY QUICKLY

Think:

MORE USERS?

↓

SCALABILITY

SERVER / AZ FAILS?

↓

HIGH AVAILABILITY

TRAFFIC CHANGES?

↓

ELASTICITY

NEED RESOURCES FAST?

↓

AGILITY

---

## Architecture Thinking

A typical scalable and highly available application looks like:

USERS

↓

LOAD BALANCER

↓

AZ-A

EC2 EC2

AZ-B

EC2 EC2

↓

AUTO SCALING GROUP

Think:

LOAD BALANCER

=

DISTRIBUTE

AUTO SCALING

=

ADD / REMOVE

MULTIPLE AZs

=

HIGH AVAILABILITY

---

## Scenario Recognition

Need one server to become more powerful?

→ Vertical Scaling

---

Need to add more servers?

→ Horizontal Scaling

---

Need more CPU and RAM for a database?

→ Vertical Scaling

---

Need a web application to handle millions of users?

→ Horizontal Scaling

---

Need an application to survive an Availability Zone failure?

→ High Availability / Multi-AZ

---

Need resources automatically added when traffic increases?

→ Elasticity / Auto Scaling

---

Need resources automatically removed when traffic decreases?

→ Elasticity / Auto Scaling

---

Need traffic distributed across many EC2 instances?

→ Elastic Load Balancing

---

Need EC2 instances automatically added and removed?

→ Auto Scaling Group

---

Need AWS resources provisioned rapidly instead of purchasing hardware?

→ Agility

---

## Exam Traps

VERTICAL SCALING

=

BIGGER INSTANCE

HORIZONTAL SCALING

=

MORE INSTANCES

SCALE UP

=

VERTICAL

SCALE OUT

=

HORIZONTAL

SCALABILITY

≠

HIGH AVAILABILITY

SCALABILITY

=

HANDLE LOAD

HIGH AVAILABILITY

=

SURVIVE FAILURE

MORE INSTANCES

≠

AUTOMATICALLY MULTI-AZ

HIGH AVAILABILITY

=

THINK MULTIPLE AZs

ELASTICITY

=

AUTOMATIC SCALE UP / DOWN

AGILITY

=

RAPID RESOURCE CREATION

LOAD BALANCER

=

DISTRIBUTE TRAFFIC

AUTO SCALING GROUP

=

ADJUST NUMBER OF INSTANCES

---

## Quick Cheat Sheet

SCALABILITY

=

HANDLE MORE LOAD

VERTICAL SCALING

=

BIGGER SERVER

HORIZONTAL SCALING

=

MORE SERVERS

SCALE UP

=

VERTICAL

SCALE OUT

=

HORIZONTAL

HIGH AVAILABILITY

=

MULTIPLE AZs + SURVIVE FAILURE

ELASTICITY

=

AUTOMATICALLY MATCH RESOURCES TO DEMAND

AGILITY

=

CREATE RESOURCES QUICKLY

ELB

=

DISTRIBUTE TRAFFIC

ASG

=

ADD / REMOVE EC2

DATABASE

=

OFTEN SCALE VERTICALLY

WEB APPLICATION

=

OFTEN SCALE HORIZONTALLY

---

## Master Memory Trick

VERTICAL

=

BIGGER

HORIZONTAL

=

MORE

SCALABILITY

=

HANDLE LOAD

HIGH AVAILABILITY

=

SURVIVE FAILURE

ELASTICITY

=

AUTO GROW + SHRINK

AGILITY

=

MOVE FAST

Think:

TRAFFIC ↑

↓

ASG ADDS EC2

↓

ELB DISTRIBUTES TRAFFIC

↓

MULTIPLE AZs SURVIVE FAILURE

---

## Related Notes

- [EC2](https://chatgpt.com/c/EC2)
    
- [Elastic Load Balancing](https://chatgpt.com/c/Elastic%20Load%20Balancing)
    
- [Auto Scaling Groups](https://chatgpt.com/c/Auto%20Scaling%20Groups)
    
- [Application Load Balancer](https://chatgpt.com/c/Application%20Load%20Balancer)
    
- [Network Load Balancer](https://chatgpt.com/c/Network%20Load%20Balancer)
    
- [Gateway Load Balancer](https://chatgpt.com/c/Gateway%20Load%20Balancer)
    
- [Load Balancer Stickiness](https://chatgpt.com/c/Load%20Balancer%20Stickiness)
    
- [Cross-Zone Load Balancing](https://chatgpt.com/c/Cross-Zone%20Load%20Balancing)
    
- [SAA High Availability Cheat Sheet](https://chatgpt.com/c/SAA%20High%20Availability%20Cheat%20Sheet)