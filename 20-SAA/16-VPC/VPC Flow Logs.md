## What Problem Does It Solve?

[[VPC Flow Logs]] capture:

**Network traffic metadata for traffic flowing through VPC network interfaces**

They help you:

- Troubleshoot connectivity
- Investigate rejected traffic
- Monitor network behavior
- Analyze traffic patterns
- Support security investigations

Architecture:

Network Traffic  
↓  
ENI  
↓  
VPC Flow Logs  
↓  
Traffic Metadata  
↓  
Logs / Analysis

> [!tip] Memory Trick
> **VPC Flow Logs = Who Talked to Whom**

---

## Core Concept

VPC Flow Logs record information about:

**IP traffic**

going to and from:

**Network interfaces**

They do NOT capture:

**Full packet contents**

### Killer Exam Clue

> **Need to determine whether traffic to an EC2 instance was accepted or rejected**
>
> → **VPC Flow Logs**

---

# What Do Flow Logs Capture?

Flow log records can contain information such as:

- Source IP
- Destination IP
- Source port
- Destination port
- Protocol
- Number of packets
- Number of bytes
- Start time
- End time
- Traffic action
- Log status

### Memory Trick

**WHO**

talked to:

**WHOM**

using:

**WHAT PORT**

and was it:

**ACCEPTED or REJECTED?**

---

# ACCEPT

An:

**ACCEPT**

record means the traffic was permitted by relevant:

**VPC networking controls**

Example:

Source:

`10.0.1.10`

Destination:

`10.0.2.20`

Port:

`443`

Action:

**ACCEPT**

---

# REJECT

A:

**REJECT**

record indicates traffic was rejected.

Possible causes include:

- Security Group rules
- NACL rules
- Other networking restrictions

### Killer Exam Clue

> **Users cannot connect to EC2 and you need evidence showing rejected traffic**
>
> → **VPC Flow Logs**

---

# Flow Log Scope

Flow Logs can be created at different scopes:

- VPC
- Subnet
- Network Interface

### Memory Trick

**VPC = Everything**

**Subnet = Neighborhood**

**ENI = Individual Network Interface**

---

# VPC-Level Flow Logs

A VPC-level Flow Log captures traffic information for:

**Network interfaces throughout the VPC**

This provides:

**Broad visibility**

---

# Subnet-Level Flow Logs

A subnet-level Flow Log captures traffic for:

**Network interfaces in that subnet**

Useful when you only need visibility into:

**A particular application tier**

---

# ENI-Level Flow Logs

A network-interface Flow Log captures traffic for:

**A specific ENI**

Useful when troubleshooting:

**A particular resource**

### Killer Exam Clue

> **Need traffic logs for one EC2 network interface**
>
> → **ENI-level VPC Flow Log**

---

# Flow Log Traffic Types

You can configure Flow Logs to capture:

- ACCEPT
- REJECT
- ALL

### Killer Shortcut

Need only blocked traffic  
→ REJECT

Need only successful traffic  
→ ACCEPT

Need both  
→ ALL

---

# Flow Logs Are Not Packet Capture

This distinction is extremely important.

Flow Logs provide:

**Metadata**

They do NOT provide:

**Packet payloads**

Example:

Flow Logs may tell you:

Source IP  
→ Destination IP  
→ TCP 443  
→ ACCEPT

They do not show:

**The actual HTTPS request body**

### Memory Trick

**Flow Logs = Envelope**

Not:

**Letter Inside**

---

# Flow Logs vs Packet Inspection

If the requirement involves:

**Deep inspection of network traffic**

think about services such as:

[[20-SAA/15-Security/Network Firewall]]

rather than Flow Logs.

### Killer Shortcut

**Observe traffic metadata**
→ VPC Flow Logs

**Inspect/block traffic**
→ Network Firewall

---

# CloudWatch Logs Destination

Flow Logs can publish to:

[[CloudWatch]] Logs

This enables:

- Log searching
- Metric filters
- Dashboards
- Alarms
- Operational troubleshooting

Architecture:

VPC Flow Logs  
↓  
CloudWatch Logs  
↓  
Search / Monitor / Alert

---

# S3 Destination

Flow Logs can also be delivered to:

[[S3]]

This is useful for:

- Long-term retention
- Large-scale analysis
- Historical investigation

Architecture:

VPC Flow Logs  
↓  
S3  
↓  
Athena / Analytics

---

# Flow Logs + Athena

A common architecture:

VPC Flow Logs  
↓  
S3  
↓  
[[Athena]]  
↓  
SQL Analysis

This allows administrators to query:

**Historical network traffic metadata**

### Killer Exam Clue

> **Need SQL queries against large volumes of historical VPC Flow Logs**
>
> → **S3 + Athena**

---

# Flow Logs + CloudWatch

Use CloudWatch when the requirement emphasizes:

- Operational monitoring
- Searching logs
- Alarms
- Near-real-time troubleshooting

### Memory Trick

**CloudWatch = Monitor**

**S3 + Athena = Analyze History**

---

# Troubleshooting Security Groups

Suppose:

Client  
↓  
EC2:443

fails.

Flow Log shows:

**REJECT**

Possible issue:

**Security Group**

You can inspect the resource's:

[[Security Groups]]

to determine whether:

**TCP 443 is allowed**

---

# Troubleshooting NACLs

Suppose:

Inbound request succeeds

but:

**Return traffic fails**

Possible issue:

[[NACL]]

because NACLs are:

**Stateless**

and may be blocking:

**Ephemeral ports**

### Killer Exam Pattern

> **Connection problem + REJECT + stateless subnet filtering**
>
> → Investigate NACL rules.

---

# Flow Logs + Security Groups

Security Groups determine:

**Whether resource-level traffic is allowed**

Flow Logs provide:

**Evidence about network flows**

### Memory Trick

**Security Group = Decide**

**Flow Logs = Record**

---

# Flow Logs + NACL

NACL:

**Allows or denies subnet traffic**

Flow Logs:

**Help investigate the resulting traffic**

### Memory Trick

**NACL = Gate**

**Flow Logs = Security Camera**

---

# Flow Logs + GuardDuty

[[GuardDuty]] can analyze network-related telemetry to detect:

**Suspicious activity**

Examples:

- Malicious IP communication
- Reconnaissance
- Command-and-control behavior

### Killer Shortcut

**Raw network metadata**
→ VPC Flow Logs

**Intelligent threat detection**
→ GuardDuty

---

# Flow Logs vs GuardDuty

## VPC Flow Logs

Think:

**Network traffic records**

## GuardDuty

Think:

**Threat detection**

### Example

Flow Logs:

> EC2 communicated with IP X.

GuardDuty:

> IP X is associated with malicious activity.

### Memory Trick

**Flow Logs = Evidence**

**GuardDuty = Detective**

---

# Flow Logs vs CloudTrail

This is one of the most important exam distinctions.

## [[CloudTrail]]

Records:

**AWS API activity**

Examples:

- Who terminated EC2?
- Who changed Security Group?
- Who created S3 bucket?

## VPC Flow Logs

Record:

**Network traffic metadata**

Examples:

- Who connected to EC2?
- Which IP attempted port 443?
- Was traffic accepted or rejected?

### Killer Shortcut

**API activity**
→ CloudTrail

**Network activity**
→ VPC Flow Logs

---

# Flow Logs vs CloudWatch

## CloudWatch

Think:

**Monitoring platform**

## VPC Flow Logs

Think:

**Network traffic data source**

Flow Logs can send data to:

**CloudWatch Logs**

### Memory Trick

**Flow Logs Generate**

**CloudWatch Stores/Monitors**

---

# Flow Logs vs WAF Logs

## [[WAF]]

logs focus on:

**Web requests**

Examples:

- URL
- HTTP request
- WAF rule
- Block/allow action

## VPC Flow Logs

focus on:

**Network flows**

Examples:

- IP
- Port
- Protocol
- ACCEPT/REJECT

### Killer Shortcut

**HTTP attack details**
→ WAF logs

**Network connection metadata**
→ VPC Flow Logs

---

# Flow Logs vs Network Firewall

## VPC Flow Logs

Observe:

**Network metadata**

## [[20-SAA/15-Security/Network Firewall]]

Inspect and potentially:

**Block traffic**

### Memory Trick

**Flow Logs = Observe**

**Network Firewall = Enforce**

---

# Flow Logs Are Not Real-Time Packet Capture

Flow Logs are intended for:

**Logging and analysis**

Do not interpret them as:

**A live packet-sniffing system**

### Exam Trap

If the question requires:

**Full packet capture**

VPC Flow Logs are not the answer.

---

# DNS Traffic Considerations

Not every type of AWS networking traffic appears exactly as you might expect in:

**VPC Flow Logs**

For SAA, focus on the main principle:

> **Flow Logs provide network-flow metadata, not a perfect packet-level record of every internal AWS interaction**

---

# Log Analysis

Flow Logs can help answer:

- Which hosts communicate most?
- Which ports are used?
- Which traffic is rejected?
- Is unexpected traffic reaching a subnet?
- Is a resource communicating externally?

---

# Security Investigation Example

Security team suspects an EC2 instance has unusual:

**Outbound traffic**

Flow Logs can help identify:

- Destination IPs
- Ports
- Protocols
- Traffic volume

Then services such as:

**GuardDuty**

can provide additional:

**Threat intelligence and detection**

---

# Architecture Thinking

## Scenario 1 — Connection Failure

Users cannot connect to:

EC2 on port 443.

Need to determine whether traffic is:

**Accepted or rejected**

Choose:

**VPC Flow Logs**

---

## Scenario 2 — API Investigation

Someone modified:

A Security Group.

Need to determine:

**Who made the API call**

Choose:

**CloudTrail**

not VPC Flow Logs.

---

## Scenario 3 — Malicious HTTP Request

Need details about:

**SQL injection requests**

Choose:

**WAF logs**

---

## Scenario 4 — Historical Network Analysis

Company stores:

Months of Flow Logs

and wants:

**SQL queries**

Choose:

VPC Flow Logs  
↓  
S3  
↓  
Athena

---

## Scenario 5 — Threat Detection

Need to automatically identify:

**Communication with known malicious IP addresses**

Choose:

**GuardDuty**

rather than manually analyzing Flow Logs.

---

## Scenario 6 — Packet Contents

Need to inspect:

**Actual packet payload**

VPC Flow Logs are:

**Not sufficient**

---

## Scenario 7 — One EC2 Instance

Need network-flow information for:

**One EC2 ENI**

Choose:

**ENI-level Flow Log**

---

# Scenario Recognition

Immediately think:

**VPC Flow Logs**

when you see:

- Network traffic metadata
- ACCEPT
- REJECT
- Source IP
- Destination IP
- Source/destination port
- Connectivity troubleshooting
- Network investigation
- ENI traffic logging

---

## Think CloudTrail When You See

- API call
- Who changed resource
- AWS account activity
- Audit history

---

## Think GuardDuty When You See

- Threat detection
- Malicious IP
- Suspicious behavior

---

## Think Network Firewall When You See

- Inspect traffic
- Block traffic
- Intrusion prevention

---

# Exam Traps

## Trap 1 — Flow Logs Capture Packet Payloads

❌

They capture:

**Metadata**

---

## Trap 2 — Flow Logs Block Traffic

❌

They:

**Observe and record**

---

## Trap 3 — Flow Logs Record AWS API Calls

❌

Think:

**CloudTrail**

---

## Trap 4 — Flow Logs Are the Same as GuardDuty

❌

Flow Logs:

**Network records**

GuardDuty:

**Threat detection**

---

## Trap 5 — ACCEPT Means the Application Successfully Processed the Request

❌

ACCEPT indicates the traffic passed relevant:

**Network controls**

It does not prove the application itself:

**Worked correctly**

---

## Trap 6 — REJECT Always Means Security Group

❌

Investigate:

- Security Groups
- NACLs
- Network configuration

---

# Quick Cheat Sheet

| Exam Clue | Answer |
|---|---|
| Network Traffic Metadata | VPC Flow Logs |
| ACCEPT / REJECT | VPC Flow Logs |
| Source / Destination IP | VPC Flow Logs |
| Network Troubleshooting | VPC Flow Logs |
| API Audit | CloudTrail |
| Threat Detection | GuardDuty |
| Packet Inspection | Network Firewall |
| Web Request Logging | WAF Logs |
| Historical SQL Analysis | S3 + Athena |
| Resource Firewall | Security Group |
| Subnet Firewall | NACL |

---

# Logging Decision Map

Need:

**Network traffic metadata**

→ VPC Flow Logs

Need:

**AWS API history**

→ CloudTrail

Need:

**Application/system metrics and logs**

→ CloudWatch

Need:

**Threat detection**

→ GuardDuty

Need:

**Web request security logs**

→ WAF Logs

Need:

**Advanced network inspection**

→ Network Firewall

---

# Final Exam Rapid-Fire

> **NETWORK TRAFFIC**
> → VPC FLOW LOGS
>
> **ACCEPT / REJECT**
> → VPC FLOW LOGS
>
> **SOURCE / DESTINATION IP**
> → VPC FLOW LOGS
>
> **NETWORK TROUBLESHOOTING**
> → VPC FLOW LOGS
>
> **API CALL**
> → CLOUDTRAIL
>
> **MALICIOUS ACTIVITY**
> → GUARDDUTY
>
> **PACKET INSPECTION**
> → NETWORK FIREWALL
>
> **SQL INJECTION LOG**
> → WAF
>
> **LONG-TERM FLOW ANALYSIS**
> → S3 + ATHENA

---

## Master Memory Trick

> [!tip] VPC Flow Logs Master Memory Trick
> Imagine your VPC is:
>
> **A highway system**
>
> Every car represents:
>
> **A NETWORK CONNECTION**
>
> VPC Flow Logs sit above the highway recording:
>
> **WHERE THE CAR CAME FROM**
>
> **WHERE IT WAS GOING**
>
> **WHICH LANE/PORT IT USED**
>
> and whether the checkpoint said:
>
> **ACCEPT**
>
> or:
>
> **REJECT**
>
> But Flow Logs do NOT open the car and inspect:
>
> **WHAT'S INSIDE**
>
> That's the difference between:
>
> **TRAFFIC METADATA**
>
> and:
>
> **PACKET CONTENT**

So remember:

> **VPC FLOW LOGS**
> → NETWORK EVIDENCE
>
> **CLOUDTRAIL**
> → API EVIDENCE
>
> **GUARDDUTY**
> → THREAT DETECTIVE
>
> **NETWORK FIREWALL**
> → TRAFFIC INSPECTOR
>
> **WAF**
> → WEB REQUEST INSPECTOR

And the killer SAA question:

> **"Does the requirement involve recording or troubleshooting source/destination network traffic and determining whether flows were accepted or rejected?"**
>
> YES
>
> → **VPC Flow Logs**

---

## Related Notes

- [[VPC]]
- [[Security Groups]]
- [[NACL]]
- [[CloudTrail]]
- [[CloudWatch]]
- [[GuardDuty]]
- [[20-SAA/15-Security/Network Firewall]]
- [[WAF]]
- [[Athena]]
- [[S3]]