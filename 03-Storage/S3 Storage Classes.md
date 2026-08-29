See also: [[S3]]

See also: [[S3 Lifecycle Policies]]

See also: [[S3 Glacier]]

See also: [[S3 Glacier Deep Archive]]

## What Problem Does It Solve?

Allows you to optimize S3 storage costs based on:

- How frequently data is accessed
- How quickly data must be retrieved
- Availability requirements
- How long data will be stored

Different types of data can be placed into different S3 storage classes.

---

## Type

Object Storage Classes

---

## Main S3 Storage Classes

Your course covers:

- S3 Standard
- S3 Standard-Infrequent Access (Standard-IA)
- S3 One Zone-Infrequent Access (One Zone-IA)
- S3 Intelligent-Tiering
- S3 Glacier Instant Retrieval
- S3 Glacier Flexible Retrieval
- S3 Glacier Deep Archive
- S3 Express One Zone

---

## Durability vs Availability

These two terms are different.

### Durability

Measures how likely your objects are to remain intact and not be lost.

S3 is designed for very high durability.

### Availability

Measures how readily accessible the service is when you need it.

Availability varies depending on the storage class.

### Memory Trick

Durability = Will my data survive?

Availability = Can I access it right now?

---

## S3 Standard

Designed for:

Frequently accessed data

### Key Features

- General-purpose storage
- Low latency
- High throughput
- High availability

### Common Use Cases

- Big data analytics
- Mobile applications
- Gaming applications
- Content distribution

### Memory Trick

Standard = Frequently Accessed

---

## S3 Standard-IA

IA stands for:

Infrequent Access

Designed for data that is accessed less frequently but still needs rapid access when requested.

### Key Features

- Lower storage cost than S3 Standard
- Rapid access when needed
- Designed for infrequently accessed data

### Common Use Cases

- Disaster recovery
- Backups

### Memory Trick

Standard-IA = Rarely Used but Still Need It Fast

---

## S3 One Zone-IA

Stores data in:

One Availability Zone

Unlike Standard-IA, the data is not stored across multiple Availability Zones.

### Best For

Data that:

- Is infrequently accessed
- Can be recreated
- Does not require Multi-AZ resilience

### Common Use Cases

- Secondary backup copies
- Re-creatable data

### Important Risk

If the Availability Zone is destroyed, the data can be lost.

### Memory Trick

One Zone-IA = Cheaper IA + One AZ

---

## S3 Intelligent-Tiering

Automatically moves objects between access tiers based on usage.

Designed for data with:

Unknown or changing access patterns

### Key Feature

AWS automatically optimizes where the object is stored based on access behavior.

### Memory Trick

Intelligent-Tiering = AWS Chooses the Tier

---

## Intelligent-Tiering Access Tiers

Your course identifies:

### Frequent Access

Default tier.

---

### Infrequent Access

Objects not accessed for:

30 days

---

### Archive Instant Access

Objects not accessed for:

90 days

---

### Archive Access

Optional archive tier.

---

### Deep Archive Access

Optional deep archive tier.

---

## Intelligent-Tiering Cost

Your course notes identify:

- Small monitoring and auto-tiering fee
- No retrieval charges for Intelligent-Tiering

---

## S3 Glacier Instant Retrieval

Designed for archival data that still needs:

Millisecond retrieval

### Best For

Archive data accessed approximately once per quarter.

### Minimum Storage Duration

90 days

### Memory Trick

Glacier Instant = Archive + Fast Retrieval

---

## S3 Glacier Flexible Retrieval

Designed for:

Cold archival storage

Retrieval does not need to be immediate.

Your course identifies retrieval options including:

- Expedited
- Standard
- Bulk

### Minimum Storage Duration

90 days

### Memory Trick

Glacier Flexible = Cold Storage

See:

[[S3 Glacier]]

---

## S3 Glacier Deep Archive

Designed for:

Long-term archival data that is very rarely accessed.

Provides the lowest-cost archival option covered in your course.

Retrieval can take many hours.

### Minimum Storage Duration

180 days

### Common Uses

- Compliance records
- Legal archives
- Long-term backups
- Rarely accessed data

### Memory Trick

Deep Archive = Put It Away and Forget It

See:

[[S3 Glacier Deep Archive]]

---

## S3 Express One Zone

Designed for:

High-performance workloads requiring extremely low latency.

Data is stored within:

One Availability Zone

### Key Characteristics

Your course identifies:

- Single-AZ storage
- Directory Buckets
- Very high request rates
- Single-digit millisecond latency
- Storage and compute can be located in the same AZ

### Common Use Cases

- Latency-sensitive applications
- Data-intensive applications
- AI/ML training
- Financial modeling
- Media processing
- HPC

### Memory Trick

Express One Zone = S3 Speed

---

## Storage Class Comparison

| Storage Class | Best For | Key Idea |
|---|---|---|
| Standard | Frequently accessed data | General purpose |
| Standard-IA | Infrequently accessed data | Multi-AZ + rapid access |
| One Zone-IA | Re-creatable infrequent data | One AZ |
| Intelligent-Tiering | Unknown access patterns | Automatic optimization |
| Glacier Instant | Archive needing fast retrieval | Millisecond archive |
| Glacier Flexible | Cold archives | Flexible retrieval |
| Deep Archive | Long-term archives | Lowest-cost archive |
| Express One Zone | High-performance workloads | Single-AZ speed |

---

## Choosing a Storage Class

Frequently accessed data?

→ S3 Standard

---

Infrequently accessed data that still needs rapid retrieval?

→ Standard-IA

---

Infrequently accessed data that can be recreated?

→ One Zone-IA

---

Don't know how frequently the data will be accessed?

→ Intelligent-Tiering

---

Archive data but need immediate retrieval?

→ Glacier Instant Retrieval

---

Cold archival data where retrieval can wait?

→ Glacier Flexible Retrieval

---

Long-term archive with very rare access?

→ Glacier Deep Archive

---

Need extremely high-performance S3 storage in one AZ?

→ S3 Express One Zone

---

## Lifecycle Connection

Objects can move between storage classes:

Manually

OR

Automatically using:

S3 Lifecycle configurations

See:

[[S3 Lifecycle Policies]]

---

## Exam Keywords

Frequent access

Infrequent access

One Availability Zone

Unknown access pattern

Automatic tiering

Archive

Cold storage

Millisecond retrieval

Long-term retention

High performance

---

## Memory Tricks

Standard = Frequent

Standard-IA = Infrequent + Multi-AZ

One Zone-IA = Infrequent + One AZ

Intelligent-Tiering = AWS Chooses

Glacier Instant = Archive + Fast

Glacier Flexible = Cold Storage

Deep Archive = Cheapest Archive

Express One Zone = S3 Speed