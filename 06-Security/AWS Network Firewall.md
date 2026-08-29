See also: [VPC](05-Networking/VPC.md)

See also: [Security Groups vs NACLs](<Security Groups vs NACLs>)

See also: [WAF](06-Security/WAF.md)

## What Problem Does It Solve?

Protects your VPC against network attacks.

AWS Network Firewall provides network-level protection for resources inside a VPC.

### Memory Trick

Network Firewall = Protect the VPC

---

## Type

Network Security Service

---

## What Is AWS Network Firewall?

AWS Network Firewall helps protect:

Amazon VPC

against:

Network Attacks

Think:

Network Traffic

↓

AWS Network Firewall

↓

VPC Protection

### Memory Trick

Network Firewall = VPC Firewall

---

## Network Firewall vs Security Groups

Your networking material identifies Security Groups as operating at the:

EC2 Instance / ENI Level

AWS Network Firewall has the broader association:

Protect the VPC against network attacks.

### Memory Trick

Security Group = Instance / ENI

Network Firewall = VPC

---

## Network Firewall vs NACL

Your networking material identifies NACLs as:

Subnet-Level Rules

They control inbound and outbound traffic at the subnet level.

For your current course:

NACL = Subnet

Network Firewall = VPC Protection

### Memory Trick

NACL = Subnet

Network Firewall = VPC

---

## Network Firewall vs WAF

These are different types of firewalls.

### AWS Network Firewall

Protects:

VPC against network attacks

### AWS WAF

Filters:

Incoming web requests based on rules

Think:

WAF = Web Traffic

Network Firewall = Network Traffic

### Memory Trick

WAF = Web

Network Firewall = Network

See:

[WAF](06-Security/WAF.md)

---

## Security Layers

A useful way to organize the concepts from your course:

| Service | Think |
|---|---|
| Security Group | EC2 Instance / ENI |
| NACL | Subnet |
| AWS Network Firewall | VPC / Network Attacks |
| WAF | Web Requests |

### Memory Trick

Security Group = Instance

NACL = Subnet

Network Firewall = VPC

WAF = Web

---

## Common Use Cases

- Protecting a VPC
- Network security
- Protecting against network attacks

---

## Scenario Questions

A company wants an AWS service designed to protect its VPC against network attacks.

→ AWS Network Firewall

---

A company wants firewall rules controlling traffic at the EC2 instance or ENI level.

→ Security Group

---

A company wants stateless inbound and outbound rules at the subnet level.

→ NACL

---

A company wants to filter malicious web requests.

→ AWS WAF

---

## Don't Confuse These

Security Group = Instance / ENI Firewall

NACL = Subnet-Level Rules

Network Firewall = Protect VPC Against Network Attacks

WAF = Filter Web Requests

---

## Exam Keywords

AWS Network Firewall

VPC

Network Security

Network Attacks

Firewall

---

## Quick Cheat Sheet

Network Firewall = Protect VPC

Security Group = Instance / ENI

NACL = Subnet

WAF = Web Requests

Network Firewall = Network Attacks