## What Problem Does It Solve?

An Elastic Network Interface gives an EC2 instance:

NETWORK CONNECTIVITY

inside a:

VPC

Think:

EC2 INSTANCE

↓

ENI

↓

NETWORK

### Memory Trick

ENI = VIRTUAL NETWORK CARD

---

## What Is an ENI?

ENI stands for:

ELASTIC NETWORK INTERFACE

It is a:

LOGICAL COMPONENT

inside a:

VPC

that represents a:

VIRTUAL NETWORK CARD

### Memory Trick

ENI = NETWORK CARD FOR EC2

---

# ENI Attributes

An ENI can have:

- Primary private IPv4 address
- One or more secondary private IPv4 addresses
- One Elastic IP per private IPv4
- One public IPv4
- One or more Security Groups
- MAC address

Think:

ENI

↓

IP ADDRESSES

+

SECURITY GROUPS

+

MAC ADDRESS

---

# Primary Private IPv4

An ENI has a:

PRIMARY PRIVATE IPv4 ADDRESS

Example from the course diagram:

192.168.0.31

Think:

EC2

↓

PRIMARY ENI

↓

PRIMARY PRIVATE IP

---

# Secondary Private IPv4

An ENI can also have:

ONE OR MORE

SECONDARY PRIVATE IPv4 ADDRESSES

This means one network interface can have multiple private IP addresses.

### Memory Trick

ENI

= PRIMARY IP + OPTIONAL SECONDARY IPs

---

# Public IPv4

An ENI can have:

ONE PUBLIC IPv4

Remember:

PUBLIC IP

= INTERNET-FACING ADDRESSING

See:

[[Private vs Public IP]]

---

# Elastic IP

Your course states:

ONE ELASTIC IP

per:

PRIVATE IPv4

Remember:

[[Elastic IP]]

=

FIXED PUBLIC IPv4

---

# Security Groups

An ENI can have:

ONE OR MORE SECURITY GROUPS

Think:

ENI

↓

SECURITY GROUP

↓

NETWORK TRAFFIC RULES

Remember:

[[EC2 Security Groups]]

=

FIREWALL RULES

---

# MAC Address

An ENI also has a:

MAC ADDRESS

This is another network-interface attribute.

For the exam, simply remember:

ENI

↓

HAS MAC ADDRESS

---

# Primary vs Secondary ENI

Your course diagram shows:

ETH0

=

PRIMARY ENI

and:

ETH1

=

SECONDARY ENI

Think:

EC2

↓

ETH0

PRIMARY NETWORK INTERFACE

+

ETH1

ADDITIONAL NETWORK INTERFACE

---

# ENIs Can Be Created Independently

An ENI can be:

CREATED INDEPENDENTLY

from an EC2 instance.

Then it can be:

ATTACHED

to an EC2 instance.

### Memory Trick

ENI DOES NOT HAVE TO BE CREATED WITH EC2

---

# ENIs Can Be Moved

This is the major SAA scenario.

Your course states that ENIs can be:

ATTACHED ON THE FLY

and:

MOVED BETWEEN EC2 INSTANCES

This can be used for:

FAILOVER

Think:

EC2 INSTANCE A

↓

ENI

↓

INSTANCE A FAILS

↓

MOVE ENI

↓

EC2 INSTANCE B

### Memory Trick

ENI = MOVE NETWORK IDENTITY

---

# ENI Failover

Suppose:

EC2-A

has an ENI containing network configuration.

EC2-A fails.

You can move the ENI to:

EC2-B

Think:

EC2-A ❌

↓

MOVE ENI

↓

EC2-B ✅

This provides a failover mechanism.

### Exam Keyword

FAILOVER

+

MOVE NETWORK INTERFACE

→ ENI

---

# Availability Zone Restriction

This is extremely important.

ENIs are bound to a:

SPECIFIC AVAILABILITY ZONE

Think:

ENI in AZ-A

↓

STAYS IN AZ-A

### Memory Trick

ENI = AZ-BOUND

---

# ENI vs Elastic IP

Don't confuse these.

## ENI

= VIRTUAL NETWORK CARD

Can contain:

IP ADDRESSES

SECURITY GROUPS

MAC ADDRESS

---

## Elastic IP

= FIXED PUBLIC IPv4 ADDRESS

### Memory Trick

ENI

= CARD

ELASTIC IP

= ADDRESS

---

# ENI vs Security Group

## ENI

Provides:

NETWORK INTERFACE

## Security Group

Controls:

NETWORK TRAFFIC

Think:

EC2

↓

ENI

↓

SECURITY GROUP RULES

---

# ENI vs EC2

EC2

= COMPUTE

ENI

= NETWORK INTERFACE

Think:

SERVER

needs:

NETWORK CARD

EC2

needs:

ENI

---

# Scenario Recognition

Need a virtual network card for EC2?

→ ENI

---

Need multiple private IPv4 addresses associated with a network interface?

→ ENI

---

Need one or more Security Groups associated with a network interface?

→ ENI

---

Need to move a network interface from one EC2 instance to another?

→ ENI

---

Need EC2 failover by moving network configuration to another instance?

→ ENI

---

Need a fixed public IPv4 address?

→ ELASTIC IP

NOT simply ENI

---

Need to move an ENI to an instance in another Availability Zone?

→ NOT POSSIBLE

ENI IS AZ-BOUND

---

# Exam Traps

ENI

= VIRTUAL NETWORK CARD

ENI

= VPC COMPONENT

ENI

= AZ-BOUND

ENI

= CAN MOVE BETWEEN EC2 INSTANCES IN ITS AZ

ENI

= CAN HAVE MULTIPLE PRIVATE IPv4 ADDRESSES

ENI

= CAN HAVE SECURITY GROUPS

ENI

= HAS MAC ADDRESS

Elastic IP

≠ ENI

Security Group

≠ ENI

---

# Quick Cheat Sheet

ENI

= ELASTIC NETWORK INTERFACE

TYPE

= VIRTUAL NETWORK CARD

LOCATION

= VPC

PRIMARY IP

= PRIVATE IPv4

SECONDARY IPs

= ONE OR MORE

ELASTIC IP

= ONE PER PRIVATE IPv4

PUBLIC IP

= ONE

SECURITY GROUPS

= ONE OR MORE

MAC ADDRESS

= YES

FAILOVER

= MOVE ENI

SCOPE

= SPECIFIC AZ

---

# Master Memory Trick

EC2

= SERVER

ENI

= NETWORK CARD

ELASTIC IP

= FIXED PUBLIC ADDRESS

SECURITY GROUP

= FIREWALL

And remember:

ENI

↓

CAN MOVE

↓

FAILOVER

BUT

↓

STAYS IN SAME AZ

---

## Related Notes

- [[EC2]]
- [[Private vs Public IP]]
- [[Elastic IP]]
- [[EC2 Security Groups]]
- [[EC2 Placement Groups]]
- [[EC2 Comparison]]
- [[SAA EC2 Cheat Sheet]]