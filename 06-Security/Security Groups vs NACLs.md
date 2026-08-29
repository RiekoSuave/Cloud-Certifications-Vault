## What Problem Does It Solve?

Both Security Groups and Network ACLs control network traffic within a VPC.

They provide different layers of network security:

Security Group = Instance / ENI Level

NACL = Subnet Level

The CCP exam frequently tests the differences between them.

---

## Security Groups

Security Groups act as virtual firewalls for EC2 instances.

### Scope

Instance / ENI Level

### Rules

Allow Rules Only

Cannot create deny rules.

### Stateful

YES

If traffic is allowed in, the return traffic is automatically allowed out.

### Common Use Cases

- Web servers
- Databases
- Application servers

### Example

Allow:

HTTP (80)

HTTPS (443)

SSH (22)

to an EC2 instance.

### Memory Trick

Security Group = Security Guard at the Door

---

## Network ACLs (NACLs)

Network ACLs act as firewalls for subnets.

### Scope

Subnet Level

### Rules

Allow Rules

AND

Deny Rules

### Stateful

NO

NACLs are stateless.

Traffic must be explicitly allowed in both directions.

### Common Use Cases

- Blocking specific IP addresses
- Subnet-level traffic filtering
- Additional network security

### Example

Deny:

Specific malicious IP range

at the subnet level.

### Memory Trick

NACL = Neighborhood Gate

---

## Security Group vs NACL

| Feature | Security Group | NACL |
| --- | --- | --- |
| Scope | Instance / ENI | Subnet |
| Allow Rules | Yes | Yes |
| Deny Rules | No | Yes |
| Stateful | Yes | No |
| Return Traffic | Automatically allowed | Must be explicitly allowed |
| Best Association | Instance firewall | Subnet firewall |

---

## Stateful vs Stateless

### Security Group = Stateful

If inbound traffic is allowed:

Request

→ EC2 Instance

The response traffic is automatically allowed back out.

You do NOT need to create a separate rule for the return traffic.

### NACL = Stateless

Inbound and outbound traffic are evaluated separately.

If traffic needs to travel in both directions:

Inbound Rule

AND

Outbound Rule

must allow the traffic.

### Memory Trick

Stateful = Remembers

Stateless = Does NOT Remember

---

## CCP Scenario Questions

A company needs a firewall for an EC2 instance.

Answer:

Security Group

Reason:

Security Groups operate at the instance / ENI level.

---

A company needs to block a specific IP address.

Answer:

NACL

Reason:

NACLs support deny rules.

---

A company needs subnet-level traffic filtering.

Answer:

NACL

Reason:

NACLs operate at the subnet level.

---

Traffic is allowed inbound to an EC2 instance.

The return traffic should automatically be allowed.

Answer:

Security Group

Reason:

Security Groups are stateful.

---

A company needs both allow and deny network rules.

Answer:

NACL

Reason:

NACLs support both allow and deny rules.

---

A company needs an instance-level firewall that only uses allow rules.

Answer:

Security Group

---

## Don't Confuse These

Security Group = Instance / ENI

NACL = Subnet

Security Group = Stateful

NACL = Stateless

Security Group = Allow Only

NACL = Allow + Deny

---

## Exam Keywords

Security Group

Network ACL

NACL

Instance Level

ENI

Subnet Level

Stateful

Stateless

Allow Rules

Deny Rules

Inbound Traffic

Outbound Traffic

---

## Memory Tricks

Security Group = Security Guard at the Door

NACL = Neighborhood Gate

Instance / ENI = Security Group

Subnet = NACL

Stateful = Security Group

Stateless = NACL

Allow Only = Security Group

Allow + Deny = NACL

---

## Quick Cheat Sheet

Security Group = Instance / ENI

Security Group = Stateful

Security Group = Allow Rules Only

NACL = Subnet

NACL = Stateless

NACL = Allow + Deny Rules

Block Specific IP = NACL

Instance Firewall = Security Group

Subnet Firewall = NACL