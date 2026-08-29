## What Problem Does It Solve?

IP addresses allow machines to:

IDENTIFY

and

COMMUNICATE WITH

each other across networks.

The major distinction is:

PUBLIC IP

vs

PRIVATE IP

### Memory Trick

PUBLIC = INTERNET

PRIVATE = INTERNAL NETWORK

---

# IPv4 vs IPv6

Networking uses two types of IP addresses:

IPv4

and

IPv6

Your course primarily uses:

IPv4

### IPv4 Example

1.160.10.240

### IPv6 Example

3ffe:1900:4545:3:200:f8ff:fe21:67cf

---

## IPv4

IPv4 is still described by your course as the:

MOST COMMON FORMAT

used online.

IPv4 format:

[0-255].[0-255].[0-255].[0-255]

Example:

192.168.0.1

---

## IPv6

IPv6 is:

NEWER

Your course associates IPv6 with helping solve addressing problems related to:

INTERNET OF THINGS

or:

IoT

For this section, focus primarily on:

IPv4

---

# Public IP

A Public IP means a machine can be:

IDENTIFIED ON THE INTERNET

Think:

INTERNET

↓

PUBLIC IP

↓

SERVER

### Memory Trick

Public IP = INTERNET ADDRESS

---

## Public IP Must Be Unique

A Public IP must be:

UNIQUE

across the:

WHOLE WEB

Two machines cannot have the same public IP on the public internet.

Think:

ONE PUBLIC IP

↓

ONE UNIQUE INTERNET IDENTITY

---

## Public IP Location

Your course notes that Public IPs can be:

GEO-LOCATED

easily.

---

# Private IP

A Private IP identifies a machine within a:

PRIVATE NETWORK

Think:

PRIVATE NETWORK

↓

PRIVATE IP

↓

SERVER

### Memory Trick

Private IP = INTERNAL ADDRESS

---

## Private IP Must Be Unique Within Its Network

Within one private network:

PRIVATE IP

must be:

UNIQUE

But different private networks can reuse:

THE SAME PRIVATE IP

---

## Example

Company A:

PRIVATE NETWORK

192.168.0.1

Company B:

PRIVATE NETWORK

192.168.0.1

This is possible because they are:

DIFFERENT PRIVATE NETWORKS

### Memory Trick

PUBLIC IP

= GLOBALLY UNIQUE

PRIVATE IP

= LOCALLY UNIQUE

---

# Private Networks Accessing the Internet

Your course explains that machines using private IP addresses can connect to the:

WWW

using:

NAT

+

INTERNET GATEWAY

Think:

PRIVATE MACHINE

↓

NAT + INTERNET GATEWAY

↓

INTERNET

We'll cover these networking components more deeply later.

---

# Public vs Private IP

| Feature | Public IP | Private IP |
| --- | --- | --- |
| Internet identity | Yes | No |
| Private network identity | Not main purpose | Yes |
| Must be unique globally | Yes | No |
| Must be unique within private network | N/A | Yes |
| Can different private networks reuse it? | No | Yes |
| Think | INTERNET | INTERNAL |

---

# EC2 IP Addresses

Your course's EC2 hands-on section states that an EC2 machine comes with:

PRIVATE IP

for:

INTERNAL AWS NETWORK

and:

PUBLIC IP

for:

WWW

Think:

EC2 INSTANCE

↓

PRIVATE IP

= INTERNAL

PUBLIC IP

= INTERNET

---

# Private IP on EC2

The private IP is used for communication within the:

INTERNAL AWS NETWORK

### Memory Trick

EC2 Private IP = AWS INTERNAL

---

# Public IP on EC2

The public IP allows the instance to communicate in the context of:

WWW / INTERNET

### Memory Trick

EC2 Public IP = INTERNET

---

# SSH and IP Addresses

Your course's hands-on example explains that when connecting to EC2 from outside its private network:

PRIVATE IP

↓

CANNOT BE USED DIRECTLY

because your computer is not on the same private network.

Instead, the course uses:

PUBLIC IP

for SSH.

Think:

YOUR COMPUTER

↓

INTERNET

↓

PUBLIC IP

↓

PORT 22

↓

EC2

See:

[[SSH and EC2 Instance Connect]]

---

# Public IP Can Change

This is very important.

When an EC2 instance is:

STOPPED

and then:

STARTED

its:

PUBLIC IP

can change.

Think:

EC2

Public IP = 1.2.3.4

↓

STOP

↓

START

↓

Public IP = DIFFERENT

### Memory Trick

STOP + START

= PUBLIC IP MAY CHANGE

---

# What If You Need a Fixed Public IP?

If you need:

FIXED PUBLIC IPv4

your course introduces:

[[Elastic IP]]

An Elastic IP provides a public IPv4 address you can retain.

Think:

NORMAL PUBLIC IP

= CAN CHANGE

ELASTIC IP

= FIXED

---

# Scenario Recognition

Need a machine identifiable on the internet?

→ PUBLIC IP

---

Need communication inside a private network?

→ PRIVATE IP

---

Can two companies use the same private IP internally?

→ YES

---

Can two internet-connected machines have the same public IP?

→ NO

---

Need to SSH from your computer over the internet to EC2 in the course example?

→ PUBLIC IP

---

Stopped and restarted EC2 and its public IP changed?

→ EXPECTED COURSE BEHAVIOR

---

Need a fixed public IPv4 address?

→ ELASTIC IP

---

# Exam Traps

PUBLIC IP

= GLOBALLY UNIQUE

PRIVATE IP

= UNIQUE ONLY WITHIN PRIVATE NETWORK

Different private networks:

CAN REUSE PRIVATE IPs

Public IP:

CAN CHANGE AFTER EC2 STOP + START

Private IP:

= INTERNAL NETWORK

Public IP:

= INTERNET

Need fixed public IPv4?

= ELASTIC IP

---

# Quick Cheat Sheet

PUBLIC IP

= INTERNET

PRIVATE IP

= INTERNAL

PUBLIC

= GLOBALLY UNIQUE

PRIVATE

= LOCALLY UNIQUE

PRIVATE IP REUSE

= YES, ACROSS DIFFERENT PRIVATE NETWORKS

EC2 PRIVATE IP

= INTERNAL AWS NETWORK

EC2 PUBLIC IP

= WWW

STOP + START

= PUBLIC IP CAN CHANGE

FIXED PUBLIC IP

= ELASTIC IP

---

# Master Memory Trick

PUBLIC

= OUTSIDE

PRIVATE

= INSIDE

PUBLIC IP

= ONE UNIQUE ADDRESS ON WEB

PRIVATE IP

= CAN REPEAT IN DIFFERENT PRIVATE NETWORKS

EC2 STOP + START

↓

PUBLIC IP MAY CHANGE

Need it fixed?

↓

ELASTIC IP

---

## Related Notes

- [[EC2]]
- [[EC2 Security Groups]]
- [[SSH and EC2 Instance Connect]]
- [[Elastic IP]]
- [[Elastic Network Interfaces]]
- [[EC2 Placement Groups]]
- [[EC2 Comparison]]
- [[SAA EC2 Cheat Sheet]]