## What Problem Does It Solve?

Security Groups control:

NETWORK TRAFFIC

into and out of EC2 instances.

Think:

INTERNET / OTHER RESOURCES

↓

SECURITY GROUP

↓

EC2 INSTANCE

### Memory Trick

Security Group = EC2 FIREWALL

---

## What Is a Security Group?

Security Groups are fundamental to:

NETWORK SECURITY IN AWS

They control how traffic is allowed:

INTO

and

OUT OF

EC2 instances.

Security Groups contain:

RULES

Rules can reference:

- IP addresses
- Other Security Groups

---

# Inbound vs Outbound

## Inbound Traffic

Inbound traffic means:

TRAFFIC COMING INTO THE INSTANCE

Think:

USER / SERVER

↓

SECURITY GROUP

↓

EC2

Examples:

SSH into EC2

HTTP request to web server

HTTPS request to web server

---

## Outbound Traffic

Outbound traffic means:

TRAFFIC LEAVING THE INSTANCE

Think:

EC2

↓

SECURITY GROUP

↓

OTHER DESTINATION

### Memory Trick

INBOUND = IN

OUTBOUND = OUT

---

# What Can Security Groups Control?

Security Groups regulate:

- Access to ports
- Authorized IPv4 ranges
- Authorized IPv6 ranges
- Inbound network traffic
- Outbound network traffic

Think:

WHO?

↓

IP / SECURITY GROUP

WHAT?

↓

PORT

WHICH DIRECTION?

↓

INBOUND / OUTBOUND

---

# Allow Rules Only

Security Groups contain:

ALLOW RULES

### Important

You do not create explicit deny rules in a Security Group.

Think:

RULE EXISTS

→ ALLOW

NO MATCHING ALLOW RULE

→ TRAFFIC DOESN'T GET THROUGH

### Memory Trick

Security Groups = ALLOW ONLY

---

# Default Traffic Behavior

Your course gives two important defaults:

### Inbound

ALL INBOUND TRAFFIC

↓

BLOCKED BY DEFAULT

### Outbound

ALL OUTBOUND TRAFFIC

↓

AUTHORIZED BY DEFAULT

### Memory Trick

IN = BLOCKED

OUT = ALLOWED

---

# Security Group Rules

A rule can define things such as:

TYPE

PROTOCOL

PORT RANGE

SOURCE

DESCRIPTION

Example:

HTTP

↓

TCP

↓

PORT 80

↓

Allowed Source

---

# Security Groups and Ports

Security Groups can control access to specific:

PORTS

For example:

Allow:

PORT 22

from:

YOUR IP ADDRESS

↓

You can SSH into the instance.

Another computer that isn't authorized:

↓

BLOCKED

---

# Classic Ports to Know

| Port | Protocol | Purpose |
| --- | --- | --- |
| 21 | FTP | Upload files into file share |
| 22 | SSH | Log into Linux |
| 22 | SFTP | Secure file transfer using SSH |
| 80 | HTTP | Unsecured website |
| 443 | HTTPS | Secured website |
| 3389 | RDP | Log into Windows |

---

## Port 22

SSH

=

SECURE SHELL

Used to:

LOG INTO LINUX

Also:

SFTP

uses SSH for secure file transfers.

### Memory Trick

22 = LINUX / SSH

---

## Port 80

HTTP

=

UNSECURED WEBSITE

### Memory Trick

80 = HTTP

---

## Port 443

HTTPS

=

SECURED WEBSITE

### Memory Trick

443 = SECURE WEB

---

## Port 3389

RDP

=

REMOTE DESKTOP PROTOCOL

Used to:

LOG INTO WINDOWS

### Memory Trick

3389 = WINDOWS

---

# Security Groups Can Be Reused

A Security Group can be attached to:

MULTIPLE INSTANCES

Think:

SECURITY GROUP

↓

EC2 #1

EC2 #2

EC2 #3

This makes Security Groups reusable.

---

# Region / VPC Scope

Your course states that Security Groups are locked to a:

REGION

+

VPC

combination.

### Memory Trick

Security Group belongs to:

REGION + VPC

---

# Security Groups Live Outside EC2

Security Groups operate:

OUTSIDE THE EC2 INSTANCE

If traffic is blocked by the Security Group:

THE EC2 INSTANCE DOESN'T SEE IT

Think:

BAD TRAFFIC

↓

SECURITY GROUP BLOCKS

❌

EC2 NEVER RECEIVES IT

---

# SSH Security Group

Your course recommends maintaining a:

SEPARATE SECURITY GROUP

for:

SSH ACCESS

This makes SSH access easier to control independently.

---

# Troubleshooting Security Groups

This is a very useful exam distinction.

## Timeout

Application is:

NOT ACCESSIBLE

and eventually:

TIMES OUT

Think:

SECURITY GROUP ISSUE

### Memory Trick

TIMEOUT = SECURITY GROUP

---

## Connection Refused

Application returns:

CONNECTION REFUSED

Think:

APPLICATION ERROR

or:

APPLICATION IS NOT RUNNING

### Memory Trick

REFUSED = APPLICATION

---

# Referencing Other Security Groups

A Security Group rule can reference:

ANOTHER SECURITY GROUP

instead of an IP address.

This is very useful when AWS resources need to communicate with each other.

Think:

EC2 WITH SG-A

↓

ALLOW TRAFFIC FROM SG-B

↓

ANY INSTANCE USING SG-B CAN MATCH THAT RULE

---

## Security Group Reference Example

Suppose:

Application EC2

↓

Security Group = APP-SG

Database EC2

↓

Security Group = DB-SG

DB-SG can allow:

APP-SG

on the required database port.

Think:

APP-SG

↓

ALLOWED BY DB-SG

↓

DATABASE

### Memory Trick

Security Group Reference = TRUST THE GROUP

---

# Why Security Group References Matter

Instead of depending on individual instance IP addresses:

IP #1

IP #2

IP #3

you can reference:

SECURITY GROUP

This is useful when instances change but remain associated with the appropriate Security Group.

---

# Security Group Diagram Logic

If Security Group 1 allows:

SECURITY GROUP 2

on:

PORT 123

Then an EC2 instance associated with Security Group 2 can communicate according to that rule.

An instance associated only with:

SECURITY GROUP 3

would not match that particular SG2 rule.

### Memory Trick

AUTHORIZED SG

→ PASS

OTHER SG

→ NO MATCH

---

# Scenario Recognition

Need firewall rules for an EC2 instance?

→ SECURITY GROUP

---

Need to allow HTTP traffic?

→ PORT 80

---

Need secure website traffic?

→ PORT 443

---

Need SSH access to Linux?

→ PORT 22

---

Need Remote Desktop access to Windows?

→ PORT 3389

---

Need to restrict SSH access to your own IP?

→ SECURITY GROUP INBOUND RULE

---

Need EC2 instances with one Security Group to access instances associated with another?

→ SECURITY GROUP REFERENCE

---

Application request times out?

→ CHECK SECURITY GROUP

---

Application says connection refused?

→ CHECK APPLICATION / WHETHER IT IS RUNNING

---

# Exam Traps

Security Groups

= ALLOW RULES ONLY

Inbound default

= BLOCKED

Outbound default

= AUTHORIZED

Security Group

= REGION + VPC

Security Groups can attach to:

MULTIPLE INSTANCES

Security Groups can reference:

IP

or

SECURITY GROUP

Blocked traffic:

EC2 DOESN'T SEE IT

TIMEOUT

= SECURITY GROUP

CONNECTION REFUSED

= APPLICATION

---

# Quick Cheat Sheet

SECURITY GROUP

= FIREWALL

INBOUND

= INTO EC2

OUTBOUND

= OUT OF EC2

RULES

= ALLOW ONLY

DEFAULT INBOUND

= BLOCKED

DEFAULT OUTBOUND

= ALLOWED

22

= SSH / SFTP

21

= FTP

80

= HTTP

443

= HTTPS

3389

= RDP

TIMEOUT

= SECURITY GROUP

CONNECTION REFUSED

= APPLICATION

SG REFERENCE

= ALLOW ANOTHER SECURITY GROUP

---

# Master Memory Trick

WHO CAN TALK?

↓

IP / SECURITY GROUP

ON WHAT?

↓

PORT

IN WHICH DIRECTION?

↓

INBOUND / OUTBOUND

Then remember:

INBOUND DEFAULT = BLOCK

OUTBOUND DEFAULT = ALLOW

TIMEOUT = SECURITY GROUP

REFUSED = APPLICATION

---

## Related Notes

- [[EC2]]
- [[SSH and EC2 Instance Connect]]
- [[Private vs Public IP]]
- [[Elastic Network Interfaces]]
- [[EC2 IAM Roles]]
- [[EC2 Comparison]]
- [[SAA EC2 Cheat Sheet]]