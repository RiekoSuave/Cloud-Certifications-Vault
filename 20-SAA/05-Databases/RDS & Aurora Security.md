## What Problem Does It Solve?

Relational databases often contain:

SENSITIVE APPLICATION DATA

↓

CUSTOMER INFORMATION

↓

FINANCIAL DATA

↓

BUSINESS DATA

The database must be protected against:

UNAUTHORIZED ACCESS

↓

DATA EXPOSURE

↓

NETWORK ATTACKS

↓

CREDENTIAL THEFT

RDS and Aurora provide several security controls for:

DATA AT REST

↓

DATA IN TRANSIT

↓

AUTHENTICATION

↓

NETWORK ACCESS

↓

AUDITING

### Memory Trick

RDS / AURORA SECURITY

=

ENCRYPT + AUTHENTICATE + RESTRICT + AUDIT

---

## Main Security Layers

Think of RDS and Aurora security as:

ENCRYPTION AT REST

↓

KMS

ENCRYPTION IN FLIGHT

↓

TLS

AUTHENTICATION

↓

IAM / DATABASE CREDENTIALS

NETWORK ACCESS

↓

SECURITY GROUPS

AUDITING

↓

CLOUDWATCH LOGS

### Memory Trick

KMS

TLS

IAM

SG

LOGS

---

## Encryption at Rest

RDS and Aurora support:

ENCRYPTION AT REST

using:

[KMS](06-Security/KMS.md)

Think:

DATABASE DATA

↓

ENCRYPTED

↓

KMS KEY

Encryption can protect:

DATABASE STORAGE

↓

READ REPLICAS

↓

SNAPSHOTS

↓

BACKUPS

### Memory Trick

DATABASE AT REST

=

KMS

---

## Encryption Must Be Defined at Launch

Your SAA course emphasizes that encryption must be defined:

AT DATABASE LAUNCH TIME

Think:

CREATE DATABASE

↓

CHOOSE ENCRYPTION

↓

KMS KEY

### Memory Trick

ENCRYPTION

=

DECIDE AT CREATION

---

## Primary and Replica Encryption

If the primary database is:

ENCRYPTED

its replicas can also be:

ENCRYPTED

Think:

ENCRYPTED PRIMARY

↓

ENCRYPTED REPLICAS

But if the primary is:

NOT ENCRYPTED

the Read Replicas cannot simply be created as:

ENCRYPTED REPLICAS

### Memory Trick

UNENCRYPTED PRIMARY

↓

UNENCRYPTED REPLICA

---

## Encrypting an Existing Unencrypted Database

Suppose you already have:

UNENCRYPTED RDS DATABASE

You cannot simply:

TURN ENCRYPTION ON

for that existing database.

Instead:

UNENCRYPTED DATABASE

↓

CREATE SNAPSHOT

↓

COPY / RESTORE SNAPSHOT AS ENCRYPTED

↓

NEW ENCRYPTED DATABASE

Think:

DATABASE

↓

SNAPSHOT

↓

ENCRYPT

↓

RESTORE

### Memory Trick

NEED TO ENCRYPT EXISTING DB?

=

SNAPSHOT + RESTORE

---

## Encryption Migration Architecture

Think:

UNENCRYPTED RDS

↓

SNAPSHOT

↓

ENCRYPTED SNAPSHOT

↓

RESTORE

↓

NEW ENCRYPTED RDS

This is an important exam workflow.

### Memory Trick

NO DIRECT SWITCH

↓

SNAPSHOT FIRST

---

## Encryption in Flight

RDS and Aurora support:

ENCRYPTION IN FLIGHT

using:

TLS

Think:

APPLICATION

↓

TLS

↓

RDS / AURORA

This protects data while it travels:

OVER THE NETWORK

### Memory Trick

AT REST

=

KMS

IN FLIGHT

=

TLS

---

## TLS-Ready by Default

Your course highlights that RDS and Aurora are:

TLS-READY BY DEFAULT

Applications can use:

AWS TLS ROOT CERTIFICATES

on the client side.

Think:

APPLICATION

↓

TRUST AWS CERTIFICATE

↓

TLS CONNECTION

↓

DATABASE

### Memory Trick

TLS

=

ENCRYPT DATABASE CONNECTION

---

## At Rest vs In Flight

### At Rest

Protects:

STORED DATABASE DATA

Technology:

KMS

---

### In Flight

Protects:

NETWORK CONNECTIONS

Technology:

TLS

Think:

DISK

↓

KMS

NETWORK

↓

TLS

### Memory Trick

KMS

=

STORED DATA

TLS

=

MOVING DATA

---

## IAM Database Authentication

RDS and Aurora can support:

IAM AUTHENTICATION

Think:

APPLICATION / USER

↓

IAM

↓

DATABASE

Instead of relying only on:

STATIC DATABASE USERNAME + PASSWORD

IAM can be used to authenticate access to supported databases.

### Memory Trick

IAM DATABASE AUTH

=

AWS IDENTITY → DATABASE

---

## IAM Authentication Benefit

Traditional database login:

USERNAME

+

PASSWORD

With IAM Authentication:

IAM IDENTITY

↓

AUTHENTICATION TOKEN

↓

DATABASE CONNECTION

This can reduce reliance on:

LONG-LIVED DATABASE PASSWORDS

### Memory Trick

IAM AUTH

=

LESS STATIC PASSWORD DEPENDENCE

---

## IAM Authentication Architecture

Think:

EC2 / LAMBDA / APPLICATION

↓

IAM ROLE

↓

DATABASE AUTHENTICATION

↓

RDS / AURORA

This can help integrate database authentication with:

AWS IAM

### Exam Thinking

Question says:

CONNECT TO DATABASE USING IAM ROLE

instead of:

DATABASE PASSWORD

↓

THINK IAM DATABASE AUTHENTICATION

---

## IAM Authentication vs IAM Authorization

Do not confuse:

IAM DATABASE AUTHENTICATION

with:

DATABASE PERMISSIONS

IAM can authenticate:

WHO IS CONNECTING

But database-level permissions still determine:

WHAT THAT USER CAN DO

Think:

IAM

=

WHO ARE YOU?

DATABASE PRIVILEGES

=

WHAT CAN YOU DO?

### Memory Trick

IAM AUTH

=

LOGIN

DB PERMISSIONS

=

DATABASE ACCESS RIGHTS

---

## Security Groups

RDS and Aurora use:

SECURITY GROUPS

to control:

NETWORK ACCESS

Think:

APPLICATION SERVER

↓

SECURITY GROUP RULE

↓

RDS / AURORA

Security Groups determine:

WHO CAN REACH THE DATABASE PORT

### Memory Trick

DATABASE SECURITY GROUP

=

NETWORK FIREWALL

---

## Database Security Group Architecture

A common architecture is:

APPLICATION EC2

↓

APP SECURITY GROUP

↓

RDS SECURITY GROUP

Instead of allowing:

0.0.0.0/0

to the database port, you can allow traffic from:

THE APPLICATION SECURITY GROUP

Think:

APP SG

↓

DB SG

### Memory Trick

ALLOW APP

NOT THE INTERNET

---

## Security Group Referencing

A strong architecture often uses:

SECURITY GROUP REFERENCES

Example:

RDS SECURITY GROUP

allows inbound traffic from:

APPLICATION SECURITY GROUP

Think:

APPLICATION INSTANCES CHANGE

↓

SECURITY GROUP REMAINS SAME

↓

DATABASE ACCESS STILL WORKS

### Memory Trick

SG → SG

=

DYNAMIC ACCESS CONTROL

---

## Keep Databases Private

RDS and Aurora databases are commonly placed in:

PRIVATE SUBNETS

Think:

INTERNET

↓

APPLICATION TIER

↓

PRIVATE DATABASE

The database generally should not need:

DIRECT PUBLIC INTERNET ACCESS

### Memory Trick

DATABASE

=

PRIVATE BACKEND

---

## No SSH Access

Normal RDS and Aurora do:

NOT

provide SSH access to the underlying host.

Think:

MANAGED DATABASE

↓

AWS MANAGES OS

↓

NO SSH

### Memory Trick

RDS / AURORA

=

MANAGED

↓

NO SSH

---

## RDS Custom Exception

The important exception is:

[RDS Custom](<RDS Custom>)

RDS Custom allows more access to:

THE UNDERLYING DATABASE ENVIRONMENT

Think:

NORMAL RDS

↓

NO SSH

RDS CUSTOM

↓

LOWER-LEVEL ACCESS

### Memory Trick

NEED OS ACCESS?

↓

RDS CUSTOM

---

## Why No SSH?

RDS and Aurora are:

MANAGED DATABASE SERVICES

AWS manages:

OPERATING SYSTEM

↓

PATCHING

↓

DATABASE INFRASTRUCTURE

Therefore you do not normally manage the host through:

SSH

### Exam Thinking

Question requires:

OPERATING SYSTEM CUSTOMIZATION

or:

HOST-LEVEL ACCESS

↓

NORMAL RDS / AURORA MAY NOT FIT

Think:

RDS CUSTOM

or:

DATABASE ON EC2

---

## Audit Logs

RDS and Aurora can generate:

AUDIT LOGS

These logs can be sent to:

[CloudWatch Logs](<CloudWatch Logs>)

Think:

DATABASE ACTIVITY

↓

AUDIT LOGS

↓

CLOUDWATCH LOGS

This enables:

LONGER LOG RETENTION

and:

CENTRALIZED MONITORING

### Memory Trick

DATABASE AUDIT

=

CLOUDWATCH LOGS

---

## Why Send Logs to CloudWatch?

Sending database logs to CloudWatch can help with:

CENTRALIZED LOGGING

↓

MONITORING

↓

TROUBLESHOOTING

↓

LONGER RETENTION

Think:

DATABASE LOGS

↓

CLOUDWATCH

↓

SEARCH / RETAIN / MONITOR

---

## Security Architecture

A secure application architecture could look like:

USERS

↓

[Application Load Balancer](<Application Load Balancer>)

↓

APPLICATION INSTANCES

↓

TLS DATABASE CONNECTION

↓

RDS / AURORA

Database protection:

AT REST

↓

KMS

NETWORK

↓

SECURITY GROUP

AUTHENTICATION

↓

IAM

AUDITING

↓

CLOUDWATCH LOGS

### Memory Trick

DB SECURITY

=

KMS + TLS + IAM + SG + LOGS

---

## Defense in Depth

Do not rely on only:

ONE SECURITY CONTROL

A stronger architecture combines:

PRIVATE SUBNETS

↓

SECURITY GROUPS

↓

TLS

↓

KMS

↓

IAM AUTHENTICATION

↓

AUDIT LOGGING

Think:

MULTIPLE SECURITY LAYERS

↓

DEFENSE IN DEPTH

### Memory Trick

DATABASE SECURITY

=

LAYERS

---

## RDS Security vs Database on EC2

### RDS / Aurora

AWS manages:

UNDERLYING INFRASTRUCTURE

You control:

DATABASE ACCESS

↓

NETWORK ACCESS

↓

ENCRYPTION SETTINGS

↓

DATABASE USERS

---

### Database on EC2

You additionally manage:

OPERATING SYSTEM

↓

HOST SECURITY

↓

PATCHING

↓

SSH ACCESS

Think:

RDS / AURORA

=

LESS HOST MANAGEMENT

EC2 DATABASE

=

MORE CONTROL + MORE RESPONSIBILITY

---

## Authentication Decision

Need:

NORMAL DATABASE CREDENTIALS?

↓

DATABASE USERNAME / PASSWORD

Need:

AWS IDENTITY-BASED LOGIN?

↓

IAM DATABASE AUTHENTICATION

Need:

SECURE STORAGE FOR DATABASE PASSWORDS?

↓

[Secrets Manager](<Secrets Manager>)

Think:

IAM

=

IDENTITY

SECRETS MANAGER

=

STORE SECRET

---

## Encryption Decision

Need:

DATABASE FILES ENCRYPTED?

↓

KMS

Need:

NETWORK CONNECTION ENCRYPTED?

↓

TLS

Need:

EXISTING UNENCRYPTED DB ENCRYPTED?

↓

SNAPSHOT

↓

ENCRYPT SNAPSHOT

↓

RESTORE

### Memory Trick

STORAGE

=

KMS

NETWORK

=

TLS

OLD UNENCRYPTED DB

=

SNAPSHOT + RESTORE

---

## Scenario Recognition

Need RDS data encrypted at rest?

→ KMS

---

Need Aurora data encrypted at rest?

→ KMS

---

Need database traffic encrypted in transit?

→ TLS

---

Need client certificate trust for TLS connection?

→ AWS TLS Root Certificate

---

Need IAM role-based database authentication?

→ IAM Database Authentication

---

Need to avoid relying only on database passwords?

→ IAM Database Authentication

---

Need to restrict which application servers can connect to the database?

→ Security Groups

---

Need database accessible only from application servers?

→ Reference Application Security Group in Database Security Group

---

Need direct SSH into normal RDS?

→ Not supported

---

Need OS-level database host access?

→ RDS Custom

---

Need longer retention of database audit logs?

→ Send Audit Logs to CloudWatch Logs

---

Need to encrypt an existing unencrypted RDS database?

→ Snapshot and Restore as Encrypted

---

Need encrypted Read Replica from unencrypted primary?

→ Not directly supported

Encrypt the database first through:

SNAPSHOT + RESTORE

---

## Exam Traps

AT-REST ENCRYPTION

=

KMS

---

IN-FLIGHT ENCRYPTION

=

TLS

---

ENCRYPTION

=

DEFINED AT DATABASE CREATION

---

UNENCRYPTED PRIMARY

↓

CANNOT HAVE ENCRYPTED READ REPLICA DIRECTLY

---

EXISTING UNENCRYPTED DATABASE

↓

SNAPSHOT

↓

ENCRYPT

↓

RESTORE

---

IAM AUTHENTICATION

=

DATABASE LOGIN USING IAM

---

IAM AUTHENTICATION

≠

NETWORK SECURITY

---

SECURITY GROUP

=

NETWORK ACCESS

---

NORMAL RDS / AURORA

=

NO SSH

---

RDS CUSTOM

=

HOST-LEVEL ACCESS EXCEPTION

---

AUDIT LOGS

↓

CLOUDWATCH LOGS

---

KMS

≠

TLS

KMS

=

DATA AT REST

TLS

=

DATA IN TRANSIT

---

MULTI-AZ

≠

SECURITY FEATURE

MULTI-AZ

=

HIGH AVAILABILITY

---

READ REPLICA

≠

SECURITY FEATURE

READ REPLICA

=

READ SCALING

---

## Quick Cheat Sheet

AT REST

=

KMS

IN FLIGHT

=

TLS

DATABASE ENCRYPTION

=

CONFIGURE AT CREATION

PRIMARY UNENCRYPTED

=

REPLICAS CANNOT BE ENCRYPTED DIRECTLY

ENCRYPT EXISTING DB

=

SNAPSHOT + RESTORE ENCRYPTED

IAM AUTHENTICATION

=

IAM-BASED DATABASE LOGIN

SECURITY GROUPS

=

NETWORK ACCESS CONTROL

DATABASE PLACEMENT

=

PRIVATE SUBNET PREFERRED

NORMAL SSH

=

NO

RDS CUSTOM

=

HOST ACCESS EXCEPTION

AUDIT LOGS

=

CLOUDWATCH LOGS

LONGER LOG RETENTION

=

CLOUDWATCH LOGS

---

## Master Memory Trick

PROTECT DATABASE DATA:

AT REST?

↓

KMS

IN TRANSIT?

↓

TLS

WHO CAN LOGIN?

↓

IAM AUTHENTICATION

WHO CAN REACH DATABASE?

↓

SECURITY GROUP

NEED AUDIT HISTORY?

↓

CLOUDWATCH LOGS

NEED SSH?

↓

NOT NORMAL RDS / AURORA

↓

RDS CUSTOM

And remember:

UNENCRYPTED DATABASE

↓

SNAPSHOT

↓

ENCRYPT

↓

RESTORE

### Final Rule

KMS

=

ENCRYPT STORED DATA

TLS

=

ENCRYPT NETWORK TRAFFIC

IAM

=

AUTHENTICATE

SECURITY GROUP

=

CONTROL NETWORK

CLOUDWATCH LOGS

=

AUDIT

---

## Related Notes

- [RDS Overview](<RDS Overview>)
- [RDS Read Replicas](<RDS Read Replicas>)
- [RDS Multi-AZ](<RDS Multi-AZ>)
- [RDS Backups](<RDS Backups>)
- [Aurora](Aurora)
- [Aurora Database Cloning](<Aurora Database Cloning>)
- [RDS Custom](<RDS Custom>)
- [RDS Proxy](<RDS Proxy>)
- [KMS](06-Security/KMS.md)
- [IAM](IAM)
- [Secrets Manager](<Secrets Manager>)
- [CloudWatch Logs](<CloudWatch Logs>)
- [EC2 Security Groups](<EC2 Security Groups>)
- [SAA Databases Cheat Sheet](<SAA Databases Cheat Sheet>)