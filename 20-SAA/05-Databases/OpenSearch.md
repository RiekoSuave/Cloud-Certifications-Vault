## What Problem Does It Solve?

Traditional databases are optimized for:

STORING

and:

RETRIEVING

structured data.

But applications may need:

FLEXIBLE SEARCH

across:

MANY DIFFERENT FIELDS

For example, DynamoDB queries are primarily based on:

PRIMARY KEYS

or:

INDEXES

But what if an application needs to search:

ANY FIELD

or:

PARTIAL MATCHES?

Think:

DYNAMODB

=

STORE / RETRIEVE DATA

OPENSEARCH

=

SEARCH DATA

### Memory Trick

OPENSEARCH

=

SEARCH ENGINE FOR YOUR DATA

---

## What Is OpenSearch?

OpenSearch is the successor to:

ELASTICSEARCH

It provides powerful:

SEARCH

and:

ANALYTICS

capabilities.

Think:

DATA

↓

INDEX

↓

SEARCH

↓

RESULTS

### Memory Trick

OPENSEARCH

=

SEARCH + ANALYTICS

---

## OpenSearch Search Capability

With OpenSearch, you can search:

ANY FIELD

including:

PARTIAL MATCHES

Think:

DATABASE ITEM

↓

NAME

DESCRIPTION

CATEGORY

LOCATION

OTHER FIELDS

↓

SEARCH ACROSS THEM

This differs from DynamoDB access patterns that depend primarily on:

PRIMARY KEYS

and:

INDEXES

### Memory Trick

ANY FIELD?

↓

OPENSEARCH

---

## Partial Matching

OpenSearch supports:

PARTIAL MATCHES

Think:

Stored value:

SOLUTIONS ARCHITECT

Search:

ARCHITECT

↓

MATCH

This makes OpenSearch useful when applications require:

FLEXIBLE TEXT SEARCH

### Memory Trick

PARTIAL TEXT SEARCH

=

OPENSEARCH

---

## OpenSearch Complements Other Databases

The SAA slides emphasize that OpenSearch is commonly used as:

A COMPLEMENT

to another database.

Think:

DATABASE

=

SOURCE OF DATA

OPENSEARCH

=

SEARCH LAYER

For example:

[[DynamoDB Overview]]

+

OPENSEARCH

### Memory Trick

DATABASE STORES

OPENSEARCH SEARCHES

---

## DynamoDB + OpenSearch

DynamoDB is excellent for:

KEY-BASED ACCESS

But OpenSearch can provide:

FLEXIBLE SEARCH

across DynamoDB data.

Think:

DYNAMODB TABLE

↓

[[DynamoDB Streams]]

↓

[[02-Compute/Lambda]]

↓

OPENSEARCH

The application can then use:

DYNAMODB API

to retrieve items

and:

OPENSEARCH API

to search items.

### Memory Trick

DYNAMODB

=

GET ITEM

OPENSEARCH

=

SEARCH ITEM

---

## DynamoDB OpenSearch Architecture

The course architecture shows:

APPLICATION

↓

DYNAMODB TABLE

↓

CRUD OPERATIONS

Changes then flow through:

DYNAMODB STREAM

↓

LAMBDA FUNCTION

↓

OPENSEARCH

Think:

DYNAMODB

↓

STREAM

↓

LAMBDA

↓

OPENSEARCH INDEX

### Memory Trick

DYNAMODB CHANGE

↓

STREAM

↓

LAMBDA

↓

SEARCH INDEX

---

## Why DynamoDB Streams?

When DynamoDB data changes:

CREATE

UPDATE

DELETE

[[DynamoDB Streams]]

captures those changes.

Think:

TABLE CHANGE

↓

STREAM EVENT

↓

LAMBDA

↓

UPDATE OPENSEARCH

This helps keep the:

SEARCH INDEX

synchronized with DynamoDB.

### Memory Trick

DYNAMODB STREAMS

=

FEED SEARCH INDEX

---

## Retrieve vs Search

The SAA architecture distinguishes:

RETRIEVE ITEMS

from:

SEARCH ITEMS

Think:

DYNAMODB API

=

RETRIEVE

OPENSEARCH API

=

SEARCH

This is an important architecture distinction.

### Memory Trick

KNOWN KEY?

↓

DYNAMODB

NEED SEARCH?

↓

OPENSEARCH

---

## OpenSearch Deployment Modes

The SAA slides identify two modes:

MANAGED CLUSTER

and:

SERVERLESS CLUSTER

Think:

OPENSEARCH

↓

MANAGED

or:

SERVERLESS

### Memory Trick

OPENSEARCH

=

MANAGED OR SERVERLESS

---

## Managed Cluster

One deployment option is:

MANAGED CLUSTER

Think:

OPENSEARCH CLUSTER

↓

AWS-MANAGED SERVICE

This provides the traditional:

CLUSTER-BASED

OpenSearch architecture.

### Memory Trick

MANAGED

=

CLUSTER

---

## Serverless Cluster

OpenSearch also supports:

SERVERLESS

Think:

SEARCH WORKLOAD

↓

SERVERLESS OPENSEARCH

This provides another deployment model without relying on the same traditional cluster-management approach.

### Memory Trick

OPENSEARCH

CAN BE:

SERVERLESS

---

## SQL Support

The SAA slide states that OpenSearch does:

NOT NATIVELY SUPPORT SQL

SQL functionality can be enabled using:

A PLUGIN

Think:

OPENSEARCH

≠

RELATIONAL SQL DATABASE

### Memory Trick

OPENSEARCH

=

SEARCH

NOT:

SQL DATABASE

---

## OpenSearch Data Ingestion

The SAA slides identify several services that can send data into OpenSearch:

DATA FIREHOSE

↓

AWS IOT

↓

CLOUDWATCH LOGS

Think:

DATA SOURCES

↓

OPENSEARCH

### Memory Trick

INGEST DATA

↓

SEARCH IT

---

## Data Firehose Integration

Data Firehose can deliver streaming data into:

OPENSEARCH

Think:

STREAMING DATA

↓

DATA FIREHOSE

↓

OPENSEARCH

The architecture can operate:

NEAR REAL TIME

### Memory Trick

FIREHOSE

↓

OPENSEARCH

=

NEAR REAL TIME

---

## CloudWatch Logs Integration

[[CloudWatch Logs]]

can send log data to:

OPENSEARCH

This enables:

SEARCH

and:

ANALYSIS

of application or infrastructure logs.

Think:

CLOUDWATCH LOGS

↓

OPENSEARCH

↓

SEARCH LOGS

### Memory Trick

SEARCH LOGS?

↓

OPENSEARCH

---

## CloudWatch Logs Pattern with Lambda

The course architecture shows:

CLOUDWATCH LOGS

↓

SUBSCRIPTION FILTER

↓

LAMBDA FUNCTION

↓

OPENSEARCH

This pattern provides:

REAL-TIME

processing.

### Memory Trick

LOGS

↓

SUBSCRIPTION FILTER

↓

LAMBDA

↓

OPENSEARCH

---

## CloudWatch Logs Pattern with Data Firehose

Another course architecture is:

CLOUDWATCH LOGS

↓

SUBSCRIPTION FILTER

↓

DATA FIREHOSE

↓

OPENSEARCH

This pattern operates:

NEAR REAL TIME

### Memory Trick

LOGS + FIREHOSE

=

NEAR REAL-TIME OPENSEARCH

---

## Real Time vs Near Real Time

The course makes an important distinction.

### Lambda Pattern

CLOUDWATCH LOGS

↓

SUBSCRIPTION FILTER

↓

LAMBDA

↓

OPENSEARCH

=

REAL TIME

---

### Data Firehose Pattern

CLOUDWATCH LOGS

↓

SUBSCRIPTION FILTER

↓

DATA FIREHOSE

↓

OPENSEARCH

=

NEAR REAL TIME

### Memory Trick

LAMBDA

=

REAL TIME

FIREHOSE

=

NEAR REAL TIME

---

## Kinesis Data Streams Integration

OpenSearch can also receive streaming data from:

KINESIS DATA STREAMS

The course shows multiple processing paths.

Think:

KINESIS DATA STREAMS

↓

PROCESSING

↓

OPENSEARCH

### Memory Trick

STREAM

↓

SEARCH

---

## Kinesis + Data Firehose Pattern

One architecture is:

KINESIS DATA STREAMS

↓

DATA FIREHOSE

↓

OPENSEARCH

This provides:

NEAR REAL-TIME

delivery.

### Memory Trick

KINESIS

↓

FIREHOSE

↓

OPENSEARCH

---

## Kinesis + Lambda Pattern

Another architecture is:

KINESIS DATA STREAMS

↓

LAMBDA

↓

OPENSEARCH

This provides:

REAL-TIME

processing.

### Memory Trick

KINESIS

↓

LAMBDA

↓

OPENSEARCH

---

## Data Transformation

The Kinesis architecture also shows:

LAMBDA

being used for:

DATA TRANSFORMATION

Think:

RAW STREAM DATA

↓

LAMBDA TRANSFORMATION

↓

OPENSEARCH

This allows data to be modified before:

INDEXING

### Memory Trick

TRANSFORM BEFORE SEARCH

=

LAMBDA

---

## AWS IoT Integration

The slides also identify:

AWS IOT

as an ingestion source for:

OPENSEARCH

Think:

IOT DATA

↓

OPENSEARCH

↓

SEARCH / ANALYTICS

### Memory Trick

IOT DATA

↓

SEARCH IT

---

## OpenSearch Security

The SAA slides highlight security through:

COGNITO

↓

IAM

↓

KMS

↓

TLS

Think:

AUTHENTICATION / ACCESS

↓

COGNITO + IAM

ENCRYPTION AT REST

↓

KMS

ENCRYPTION IN TRANSIT

↓

TLS

### Memory Trick

OPENSEARCH SECURITY

=

COGNITO + IAM + KMS + TLS

---

## Cognito Integration

OpenSearch can use:

COGNITO

for security.

Think:

USER ACCESS

↓

COGNITO

↓

OPENSEARCH

This is especially relevant when providing controlled access to:

SEARCH

or:

DASHBOARD

functionality.

### Memory Trick

OPENSEARCH USERS

↓

COGNITO

---

## IAM Integration

OpenSearch security also integrates with:

IAM

Think:

AWS IDENTITY

↓

IAM PERMISSIONS

↓

OPENSEARCH ACCESS

### Memory Trick

AWS ACCESS CONTROL

=

IAM

---

## KMS Encryption

OpenSearch supports:

KMS ENCRYPTION

Think:

DATA AT REST

↓

KMS

### Memory Trick

OPENSEARCH AT REST

=

KMS

---

## TLS Encryption

OpenSearch supports:

TLS

Think:

DATA IN TRANSIT

↓

TLS

### Memory Trick

OPENSEARCH IN TRANSIT

=

TLS

---

## OpenSearch Dashboards

OpenSearch includes:

OPENSEARCH DASHBOARDS

for:

VISUALIZATION

Think:

OPENSEARCH DATA

↓

DASHBOARDS

↓

VISUALIZE RESULTS

### Memory Trick

SEARCH DATA

↓

DASHBOARDS

↓

VISUALIZE

---

## Search Architecture Scenario

Imagine an e-commerce application stores products in:

DYNAMODB

Users need to search by:

PRODUCT NAME

DESCRIPTION

CATEGORY

PARTIAL TEXT

The application cannot rely only on:

PRIMARY KEY LOOKUPS

Architecture:

DYNAMODB

↓

DYNAMODB STREAMS

↓

LAMBDA

↓

OPENSEARCH

### Memory Trick

DYNAMODB + FLEXIBLE SEARCH

=

OPENSEARCH

---

## Log Analytics Scenario

A company stores application logs in:

CLOUDWATCH LOGS

Requirement:

SEARCH

and:

ANALYZE

those logs.

Architecture:

CLOUDWATCH LOGS

↓

SUBSCRIPTION FILTER

↓

LAMBDA / DATA FIREHOSE

↓

OPENSEARCH

### Memory Trick

SEARCH CLOUDWATCH LOGS

=

OPENSEARCH

---

## Streaming Search Scenario

A company receives:

CONTINUOUS STREAMING DATA

through:

KINESIS DATA STREAMS

Requirement:

MAKE DATA SEARCHABLE

Think:

KINESIS DATA STREAMS

↓

DATA FIREHOSE

or:

LAMBDA

↓

OPENSEARCH

### Memory Trick

STREAMING DATA + SEARCH

=

OPENSEARCH

---

## OpenSearch vs DynamoDB

Do not confuse:

[[DynamoDB Overview]]

with:

OPENSEARCH

### DynamoDB

Purpose:

NOSQL DATABASE

Access primarily through:

KEYS + INDEXES

---

### OpenSearch

Purpose:

SEARCH

Can search:

ANY FIELD

and:

PARTIAL MATCHES

### Memory Trick

DYNAMODB

=

DATABASE

OPENSEARCH

=

SEARCH

---

## OpenSearch vs DynamoDB Indexes

[[DynamoDB Indexes]]

provide:

ALTERNATIVE DYNAMODB QUERY PATTERNS

OpenSearch provides:

MORE FLEXIBLE SEARCH

Think:

KNOWN ACCESS PATTERN

↓

DYNAMODB INDEX

FLEXIBLE / PARTIAL SEARCH

↓

OPENSEARCH

### Memory Trick

INDEXED DYNAMODB QUERY

=

DYNAMODB INDEX

SEARCH ENGINE

=

OPENSEARCH

---

## OpenSearch vs Athena

Do not confuse:

OPENSEARCH

with:

[[09-Analytics/Athena]]

### OpenSearch

Purpose:

SEARCH / ANALYTICS

especially for:

INDEXED SEARCH DATA

---

### Athena

Purpose:

SERVERLESS SQL QUERIES

against data stored in:

S3

### Memory Trick

SEARCH INDEX

=

OPENSEARCH

SQL ON S3

=

ATHENA

---

## OpenSearch vs CloudWatch Logs

[[CloudWatch Logs]]

stores and manages:

LOG DATA

OpenSearch can provide:

SEARCH

and:

ANALYSIS

over ingested log data.

Think:

CLOUDWATCH LOGS

=

LOG SOURCE

OPENSEARCH

=

SEARCH / ANALYSIS

### Memory Trick

STORE LOGS

=

CLOUDWATCH LOGS

SEARCH LOGS

=

OPENSEARCH

---

## OpenSearch vs Relational Database

OpenSearch should not be selected simply because a question asks for:

SQL

or:

RELATIONAL TRANSACTIONS

OpenSearch is designed around:

SEARCH

and:

ANALYTICS

Think:

RELATIONAL DATA / TRANSACTIONS

↓

RDS / AURORA

SEARCH ANY FIELD

↓

OPENSEARCH

### Memory Trick

TRANSACTIONS

=

RELATIONAL DATABASE

SEARCH

=

OPENSEARCH

---

## When Should You Think OpenSearch?

Look for requirements such as:

SEARCH ANY FIELD

↓

PARTIAL MATCHES

↓

FULL / FLEXIBLE SEARCH

↓

SEARCH DYNAMODB DATA

↓

SEARCH LOG DATA

↓

INDEX STREAMING DATA

↓

VISUALIZE SEARCH DATA

These strongly point toward:

OPENSEARCH

### Memory Trick

QUESTION SAYS:

SEARCH

↓

THINK OPENSEARCH

---

## Scenario Recognition

Need to search any field?

→ OpenSearch

---

Need partial matching?

→ OpenSearch

---

Need flexible search over DynamoDB data?

→ DynamoDB + DynamoDB Streams + Lambda + OpenSearch

---

Need DynamoDB primary-key retrieval?

→ [[DynamoDB Overview]]

---

Need alternative DynamoDB key-based query patterns?

→ [[DynamoDB Indexes]]

---

Need to search CloudWatch log data?

→ CloudWatch Logs → OpenSearch

---

Need real-time CloudWatch Logs ingestion?

→ Subscription Filter → Lambda → OpenSearch

---

Need near real-time CloudWatch Logs ingestion?

→ Subscription Filter → Data Firehose → OpenSearch

---

Need near real-time Kinesis delivery to OpenSearch?

→ Kinesis Data Streams → Data Firehose → OpenSearch

---

Need real-time Kinesis processing into OpenSearch?

→ Kinesis Data Streams → Lambda → OpenSearch

---

Need OpenSearch visualizations?

→ OpenSearch Dashboards

---

Need OpenSearch authentication/access security?

→ Cognito + IAM

---

Need OpenSearch encryption at rest?

→ KMS

---

Need OpenSearch encryption in transit?

→ TLS

---

Need serverless SQL against S3?

→ [[09-Analytics/Athena]]

NOT OpenSearch

---

## Exam Traps

OPENSEARCH

=

SUCCESSOR TO ELASTICSEARCH

---

OPENSEARCH

=

SEARCH ANY FIELD

---

OPENSEARCH

=

PARTIAL MATCHES

---

OPENSEARCH

=

COMMONLY COMPLEMENTS ANOTHER DATABASE

---

OPENSEARCH MODES

=

MANAGED CLUSTER

+

SERVERLESS CLUSTER

---

OPENSEARCH

=

DOES NOT NATIVELY SUPPORT SQL

---

SQL

=

PLUGIN CAN ENABLE IT

---

INGESTION SOURCES

=

DATA FIREHOSE

AWS IOT

CLOUDWATCH LOGS

---

SECURITY

=

COGNITO

+

IAM

+

KMS

+

TLS

---

VISUALIZATION

=

OPENSEARCH DASHBOARDS

---

DYNAMODB + OPENSEARCH

=

STREAMS + LAMBDA PATTERN

---

LAMBDA INGESTION

=

REAL TIME

---

DATA FIREHOSE INGESTION

=

NEAR REAL TIME

---

OPENSEARCH

≠

PRIMARY DATABASE REPLACEMENT

---

OPENSEARCH

≠

ATHENA

---

OPENSEARCH

≠

DYNAMODB INDEX

---

## Quick Cheat Sheet

OPENSEARCH

=

SEARCH + ANALYTICS

PREDECESSOR

=

ELASTICSEARCH

SEARCH

=

ANY FIELD

MATCHING

=

PARTIAL MATCHES SUPPORTED

COMMON PATTERN

=

COMPLEMENT ANOTHER DATABASE

DEPLOYMENT

=

MANAGED CLUSTER OR SERVERLESS

SQL

=

NOT NATIVE

INGESTION

=

DATA FIREHOSE + AWS IOT + CLOUDWATCH LOGS

SECURITY

=

COGNITO + IAM + KMS + TLS

VISUALIZATION

=

OPENSEARCH DASHBOARDS

DYNAMODB PATTERN

=

DYNAMODB → STREAMS → LAMBDA → OPENSEARCH

CLOUDWATCH REAL TIME

=

LOGS → LAMBDA → OPENSEARCH

CLOUDWATCH NEAR REAL TIME

=

LOGS → DATA FIREHOSE → OPENSEARCH

KINESIS REAL TIME

=

KINESIS → LAMBDA → OPENSEARCH

KINESIS NEAR REAL TIME

=

KINESIS → DATA FIREHOSE → OPENSEARCH

DYNAMODB

=

STORE / RETRIEVE

OPENSEARCH

=

SEARCH

ATHENA

=

SQL ON S3

---

## Master Memory Trick

Think:

DATABASE

↓

STORE DATA

OPENSEARCH

↓

SEARCH DATA

Then:

DYNAMODB

↓

STREAMS

↓

LAMBDA

↓

OPENSEARCH

And remember:

ANY FIELD

+

PARTIAL MATCH

=

OPENSEARCH

For streaming:

LAMBDA

=

REAL TIME

DATA FIREHOSE

=

NEAR REAL TIME

### Final Rule

QUESTION SAYS:

SEARCH ANY FIELD

+

PARTIAL MATCHES

↓

OPENSEARCH

QUESTION SAYS:

DYNAMODB

+

FLEXIBLE SEARCH

↓

DYNAMODB STREAMS

↓

LAMBDA

↓

OPENSEARCH

QUESTION SAYS:

SEARCH / ANALYZE LOGS

↓

CLOUDWATCH LOGS

↓

OPENSEARCH

QUESTION SAYS:

SERVERLESS SQL ON S3

↓

ATHENA

---

## Related Notes

- [[DynamoDB Overview]]
- [[DynamoDB Streams]]
- [[DynamoDB Indexes]]
- [[02-Compute/Lambda]]
- [[CloudWatch Logs]]
- [[09-Analytics/Athena]]
- [[20-SAA/10-Messaging/Kinesis Data Streams]]
- [[Data Firehose]]
- [[Cognito]]
- [[IAM]]
- [[06-Security/KMS]]
- [[SAA Databases Cheat Sheet]]