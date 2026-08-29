See also: [VPC](05-Networking/VPC.md)

See also: [Subnets](Subnets)

See also: [Security Groups vs NACLs](<Security Groups vs NACLs>)

## What Problem Does It Solve?

Provides visibility into network traffic flowing through your VPC.

VPC Flow Logs help you monitor and troubleshoot network connectivity and investigate network traffic.

### Memory Trick

VPC Flow Logs = Network Traffic Records

---

## Type

VPC Monitoring and Logging Feature

---

## What Are VPC Flow Logs?

VPC Flow Logs capture information about network traffic.

They provide records that can help you understand traffic flowing through your AWS network.

Think:

Network Traffic

↓

VPC Flow Logs

↓

Traffic Records

### Memory Trick

Flow Logs = See What the Network Is Doing

---

## Why Use VPC Flow Logs?

VPC Flow Logs can help with:

- Network monitoring
- Troubleshooting
- Security analysis
- Understanding network traffic

---

## Network Troubleshooting

VPC Flow Logs can help investigate networking problems.

Example:

An EC2 instance cannot communicate as expected.

↓

Check network traffic information

↓

Use Flow Logs to help troubleshoot the connection

### Memory Trick

Connection Problem?

→ Check Flow Logs

---

## Security Analysis

Flow Logs provide visibility into network traffic that can assist with security investigations.

They can help you better understand what traffic is occurring within your network.

See:

[Security Groups vs NACLs](<Security Groups vs NACLs>)

---

## VPC Flow Logs vs Security Groups and NACLs

These solve different problems.

### Security Groups

Control allowed traffic at the resource level.

### NACLs

Control allowed and denied traffic at the subnet level.

### VPC Flow Logs

Provide information about network traffic.

| Feature | Purpose |
|---|---|
| Security Group | Control resource traffic |
| NACL | Control subnet traffic |
| VPC Flow Logs | Observe network traffic |

### Memory Trick

Security Group = Control Resource Traffic

NACL = Control Subnet Traffic

Flow Logs = Observe Traffic

---

## VPC Flow Logs vs CloudTrail

Don't confuse network traffic visibility with AWS API activity.

### VPC Flow Logs

Think:

Network Traffic

### CloudTrail

Think:

AWS API Activity

### Memory Trick

Flow Logs = Network

CloudTrail = API Actions

---

## Common Use Cases

- Monitoring network traffic
- Troubleshooting connectivity
- Investigating network behavior
- Security analysis

---

## Scenario Questions

A company wants visibility into network traffic inside its VPC.

→ VPC Flow Logs

---

An administrator is troubleshooting network connectivity between AWS resources.

→ VPC Flow Logs

---

A security team wants information about network traffic for an investigation.

→ VPC Flow Logs

---

A company needs to control which traffic can reach an EC2 instance.

→ Security Group

NOT VPC Flow Logs

---

A company needs subnet-level traffic filtering.

→ NACL

NOT VPC Flow Logs

---

A company needs to track AWS API activity.

→ CloudTrail

NOT VPC Flow Logs

---

## Don't Confuse These

VPC Flow Logs = Network Traffic Records

Security Groups = Resource-Level Traffic Control

NACLs = Subnet-Level Traffic Control

CloudTrail = AWS API Activity

CloudWatch = Monitoring

---

## Exam Keywords

VPC Flow Logs

Network Traffic

Network Monitoring

Troubleshooting

Security Analysis

Connectivity

---

## Quick Cheat Sheet

VPC Flow Logs = Network Traffic Records

Flow Logs = Observe Traffic

Security Group = Control Resource Traffic

NACL = Control Subnet Traffic

CloudTrail = API Activity

Connection Problem → Check Flow Logs