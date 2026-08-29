## What Problem Does It Solve?

ElastiCache may store:

FREQUENTLY ACCESSED APPLICATION DATA

↓

USER SESSIONS

↓

TOKENS

↓

TEMPORARY BUSINESS DATA

Because this data is accessed by applications over the network, you need to control:

WHO CAN REACH THE CACHE

↓

WHO CAN AUTHENTICATE

↓

HOW DATA IS PROTECTED IN TRANSIT

ElastiCache provides several security mechanisms including:

SECURITY GROUPS

↓

REDIS AUTH

↓

IAM AUTHENTICATION

↓

SSL / TLS

↓

MEMCACHED SASL

### Memory Trick

ELASTICACHE SECURITY

=

NETWORK + AUTH + ENCRYPTION

---

## Main ElastiCache Security Controls

Think:

NETWORK ACCESS

↓

SECURITY GROUPS

REDIS AUTHENTICATION

↓

REDIS AUTH

AWS IDENTITY AUTHENTICATION

↓

IAM AUTHENTICATION FOR REDIS

DATA IN TRANSIT

↓

SSL / TLS

MEMCACHED AUTHENTICATION

↓

SASL

### Memory Trick

SG

+

AUTH

+

TLS

=

CACHE SECURITY

---

## Security Groups

ElastiCache uses:

SECURITY GROUPS

to control:

NETWORK ACCESS

Think:

APPLICATION

↓

APPLICATION SECURITY GROUP

↓

ELASTICACHE SECURITY GROUP

The ElastiCache Security Group can allow traffic from:

ONLY THE APPLICATION SERVERS

that need access.

### Memory Trick

SECURITY GROUP

=

WHO CAN REACH THE CACHE

---

## Security Group Architecture

A common architecture is:

[Application Load Balancer](<Application Load Balancer>)

↓

EC2 APPLICATION INSTANCES

↓

EC2 SECURITY GROUP

↓

ELASTICACHE SECURITY GROUP

Instead of allowing:

ANY INTERNET CLIENT

to reach ElastiCache, configure the cache Security Group to allow:

ONLY THE APPLICATION SECURITY GROUP

### Memory Trick

APP SG

↓

CACHE SG

---

## Security Group Referencing

Your SAA architecture can use:

SECURITY GROUP REFERENCES

Think:

EC2 SECURITY GROUP

↓

ALLOWED BY

↓

ELASTICACHE SECURITY GROUP

This is better than relying on:

INDIVIDUAL EC2 IP ADDRESSES

because instances can:

SCALE OUT

↓

SCALE IN

↓

CHANGE IP ADDRESSES

while the Security Group relationship remains valid.

### Memory Trick

SG → SG

=

DYNAMIC NETWORK ACCESS

---

## Keep ElastiCache Private

ElastiCache is normally used as:

BACKEND INFRASTRUCTURE

Think:

INTERNET

↓

APPLICATION

↓

ELASTICACHE

NOT:

INTERNET

↓

ELASTICACHE DIRECTLY

The cache should generally only be reachable by:

AUTHORIZED APPLICATION RESOURCES

inside the VPC.

### Memory Trick

CACHE

=

PRIVATE BACKEND

---

## Redis AUTH

Redis supports:

REDIS AUTH

When creating a Redis cluster, you can configure:

PASSWORD / TOKEN

Think:

APPLICATION

↓

PASSWORD / TOKEN

↓

REDIS

↓

ACCESS GRANTED

This provides an additional authentication layer:

ON TOP OF SECURITY GROUPS

### Memory Trick

REDIS AUTH

=

CACHE PASSWORD

---

## Redis AUTH + Security Groups

Redis AUTH does not replace:

SECURITY GROUPS

Instead, they provide:

TWO DIFFERENT SECURITY LAYERS

Think:

SECURITY GROUP

=

CAN YOU REACH REDIS?

REDIS AUTH

=

CAN YOU AUTHENTICATE TO REDIS?

Architecture:

APPLICATION

↓

SECURITY GROUP ALLOWS CONNECTION

↓

REDIS AUTH TOKEN

↓

CACHE ACCESS

### Memory Trick

SG

=

REACH IT

AUTH

=

ENTER IT

---

## Defense in Depth

Using both:

SECURITY GROUPS

and:

REDIS AUTH

provides:

DEFENSE IN DEPTH

Think:

NETWORK SECURITY

↓

SECURITY GROUP

then:

APPLICATION AUTHENTICATION

↓

REDIS AUTH

If one control alone is insufficient:

THE SECOND CONTROL STILL HELPS

### Memory Trick

REDIS SECURITY

=

NETWORK WALL + PASSWORD

---

## IAM Authentication for Redis

ElastiCache supports:

IAM AUTHENTICATION

for:

REDIS

Think:

APPLICATION

↓

IAM IDENTITY

↓

REDIS AUTHENTICATION

This allows supported Redis deployments to use:

AWS IAM IDENTITY

for authentication.

### Memory Trick

IAM + REDIS

=

AWS IDENTITY TO CACHE

---

## IAM Authentication Architecture

Think:

EC2 / APPLICATION

↓

IAM ROLE

↓

ELASTICACHE REDIS

Instead of relying entirely on:

STATIC PASSWORDS

an application can use:

IAM-BASED AUTHENTICATION

### Memory Trick

IAM AUTH

=

AWS IDENTITY LOGIN

---

## IAM Authentication vs IAM Policies

This is an important SAA distinction.

IAM can be involved in two different ways:

IAM AUTHENTICATION FOR REDIS

and:

IAM POLICIES FOR ELASTICACHE API CALLS

These are not the same thing.

### Memory Trick

IAM AUTH

=

CONNECT TO REDIS

IAM POLICY

=

CONTROL AWS API ACTIONS

---

## IAM Policies and ElastiCache

Your course emphasizes:

IAM POLICIES ON ELASTICACHE

are used for:

AWS API-LEVEL SECURITY

Think:

IAM POLICY

↓

WHO CAN:

CREATE CLUSTER

↓

DELETE CLUSTER

↓

MODIFY CLUSTER

↓

VIEW CONFIGURATION

This controls management actions against the:

ELASTICACHE SERVICE API

### Memory Trick

IAM POLICY

=

MANAGE THE CACHE SERVICE

---

## API-Level Security

Imagine an administrator attempts to:

DELETE ELASTICACHE CLUSTER

AWS checks:

IAM POLICY

Think:

USER / ROLE

↓

AWS API REQUEST

↓

IAM POLICY

↓

ALLOW / DENY

This is different from an application attempting to:

READ DATA FROM REDIS

### Memory Trick

AWS CONTROL PLANE

=

IAM POLICY

CACHE CONNECTION

=

REDIS AUTH / IAM AUTH

---

## Control Plane vs Data Plane Thinking

### Control Plane

Actions such as:

CREATE

↓

DELETE

↓

MODIFY

↓

DESCRIBE

ElastiCache resources.

Security:

IAM POLICIES

---

### Data / Connection Access

Application connects to:

REDIS

Security may include:

SECURITY GROUPS

↓

REDIS AUTH

↓

IAM AUTHENTICATION

↓

TLS

### Memory Trick

MANAGE CACHE

=

IAM POLICY

USE CACHE

=

CACHE AUTHENTICATION

---

## SSL / TLS In-Flight Encryption

ElastiCache supports:

SSL / TLS

for:

ENCRYPTION IN TRANSIT

Think:

APPLICATION

↓

ENCRYPTED CONNECTION

↓

ELASTICACHE

This protects data while it moves:

ACROSS THE NETWORK

### Memory Trick

CACHE TRAFFIC

=

TLS

---

## Why In-Flight Encryption Matters

Without encryption:

APPLICATION DATA

↓

NETWORK

↓

CACHE

could potentially be exposed if traffic were intercepted.

With TLS:

APPLICATION DATA

↓

ENCRYPT

↓

NETWORK

↓

DECRYPT AT CACHE

### Memory Trick

TLS

=

PROTECT MOVING CACHE DATA

---

## Redis Security Architecture

A secure Redis architecture can look like:

APPLICATION

↓

SECURITY GROUP

↓

TLS CONNECTION

↓

IAM AUTHENTICATION / REDIS AUTH

↓

REDIS

Think:

NETWORK

↓

ENCRYPTION

↓

AUTHENTICATION

### Memory Trick

REDIS SECURITY

=

SG + TLS + AUTH

---

## Memcached Authentication

Memcached supports:

SASL-BASED AUTHENTICATION

Your course describes this as:

ADVANCED

Think:

APPLICATION

↓

SASL AUTHENTICATION

↓

MEMCACHED

### Memory Trick

MEMCACHED AUTH

=

SASL

---

## What Is SASL?

SASL stands for:

SIMPLE AUTHENTICATION AND SECURITY LAYER

For the SAA exam, the important association is:

MEMCACHED

↓

SASL

You do not need to deeply understand the SASL protocol.

### Memory Trick

MEMCACHED

=

SASL AUTH

---

## Redis AUTH vs Memcached SASL

### Redis

Authentication option:

REDIS AUTH

Think:

PASSWORD / TOKEN

---

### Memcached

Authentication option:

SASL

Think:

MEMCACHED AUTHENTICATION

### Memory Trick

REDIS

=

AUTH

MEMCACHED

=

SASL

---

## Redis IAM Auth vs Redis AUTH

Do not confuse:

IAM AUTHENTICATION

with:

REDIS AUTH

### IAM Authentication

Uses:

AWS IAM IDENTITY

Think:

IAM ROLE / AWS IDENTITY

---

### Redis AUTH

Uses:

PASSWORD / TOKEN

Think:

CACHE CREDENTIAL

### Memory Trick

IAM AUTH

=

AWS IDENTITY

REDIS AUTH

=

TOKEN / PASSWORD

---

## Security Groups vs Authentication

Do not confuse:

NETWORK ACCESS

with:

AUTHENTICATION

### Security Group

Determines:

CAN THIS CLIENT REACH THE CACHE?

### Authentication

Determines:

IS THIS CLIENT ALLOWED TO USE THE CACHE?

Think:

SECURITY GROUP

=

DOOR TO BUILDING

AUTHENTICATION

=

KEY TO ROOM

### Memory Trick

NETWORK

≠

IDENTITY

---

## ElastiCache vs RDS Security

Both commonly use:

SECURITY GROUPS

and:

ENCRYPTION

But their authentication models differ.

### RDS

Can use:

DATABASE USERNAME / PASSWORD

↓

IAM DATABASE AUTHENTICATION

---

### ElastiCache Redis

Can use:

REDIS AUTH

↓

IAM AUTHENTICATION

Think:

RDS

=

DATABASE LOGIN

REDIS

=

CACHE LOGIN

---

## ElastiCache vs RDS Proxy

Do not confuse:

CACHE SECURITY

with:

[RDS Proxy](<RDS Proxy>)

RDS Proxy can:

ENFORCE IAM AUTHENTICATION

and use:

[Secrets Manager](<Secrets Manager>)

for database credentials.

ElastiCache security focuses on protecting:

CACHE ACCESS

Think:

RDS PROXY

=

DATABASE CONNECTION SECURITY

ELASTICACHE

=

CACHE CONNECTION SECURITY

---

## Secure Web Architecture

Imagine:

USERS

↓

ALB SECURITY GROUP

↓

EC2 SECURITY GROUP

↓

ELASTICACHE SECURITY GROUP

Then:

EC2

↓

TLS

↓

REDIS

↓

IAM AUTH / REDIS AUTH

Think:

PUBLIC INTERNET ACCESS

STOPS AT:

LOAD BALANCER

The backend cache remains:

PRIVATE

### Memory Trick

PUBLIC

↓

ALB

PRIVATE

↓

APP + CACHE

---

## Scenario Recognition

Need to control which EC2 instances can reach ElastiCache?

→ Security Groups

---

Need cache network access restricted to application servers?

→ Allow Application Security Group in ElastiCache Security Group

---

Need Redis password / token authentication?

→ Redis AUTH

---

Need an extra security layer on top of Security Groups?

→ Redis AUTH

---

Need AWS identity-based authentication to Redis?

→ IAM Authentication

---

Need to control who can create or delete ElastiCache clusters?

→ IAM Policies

---

Need authorization for ElastiCache AWS API calls?

→ IAM Policies

---

Need cache traffic encrypted across the network?

→ SSL / TLS

---

Need Memcached authentication?

→ SASL

---

Need Redis authentication using password/token?

→ Redis AUTH

---

Need a private backend cache architecture?

→ ElastiCache + VPC Security Groups

---

## Exam Traps

ELASTICACHE SECURITY GROUP

=

NETWORK ACCESS

---

REDIS AUTH

=

PASSWORD / TOKEN

---

REDIS AUTH

=

EXTRA SECURITY ON TOP OF SECURITY GROUPS

---

IAM AUTHENTICATION

=

SUPPORTED FOR REDIS

---

IAM POLICY

=

AWS API-LEVEL SECURITY

---

IAM POLICY

≠

AUTOMATIC CACHE DATA ACCESS

---

IAM AUTH

=

AUTHENTICATE TO REDIS

IAM POLICY

=

MANAGE ELASTICACHE SERVICE

---

SSL / TLS

=

IN-FLIGHT ENCRYPTION

---

MEMCACHED

=

SASL AUTHENTICATION

---

SECURITY GROUP

≠

AUTHENTICATION

---

SECURITY GROUP

=

CAN REACH CACHE

AUTH

=

CAN USE CACHE

---

REDIS

=

REDIS AUTH / IAM AUTH

MEMCACHED

=

SASL

---

## Quick Cheat Sheet

ELASTICACHE SECURITY

=

SG + AUTH + TLS

SECURITY GROUP

=

NETWORK ACCESS

REDIS AUTH

=

PASSWORD / TOKEN

REDIS AUTH PURPOSE

=

EXTRA CACHE AUTHENTICATION

IAM AUTHENTICATION

=

REDIS AWS IDENTITY AUTH

IAM POLICIES

=

AWS API-LEVEL SECURITY

TLS / SSL

=

ENCRYPTION IN TRANSIT

MEMCACHED AUTH

=

SASL

CACHE PLACEMENT

=

PRIVATE BACKEND

APP ACCESS

=

APP SG → CACHE SG

CONTROL PLANE

=

IAM POLICY

REDIS CONNECTION AUTH

=

IAM AUTH / REDIS AUTH

---

## Master Memory Trick

ASK:

WHO CAN REACH THE CACHE?

↓

SECURITY GROUP

WHO CAN LOGIN TO REDIS?

↓

IAM AUTH

or:

REDIS AUTH

HOW DO I PROTECT NETWORK TRAFFIC?

↓

TLS

WHO CAN MANAGE ELASTICACHE THROUGH AWS?

↓

IAM POLICY

WHAT AUTH DOES MEMCACHED USE?

↓

SASL

Think:

SG

=

NETWORK

IAM / AUTH

=

IDENTITY

TLS

=

ENCRYPTION

SASL

=

MEMCACHED AUTH

### Final Rule

QUESTION SAYS:

REDIS PASSWORD / TOKEN

↓

REDIS AUTH

QUESTION SAYS:

AWS IDENTITY TO REDIS

↓

IAM AUTHENTICATION

QUESTION SAYS:

CREATE / DELETE / MODIFY ELASTICACHE

↓

IAM POLICY

QUESTION SAYS:

ENCRYPT CACHE NETWORK TRAFFIC

↓

TLS

QUESTION SAYS:

MEMCACHED AUTHENTICATION

↓

SASL

---

## Related Notes

- [ElastiCache Overview](<ElastiCache Overview>)
- [Redis vs Memcached](<Redis vs Memcached>)
- [ElastiCache Caching Strategies](<ElastiCache Caching Strategies>)
- [RDS & Aurora Security](<RDS & Aurora Security>)
- [RDS Proxy](<RDS Proxy>)
- [IAM](IAM)
- [EC2 Security Groups](<EC2 Security Groups>)
- [VPC](05-Networking/VPC.md)
- [SAA Databases Cheat Sheet](<SAA Databases Cheat Sheet>)