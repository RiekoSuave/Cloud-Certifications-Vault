## What Problem Does It Solve?

A normal EC2 public IP can:

CHANGE

when an instance is:

STOPPED

↓

STARTED

If you need a:

FIXED PUBLIC IPv4 ADDRESS

you can use:

ELASTIC IP

### Memory Trick

Elastic IP = FIXED PUBLIC IP

---

## What Is an Elastic IP?

An Elastic IP is a:

PUBLIC IPv4 ADDRESS

that you own as long as you:

DON'T DELETE IT

Think:

EC2 NORMAL PUBLIC IP

↓

CAN CHANGE

ELASTIC IP

↓

STAYS FIXED

---

## Why Would You Need One?

Suppose an application depends on a specific:

PUBLIC IP ADDRESS

A normal EC2 public IP may change after:

STOP

+

START

An Elastic IP solves this by providing:

FIXED PUBLIC IPv4

---

## Elastic IP Attachment

Your course states that an Elastic IP can be attached to:

ONE INSTANCE AT A TIME

Think:

ELASTIC IP

↓

EC2 INSTANCE

---

# Elastic IP and Failure

An Elastic IP can help:

MASK THE FAILURE

of an EC2 instance or software.

How?

You can rapidly:

REMAP

the Elastic IP to:

ANOTHER INSTANCE

Think:

ELASTIC IP

↓

EC2 INSTANCE A

❌ FAILURE

↓

REMAP ELASTIC IP

↓

EC2 INSTANCE B

### Memory Trick

Elastic IP = MOVE THE ADDRESS

---

# Elastic IP Limit

Your course states that you can have:

5 ELASTIC IPs

in your account.

You can ask AWS to:

INCREASE

this limit.

For your course notes, remember:

DEFAULT COURSE LIMIT = 5

---

# Why Your Course Says to Avoid Elastic IPs

This is an important architecture point.

Your course says:

TRY TO AVOID USING ELASTIC IPs

because they can often reflect:

POOR ARCHITECTURAL DECISIONS

Instead, the course recommends alternatives.

---

## Alternative #1

Use a:

RANDOM PUBLIC IP

and register a:

DNS NAME

to it.

Think:

PUBLIC IP

↓

DNS NAME

↓

USERS CONNECT THROUGH NAME

---

## Alternative #2

Use a:

LOAD BALANCER

and:

DON'T USE A PUBLIC IP

on the instance.

We'll cover Load Balancers later.

### Memory Trick

Good Architecture?

DNS / LOAD BALANCER

instead of depending heavily on:

ELASTIC IP

---

# Normal Public IP vs Elastic IP

| Feature | Normal Public IP | Elastic IP |
| --- | --- | --- |
| Public IPv4 | Yes | Yes |
| Can change after stop/start | Yes | Fixed |
| Retained by you | No guarantee | Until deleted |
| Can remap to another instance | Not the key feature | Yes |
| Think | TEMPORARY PUBLIC IP | FIXED PUBLIC IP |

---

# Elastic IP vs Private IP

Don't confuse these.

### Private IP

Think:

INTERNAL NETWORK

### Elastic IP

Think:

FIXED PUBLIC IPv4

### Memory Trick

PRIVATE IP

= INTERNAL

ELASTIC IP

= FIXED PUBLIC

---

# Scenario Recognition

Need a fixed public IPv4 address for EC2?

→ ELASTIC IP

---

EC2 public IP changes after stop/start?

→ NORMAL BEHAVIOR FROM COURSE

Need it fixed?

→ ELASTIC IP

---

EC2 instance fails and you want to rapidly move its public address to another instance?

→ REMAP ELASTIC IP

---

Need a better scalable architecture instead of depending on fixed public IPs?

→ DNS

or

LOAD BALANCER

---

# Exam Traps

ELASTIC IP

= PUBLIC IPv4

ELASTIC IP

= FIXED

NORMAL PUBLIC IP

= CAN CHANGE AFTER STOP + START

ELASTIC IP

≠ PRIVATE IP

ELASTIC IP

= ONE INSTANCE AT A TIME

ELASTIC IP

= CAN BE REMAPPED

Course recommendation:

TRY TO AVOID ELASTIC IPs

when better architecture can use:

DNS

or

LOAD BALANCER

---

# Quick Cheat Sheet

ELASTIC IP

= FIXED PUBLIC IPv4

NORMAL PUBLIC IP

= CAN CHANGE

ATTACHMENT

= ONE INSTANCE AT A TIME

FAILURE?

= REMAP TO ANOTHER INSTANCE

COURSE LIMIT

= 5

BETTER ARCHITECTURE

= DNS / LOAD BALANCER

---

# Master Memory Trick

Need:

PUBLIC IP

that:

DOESN'T CHANGE?

↓

ELASTIC IP

Instance fails?

↓

REMAP IT

But architecturally:

DNS / LOAD BALANCER

↓

OFTEN BETTER

---

## Related Notes

- [[EC2]]
- [[Private vs Public IP]]
- [[EC2 Security Groups]]
- [[SSH and EC2 Instance Connect]]
- [[Elastic Network Interfaces]]
- [[Elastic Load Balancing]]
- [[EC2 Comparison]]
- [[SAA EC2 Cheat Sheet]]