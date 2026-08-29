## What Problem Does It Solve?

Applications can open:

TOO MANY DATABASE CONNECTIONS

This is especially common with:

LAMBDA

or:

HIGHLY SCALABLE APPLICATIONS

Think:

THOUSANDS OF APPLICATION REQUESTS

↓

THOUSANDS OF DB CONNECTIONS

↓

DATABASE CPU / RAM STRESS

↓

TIMEOUTS

↓

POOR PERFORMANCE

RDS Proxy solves this by:

POOLING

and:

SHARING

database connections.

### Memory Trick

RDS PROXY

=

FEWER DATABASE CONNECTIONS

---

## What Is RDS Proxy?

RDS Proxy is a:

FULLY MANAGED DATABASE PROXY

that sits between:

APPLICATIONS

and:

RDS / AURORA

Think:

APPLICATION

↓

RDS PROXY

↓

DATABASE

Instead of every application connection creating:

A NEW DATABASE CONNECTION

RDS Proxy can reuse:

EXISTING DATABASE CONNECTIONS

### Memory Trick

PROXY

=

MIDDLE LAYER BETWEEN APP AND DB

---

## Connection Pooling

The most important RDS Proxy concept is:

CONNECTION POOLING

Think:

APPLICATION CONNECTION #1

APPLICATION CONNECTION #2

APPLICATION CONNECTION #3

APPLICATION CONNECTION #4

↓

RDS PROXY

↓

SMALLER POOL OF DATABASE CONNECTIONS

RDS Proxy maintains and reuses database connections.

### Memory Trick

POOL

=

REUSE CONNECTIONS

---

## Connection Sharing

RDS Proxy allows applications to:

SHARE DATABASE CONNECTIONS

Think:

MANY APP CONNECTIONS

↓

FEWER BACKEND DATABASE CONNECTIONS

This helps prevent the database from being overwhelmed by:

TOO MANY OPEN CONNECTIONS

### Memory Trick

MANY APP CONNECTIONS

↓

FEWER DB CONNECTIONS

---

## Why Too Many Connections Are Bad

Each database connection consumes:

DATABASE RESOURCES

such as:

CPU

↓

RAM

↓

CONNECTION SLOTS

If too many connections are opened:

DATABASE

↓

RESOURCE PRESSURE

↓

TIMEOUTS

↓

POOR PERFORMANCE

RDS Proxy reduces this pressure.

### Memory Trick

CONNECTIONS

=

DATABASE COST

POOLING

=

REDUCE PRESSURE

---

## Database Efficiency

RDS Proxy improves:

DATABASE EFFICIENCY

by reducing stress on:

CPU

and:

RAM

Think:

WITHOUT PROXY

↓

TOO MANY CONNECTIONS

↓

HIGH DB RESOURCE USAGE

WITH PROXY

↓

CONNECTION POOL

↓

LOWER CONNECTION OVERHEAD

### Memory Trick

RDS PROXY

=

PROTECT DATABASE RESOURCES

---

## RDS Proxy Architecture

Think:

APPLICATION SERVERS

↓

RDS PROXY

↓

RDS DATABASE

or:

APPLICATION SERVERS

↓

RDS PROXY

↓

AURORA

The application connects to:

THE PROXY

The proxy manages connections to:

THE DATABASE

### Memory Trick

APP

↓

PROXY

↓

DB

---

## RDS Proxy Is Fully Managed

RDS Proxy is:

FULLY MANAGED

You do not need to:

INSTALL

↓

PATCH

↓

MAINTAIN

your own database proxy infrastructure.

AWS manages the service.

Think:

DATABASE PROXY

↓

AWS MANAGED

---

## RDS Proxy Is Serverless

Your course describes RDS Proxy as:

SERVERLESS

Think:

NO PROXY SERVERS TO MANAGE

You do not provision and maintain:

EC2 PROXY INSTANCES

### Memory Trick

RDS PROXY

=

NO PROXY SERVERS TO MANAGE

---

## RDS Proxy Auto Scaling

RDS Proxy can:

AUTO SCALE

to handle changing connection demand.

Think:

APPLICATION CONNECTIONS ↑

↓

RDS PROXY SCALES

↓

DATABASE CONNECTION POOL MANAGED

This helps support:

HIGHLY VARIABLE APPLICATION LOAD

---

## RDS Proxy Is Highly Available

RDS Proxy is:

HIGHLY AVAILABLE

and:

MULTI-AZ

Think:

PROXY LAYER

↓

MULTIPLE AZs

↓

HIGH AVAILABILITY

### Memory Trick

RDS PROXY

=

SERVERLESS + AUTO SCALING + MULTI-AZ

---

## RDS Proxy and Failover

RDS Proxy can improve:

DATABASE FAILOVER

Your course highlights that it can reduce:

RDS / AURORA FAILOVER TIME

by up to:

66%

Think:

DATABASE FAILURE

↓

FAILOVER

↓

RDS PROXY

↓

APPLICATION RECOVERS FASTER

### Memory Trick

RDS PROXY

=

FASTER FAILOVER

---

## Preserving Connections

During failover, RDS Proxy helps:

PRESERVE APPLICATION CONNECTIONS

Think:

APPLICATION

↓

PROXY CONNECTION

↓

DATABASE FAILOVER

↓

PROXY MANAGES BACKEND CHANGE

This reduces disruption to:

APPLICATION CONNECTIONS

### Memory Trick

PROXY

=

SHIELD APP FROM DB FAILOVER

---

## Why Failover Is Faster

Without a proxy:

APPLICATION

↓

DATABASE CONNECTION BREAKS

↓

APPLICATION RECONNECTS

↓

NEW PRIMARY DISCOVERED

With RDS Proxy:

APPLICATION

↓

RDS PROXY

↓

PROXY MANAGES DATABASE CONNECTIONS

↓

NEW DATABASE TARGET

Think:

PROXY

=

CONNECTION ABSTRACTION

---

## Supported Databases

Your SAA slides highlight support for RDS engines such as:

MYSQL

↓

POSTGRESQL

↓

MARIADB

↓

MICROSOFT SQL SERVER

and Aurora:

MYSQL-COMPATIBLE

↓

POSTGRESQL-COMPATIBLE

### Memory Trick

RDS PROXY

=

RDS + AURORA SUPPORTED ENGINES

---

## IAM Authentication

RDS Proxy can enforce:

IAM AUTHENTICATION

Think:

APPLICATION

↓

IAM

↓

RDS PROXY

↓

DATABASE

This can reduce reliance on:

STATIC DATABASE PASSWORDS

### Memory Trick

RDS PROXY

=

IAM AUTH AVAILABLE

---

## Secrets Manager

RDS Proxy can securely use:

[Secrets Manager](<Secrets Manager>)

to store:

DATABASE CREDENTIALS

Think:

DATABASE USERNAME / PASSWORD

↓

SECRETS MANAGER

↓

RDS PROXY

### Memory Trick

DB CREDENTIALS

=

SECRETS MANAGER

---

## IAM + Secrets Manager Architecture

Think:

APPLICATION

↓

IAM AUTHENTICATION

↓

RDS PROXY

↓

SECRETS MANAGER CREDENTIALS

↓

RDS / AURORA

This combines:

IDENTITY-BASED ACCESS

with:

SECURE SECRET STORAGE

### Memory Trick

IAM

=

WHO CONNECTS

SECRETS MANAGER

=

WHERE DB SECRET LIVES

---

## No Code Changes for Most Applications

Your course notes that RDS Proxy requires:

NO CODE CHANGES

for most applications.

Typically the application changes its:

DATABASE ENDPOINT

to the:

RDS PROXY ENDPOINT

Think:

OLD

APPLICATION

↓

RDS ENDPOINT

NEW

APPLICATION

↓

RDS PROXY ENDPOINT

### Memory Trick

CHANGE CONNECTION TARGET

↓

USE PROXY

---

## RDS Proxy Is Never Publicly Accessible

This is an important exam point.

RDS Proxy is:

NEVER PUBLICLY ACCESSIBLE

It must be accessed from:

A VPC

Think:

INTERNET

↓

X

↓

RDS PROXY

Instead:

VPC

↓

APPLICATION

↓

RDS PROXY

↓

DATABASE

### Memory Trick

RDS PROXY

=

VPC ONLY

---

## Private Architecture

A common architecture is:

VPC

↓

PRIVATE SUBNET

↓

APPLICATION

↓

RDS PROXY

↓

RDS

Think:

DATABASE LAYER

=

PRIVATE

RDS Proxy should be treated as:

PRIVATE INFRASTRUCTURE

---

## RDS Proxy and Lambda

One of the most important use cases is:

LAMBDA

Lambda can scale:

VERY QUICKLY

Think:

10 FUNCTIONS

↓

100 FUNCTIONS

↓

1000 FUNCTIONS

If each Lambda function opens:

ITS OWN DATABASE CONNECTION

the database may be overwhelmed.

### Memory Trick

LAMBDA + RDS

=

THINK RDS PROXY

---

## Lambda Connection Problem

Imagine:

1000 LAMBDA INVOCATIONS

Each invocation opens:

1 DATABASE CONNECTION

Result:

1000 CONNECTIONS

↓

RDS

↓

CONNECTION EXHAUSTION

Instead:

1000 LAMBDA CONNECTIONS

↓

RDS PROXY

↓

POOLED DB CONNECTIONS

↓

RDS

### Memory Trick

LAMBDA BURST

↓

PROXY POOL

↓

PROTECT DB

---

## Lambda Must Be in the VPC

Because RDS Proxy is:

NEVER PUBLICLY ACCESSIBLE

a Lambda function using RDS Proxy must be deployed in:

THE VPC

Think:

LAMBDA

↓

VPC CONFIGURATION

↓

RDS PROXY

↓

RDS

### Memory Trick

LAMBDA + RDS PROXY

=

LAMBDA IN VPC

---

## Lambda Architecture

Think:

LAMBDA FUNCTIONS

↓

HIGH CONCURRENCY

↓

RDS PROXY

↓

CONNECTION POOL

↓

RDS DATABASE

RDS Proxy helps with:

SCALABILITY

↓

AVAILABILITY

↓

SECURITY

### Memory Trick

LAMBDA

+

RDS PROXY

=

SAFE DATABASE CONNECTION SCALING

---

## RDS Proxy vs Direct Database Connection

### Direct Connection

APPLICATION

↓

DATABASE

Every application may create:

ITS OWN DB CONNECTION

Potential problem:

TOO MANY CONNECTIONS

---

### RDS Proxy

APPLICATION

↓

PROXY

↓

DATABASE

Connections are:

POOLED

and:

SHARED

Think:

DIRECT

=

MORE CONNECTION PRESSURE

PROXY

=

CONNECTION MANAGEMENT

---

## RDS Proxy vs Read Replica

Do not confuse:

RDS PROXY

with:

[RDS Read Replicas](<RDS Read Replicas>)

### RDS Proxy

Purpose:

CONNECTION MANAGEMENT

Think:

TOO MANY CONNECTIONS

---

### Read Replica

Purpose:

READ SCALABILITY

Think:

TOO MANY READ QUERIES

### Memory Trick

CONNECTION PROBLEM

=

RDS PROXY

READ PROBLEM

=

READ REPLICA

---

## RDS Proxy vs Multi-AZ

### RDS Proxy

Improves:

CONNECTION MANAGEMENT

and:

FAILOVER EXPERIENCE

### Multi-AZ

Provides:

DATABASE HIGH AVAILABILITY

Think:

MULTI-AZ

=

STANDBY DATABASE

RDS PROXY

=

CONNECTION LAYER

### Memory Trick

MULTI-AZ

=

DB SURVIVES

PROXY

=

APP CONNECTS BETTER

---

## RDS Proxy vs ElastiCache

Do not confuse:

DATABASE CONNECTION POOLING

with:

DATA CACHING

### RDS Proxy

Caches / reuses:

DATABASE CONNECTIONS

NOT application data.

---

### ElastiCache

Caches:

APPLICATION DATA

in memory.

Think:

RDS PROXY

=

CONNECTIONS

ELASTICACHE

=

DATA

### Memory Trick

PROXY

≠

CACHE

---

## RDS Proxy Does Not Cache Query Results

A major exam trap:

RDS Proxy does:

NOT

exist to cache database query results.

Think:

QUERY

↓

DATABASE

RDS Proxy manages:

CONNECTIONS

not:

QUERY DATA CACHE

Need cached application data?

↓

[ElastiCache](ElastiCache)

### Memory Trick

RDS PROXY

=

CONNECTION POOL

NOT DATA CACHE

---

## High-Concurrency Architecture

Imagine:

API REQUESTS

↓

LAMBDA

↓

LAMBDA

↓

LAMBDA

↓

LAMBDA

↓

RDS PROXY

↓

RDS

Without Proxy:

EVERY FUNCTION

↓

NEW DB CONNECTION

With Proxy:

FUNCTIONS

↓

SHARED CONNECTION POOL

↓

DATABASE

This is ideal for:

BURSTY

and:

HIGH-CONCURRENCY

applications.

---

## Security Architecture

Think:

LAMBDA IN VPC

↓

IAM AUTHENTICATION

↓

RDS PROXY

↓

SECRETS MANAGER

↓

DATABASE CREDENTIALS

↓

RDS

This architecture reduces:

HARDCODED CREDENTIALS

and:

UNNECESSARY PUBLIC ACCESS

### Memory Trick

PROXY SECURITY

=

IAM + SECRETS MANAGER + VPC

---

## Failure Architecture

Normal operation:

APPLICATION

↓

RDS PROXY

↓

PRIMARY DATABASE

Then:

PRIMARY FAILS

↓

DATABASE FAILOVER

↓

RDS PROXY PRESERVES CONNECTIONS

↓

NEW PRIMARY

↓

APPLICATION RECOVERS FASTER

Think:

APP

↓

STAYS CONNECTED TO PROXY

while:

DATABASE BACKEND CHANGES

---

## Scenario Recognition

Application opens too many database connections?

→ RDS Proxy

---

Lambda functions overwhelm RDS with connections?

→ RDS Proxy

---

Need database connection pooling?

→ RDS Proxy

---

Need applications to share database connections?

→ RDS Proxy

---

Need to reduce CPU / RAM stress caused by connections?

→ RDS Proxy

---

Need fewer open database connections and fewer timeouts?

→ RDS Proxy

---

Need faster RDS / Aurora failover?

→ RDS Proxy

---

Question mentions reducing failover time by up to 66%?

→ RDS Proxy

---

Need IAM authentication to database through proxy?

→ RDS Proxy

---

Need database credentials securely stored?

→ Secrets Manager + RDS Proxy

---

Need publicly accessible database proxy?

→ RDS Proxy is NOT the answer

RDS Proxy is:

VPC ONLY

---

Need Lambda to access RDS Proxy?

→ Lambda must be configured in the VPC

---

Need to scale database reads?

→ Read Replica

NOT RDS Proxy

---

Need query result caching?

→ ElastiCache

NOT RDS Proxy

---

## Exam Traps

RDS PROXY

=

FULLY MANAGED DATABASE PROXY

---

RDS PROXY

=

CONNECTION POOLING

---

RDS PROXY

=

CONNECTION SHARING

---

RDS PROXY

=

REDUCES OPEN DB CONNECTIONS

---

RDS PROXY

=

REDUCES CPU / RAM PRESSURE

---

RDS PROXY

=

SERVERLESS

---

RDS PROXY

=

AUTO SCALING

---

RDS PROXY

=

HIGHLY AVAILABLE / MULTI-AZ

---

FAILOVER TIME

=

UP TO 66% REDUCTION

---

RDS PROXY

=

CAN PRESERVE CONNECTIONS DURING FAILOVER

---

IAM AUTHENTICATION

=

SUPPORTED

---

DATABASE CREDENTIALS

=

SECRETS MANAGER

---

PUBLIC ACCESS

=

NO

---

RDS PROXY

=

VPC ONLY

---

LAMBDA + RDS PROXY

=

LAMBDA MUST BE IN VPC

---

RDS PROXY

≠

READ REPLICA

---

RDS PROXY

≠

ELASTICACHE

---

RDS PROXY

=

CONNECTION CACHE / POOL

ELASTICACHE

=

DATA CACHE

---

## Quick Cheat Sheet

RDS PROXY

=

MANAGED DATABASE PROXY

PURPOSE

=

POOL + SHARE DATABASE CONNECTIONS

BENEFIT

=

FEWER OPEN CONNECTIONS

DATABASE STRESS

=

REDUCED CPU / RAM PRESSURE

SCALING

=

SERVERLESS + AUTO SCALING

AVAILABILITY

=

MULTI-AZ

FAILOVER

=

UP TO 66% FASTER

CONNECTIONS DURING FAILOVER

=

PRESERVED / BETTER MANAGED

IAM AUTHENTICATION

=

SUPPORTED

CREDENTIAL STORAGE

=

SECRETS MANAGER

PUBLIC ACCESS

=

NO

NETWORK

=

VPC ONLY

LAMBDA

=

MAJOR USE CASE

LAMBDA REQUIREMENT

=

DEPLOY IN VPC

READ REPLICA

=

READ SCALE

RDS PROXY

=

CONNECTION SCALE

ELASTICACHE

=

DATA CACHE

RDS PROXY

=

CONNECTION POOL

---

## Master Memory Trick

MANY APPLICATION CONNECTIONS

↓

RDS PROXY

↓

SMALLER SHARED CONNECTION POOL

↓

RDS / AURORA

Think:

1000 APP CONNECTIONS

↓

PROXY

↓

FEWER DB CONNECTIONS

Remember:

TOO MANY CONNECTIONS?

↓

RDS PROXY

TOO MANY READS?

↓

READ REPLICA

SLOW REPEATED DATA READS?

↓

ELASTICACHE

DATABASE FAILURE?

↓

MULTI-AZ

And:

LAMBDA

+

DATABASE

+

HIGH CONCURRENCY

↓

RDS PROXY

### Final Rule

RDS PROXY

=

POOL CONNECTIONS

↓

PROTECT DATABASE

↓

IMPROVE FAILOVER

↓

IAM + SECRETS MANAGER

↓

VPC ONLY

---

## Related Notes

- [RDS Overview](<RDS Overview>)
- [RDS Read Replicas](<RDS Read Replicas>)
- [RDS Multi-AZ](<RDS Multi-AZ>)
- [RDS & Aurora Security](<RDS & Aurora Security>)
- [Aurora](Aurora)
- [Aurora Serverless](<Aurora Serverless>)
- [ElastiCache](ElastiCache)
- [Secrets Manager](<Secrets Manager>)
- [IAM](IAM)
- [Lambda](02-Compute/Lambda.md)
- [VPC](05-Networking/VPC.md)
- [SAA Databases Cheat Sheet](<SAA Databases Cheat Sheet>)