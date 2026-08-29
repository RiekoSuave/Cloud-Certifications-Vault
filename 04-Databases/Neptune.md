See also: [[Database Fundamentals]]

See also: [[RDS]]

See also: [[04-Databases/DynamoDB]]

## What Problem Does It Solve?

Provides a managed graph database for storing and analyzing highly connected data.

Neptune is designed for situations where the relationships between pieces of data are especially important.

### Memory Trick

Neptune = Relationships

---

## Type

Graph Database

---

## What Is Neptune?

Neptune is AWS's:

Fully managed graph database.

A graph database is optimized for storing and navigating relationships between data.

Instead of focusing primarily on rows and tables, graph databases focus on:

- Entities
- Connections
- Relationships

### Memory Trick

Graph Database = Connected Data

---

## Graph Database Concept

Think about a social network.

You have:

Person A

↓

Friends With

↓

Person B

↓

Friends With

↓

Person C

The relationships between people are just as important as the people themselves.

This is the type of problem a graph database is designed to solve.

---

## Highly Connected Data

Neptune is useful when data contains many complex relationships.

Examples:

Person

↓

Knows

↓

Person

↓

Purchased

↓

Product

↓

Recommended With

↓

Another Product

A graph database makes it easier to navigate these connections.

---

## High Availability

Your course describes Neptune as:

Highly available

with replication across:

3 Availability Zones

### Memory Trick

Neptune = Managed + Multi-AZ

---

## Read Replicas

Your course notes state that Neptune can support:

Up to 15 Read Replicas

These replicas can help:

- Scale reads
- Improve read performance

### Memory Trick

Read Replicas = More Read Capacity

---

## Social Networks

One of the easiest Neptune use cases to remember is:

Social Networking

Examples of relationships:

- Friends
- Followers
- Likes
- Connections
- Groups

### Exam Clue

Social Network + Relationships

→ Neptune

---

## Knowledge Graphs

Neptune can be used for:

Knowledge Graphs

A knowledge graph connects information based on relationships.

Example:

Person

↓

Works For

↓

Company

↓

Located In

↓

Country

### Memory Trick

Knowledge Graph = Connected Knowledge

---

## Fraud Detection

Neptune can help identify relationships between:

- Users
- Accounts
- Transactions
- Devices

This can help reveal suspicious patterns.

### Example

Account A

↓

Transfers Money To

↓

Account B

↓

Connected To

↓

Account C

↓

Suspicious Activity

### Exam Clue

Fraud + Complex Relationships

→ Neptune

---

## Recommendation Engines

Neptune can also support:

Recommendation Engines

Relationships between:

- Customers
- Products
- Purchases
- Preferences

can help determine recommendations.

Example:

Customer

↓

Purchased

↓

Product A

↓

Frequently Purchased With

↓

Product B

---

## Neptune vs RDS

### RDS

Relational database.

Designed around:

- Tables
- Rows
- SQL
- Structured relationships

### Neptune

Graph database.

Designed around:

Connected relationships.

| RDS | Neptune |
|---|---|
| Relational database | Graph database |
| Tables | Connected data |
| SQL workloads | Relationship-heavy workloads |
| Application database | Graph relationships |

### Memory Trick

RDS = Tables

Neptune = Relationships

---

## Neptune vs DynamoDB

### DynamoDB

NoSQL key-value database designed for massive scale and low latency.

### Neptune

Graph database designed for connected data.

| DynamoDB | Neptune |
|---|---|
| NoSQL key-value | Graph database |
| Massive scale | Complex relationships |
| Fast lookups | Relationship traversal |
| Application data | Connected data |

### Memory Trick

DynamoDB = Fast NoSQL

Neptune = Connected Data

---

## Neptune vs Redshift

### Neptune

Analyzes relationships between connected data.

### Redshift

Analyzes large datasets for business intelligence and data warehousing.

### Memory Trick

Neptune = Relationships

Redshift = Analytics

---

## Common Use Cases

- Social networks
- Knowledge graphs
- Fraud detection
- Recommendation engines

The common theme is:

Relationships

---

## Exam Scenarios

A company is building a social networking application and needs to analyze relationships between users.

→ Neptune

---

A company needs to build a knowledge graph containing highly connected information.

→ Neptune

---

A financial company wants to analyze relationships between accounts and transactions to detect fraud.

→ Neptune

---

An application needs to build recommendations based on relationships between users and products.

→ Neptune

---

An application needs a traditional relational SQL database.

→ RDS or Aurora

NOT Neptune

---

An application needs a massively scalable key-value NoSQL database.

→ DynamoDB

NOT Neptune

---

A company needs a data warehouse for large analytical queries.

→ Redshift

NOT Neptune

---

## Don't Confuse These

RDS = Relational SQL

Aurora = High-Performance Relational

DynamoDB = NoSQL Key-Value

Redshift = Data Warehouse

ElastiCache = In-Memory Cache

Neptune = Graph Database

---

## Exam Keywords

Graph database

Relationships

Connected data

Social networks

Knowledge graphs

Fraud detection

Recommendation engines

Multi-AZ

Read replicas

---

## Memory Tricks

Neptune = Relationships

Neptune = Graph Database

Graph = Connected Data

Social Network = Neptune

Knowledge Graph = Neptune

Fraud Relationships = Neptune

Recommendation Relationships = Neptune