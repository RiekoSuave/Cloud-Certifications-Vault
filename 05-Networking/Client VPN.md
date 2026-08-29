See also: [VPC](05-Networking/VPC.md)

See also: [Site-to-Site VPN](<05-Networking/Site-to-Site VPN.md>)

See also: [Direct Connect](<05-Networking/Direct Connect.md>)

## What Problem Does It Solve?

Allows an individual computer to connect to a private network in AWS and on-premises.

Client VPN lets a user remotely access private AWS resources as if the computer were connected to the private network.

### Memory Trick

Client VPN = Computer → Private Network

---

## Type

Remote Network Connectivity

---

## What Is Client VPN?

Client VPN allows you to connect from your computer using:

OpenVPN

to a private network in:

- AWS
- On-Premises

Basic Idea:

Computer

↓

Client VPN / OpenVPN

↓

Public Internet

↓

Private AWS Network

---

## Private Resource Access

Client VPN can allow you to connect to EC2 instances using their:

Private IP Addresses

This allows your computer to access resources as if it were connected to the private VPC network.

### Memory Trick

Client VPN = Remote Access to Private Resources

---

## Public Internet

Client VPN travels over the:

Public Internet

### Memory Trick

Client VPN = Remote User Over Internet

---

## Client VPN vs Site-to-Site VPN

### Client VPN

Connects:

Computer → Private Network

### Site-to-Site VPN

Connects:

On-Premises Network → AWS

### Memory Trick

Client VPN = One Computer

Site-to-Site VPN = Whole Network

See:

[Site-to-Site VPN](<05-Networking/Site-to-Site VPN.md>)

---

## Client VPN vs Direct Connect

### Client VPN

Remote computer connectivity over the public internet.

### Direct Connect

Dedicated private physical connection between on-premises and AWS.

### Memory Trick

Client VPN = Remote Computer

Direct Connect = Private Line

See:

[Direct Connect](<05-Networking/Direct Connect.md>)

---

## Scenario Questions

An individual user needs to connect a computer to private AWS resources.

→ Client VPN

---

A user wants to connect to an EC2 instance using its private IP address from a remote computer.

→ Client VPN

---

An entire on-premises network needs an encrypted VPN connection to AWS.

→ Site-to-Site VPN

NOT Client VPN

---

A company needs a dedicated private physical connection to AWS.

→ Direct Connect

NOT Client VPN

---

## Don't Confuse These

Client VPN = Computer → Private Network

Site-to-Site VPN = On-Premises Network → AWS

Direct Connect = Dedicated Private Connection

---

## Exam Keywords

Client VPN

OpenVPN

Private Network

Private IP

EC2

Remote Access

Public Internet

---

## Quick Cheat Sheet

Client VPN = Computer → Private Network

Client VPN = OpenVPN

Client VPN = Access EC2 Using Private IP

Client VPN = Public Internet

Site-to-Site VPN = Network → AWS

Direct Connect = Private Line