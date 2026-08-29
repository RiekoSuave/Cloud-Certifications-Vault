See also: [VPC](05-Networking/VPC.md)

See also: [VPC Endpoints](<05-Networking/VPC Endpoints.md>)

## What Problem Does It Solve?

Provides private connectivity to a service in a third-party VPC.

AWS PrivateLink allows private access to services without using the public internet.

### Memory Trick

PrivateLink = Private Connection to a Service

---

## Type

Private Networking

---

## What Is AWS PrivateLink?

AWS PrivateLink allows you to privately connect to a service located in another VPC.

Your course specifically describes it as:

Private connectivity to a service in a third-party VPC.

Basic Idea:

Your VPC

↓

PrivateLink

↓

Service in Third-Party VPC

### Memory Trick

PrivateLink = Private Service Access

---

## Private Connectivity

The key concept to remember is:

PrivateLink provides private connectivity.

Instead of accessing the service through the public internet, communication can remain private.

---

## PrivateLink vs VPC Peering

At the level covered in your current course:

### PrivateLink

Think:

Private access to a service

### VPC Peering

Think:

Private connection between two VPCs

### Memory Trick

PrivateLink = Service

VPC Peering = VPC

---

## PrivateLink vs VPC Endpoint

Your course discusses VPC Endpoints separately.

### VPC Endpoint

Provides private access to AWS services from within a VPC.

### PrivateLink

Provides private connectivity to a service in a third-party VPC.

### Memory Trick

Endpoint = AWS Service Access

PrivateLink = Private Service Connection

See:

[VPC Endpoints](<05-Networking/VPC Endpoints.md>)

---

## Scenario Questions

A company needs to privately connect to a service located in a third-party VPC.

→ AWS PrivateLink

---

Two VPCs need direct private connectivity.

→ VPC Peering

---

Resources inside a VPC need private access to an AWS service.

→ VPC Endpoint

---

## Don't Confuse These

PrivateLink = Private Connection to a Service

VPC Peering = VPC ↔ VPC

VPC Endpoint = Private Access to AWS Services

Transit Gateway = Central Network Hub

---

## Exam Keywords

AWS PrivateLink

Private Connectivity

Third-Party VPC

Private Service Access

VPC

---

## Quick Cheat Sheet

PrivateLink = Private Service Access

PrivateLink = Third-Party VPC Service

VPC Peering = VPC → VPC

VPC Endpoint = VPC → AWS Service

Transit Gateway = Many Networks → Hub