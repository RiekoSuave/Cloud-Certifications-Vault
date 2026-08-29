## What Problem Does It Solve?

IP addresses allow AWS resources to communicate across private networks and the internet.

Elastic IP solves the problem of needing a fixed public IPv4 address for an AWS resource such as an EC2 instance.

---

## IPv4

IPv4 = Internet Protocol version 4.

IPv4 provides approximately 4.3 billion possible addresses.

AWS uses both:

- Public IPv4 addresses
- Private IPv4 addresses

---

## Public IPv4

A Public IPv4 address can be used to communicate over the internet.

For an EC2 instance:

- A public IPv4 address can be assigned to the instance
- By default, the public IPv4 address can change when the EC2 instance is stopped and started

### Exam Idea

Normal Public IPv4 = Can Change

---

## Private IPv4

A Private IPv4 address is used for communication inside private networks such as a VPC.

Example:

192.168.1.1

For an EC2 instance:

- The private IPv4 address is used for internal AWS networking
- The private IPv4 address remains fixed when the instance is stopped and started

### Exam Idea

Private IPv4 = Internal Communication

---

## Elastic IP

Elastic IP (EIP) provides a fixed public IPv4 address.

Instead of receiving a different public IP after stopping and starting an EC2 instance, an Elastic IP can remain associated with the resource.

### Key Features

- Static public IPv4 address
- Can be associated with an EC2 instance
- Useful when a resource needs a consistent public IP address

### Important Cost Concept

AWS charges for public IPv4 addresses, including Elastic IP addresses.

---

## IPv6

IPv6 = Internet Protocol version 6.

IPv6 was created because the number of available IPv4 addresses is limited.

IPv6 provides an extremely large address space.

In AWS:

- IPv6 addresses are publicly routable
- There is no traditional private IPv6 address range like IPv4
- AWS does not charge for IPv6 addresses

---

## IPv4 vs IPv6

| IPv4 | IPv6 |
|---|---|
| About 4.3 billion addresses | Extremely large address space |
| Public and private addresses | Publicly routable addresses |
| Public IPv4 addresses have AWS charges | IPv6 addresses are free |

---

## Public IPv4 vs Private IPv4 vs Elastic IP

| Address | Purpose | Fixed? |
|---|---|---|
| Public IPv4 | Internet communication | Can change after stop/start |
| Private IPv4 | Internal VPC communication | Remains fixed |
| Elastic IP | Fixed public internet address | Yes |

---

## Exam Keywords

- IPv4
- IPv6
- Public IP
- Private IP
- Elastic IP
- Static public IP
- EC2 networking
- VPC

---

## Memory Tricks

**Public IPv4 = Internet Address**

**Private IPv4 = Internal Address**

**Elastic IP = Static Public Address**

**IPv6 = Huge Address Space**

---

## CCP Importance

MEDIUM

Know the differences between:

Public IPv4  
vs  
Private IPv4  
vs  
Elastic IP  
vs  
IPv6