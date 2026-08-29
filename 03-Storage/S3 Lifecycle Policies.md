See also: [[S3]]

See also: [[03-Storage/S3 Storage Classes]]

See also: [[S3 Glacier]]

See also: [[S3 Glacier Deep Archive]]

## What Problem Does It Solve?

Helps optimize S3 storage costs by moving objects between storage classes as their access requirements change.

---

## Type

Storage Cost Optimization

---

## What Is an S3 Lifecycle Policy?

S3 Lifecycle configurations can automatically move objects between S3 storage classes.

Instead of manually changing the storage class of objects, lifecycle configurations can automate the process.

### Memory Trick

Lifecycle = Automatically Move Data to Cheaper Storage

---

## Manual vs Automatic Movement

Objects can move between S3 storage classes:

### Manually

You choose when to change the object's storage class.

### Automatically

Use:

S3 Lifecycle configurations

AWS then manages the storage-class transitions according to the lifecycle configuration.

---

## Why Use Lifecycle Policies?

Data often becomes less valuable to access immediately as it gets older.

Example:

New Data

↓

Frequently Accessed

↓

Less Frequently Accessed

↓

Archive

A lifecycle strategy can help move that data into more cost-effective storage classes.

---

## Example Lifecycle Concept

S3 Standard

↓

Standard-IA

↓

Glacier

↓

Glacier Deep Archive

The general idea is:

As data becomes less frequently accessed, move it into lower-cost storage.

---

## Relationship to Storage Classes

Lifecycle policies work together with:

[[03-Storage/S3 Storage Classes]]

Your storage-class choice depends on factors such as:

- Access frequency
- Retrieval requirements
- Availability requirements
- Cost

---

## Common Storage Progression

### Frequently Accessed

S3 Standard

↓

### Infrequently Accessed

Standard-IA

↓

### Archived

Glacier

↓

### Long-Term Archive

Glacier Deep Archive

---

## Lifecycle vs Intelligent-Tiering

These concepts are related but different.

### Lifecycle Configuration

You configure how objects should transition between storage classes.

### Intelligent-Tiering

AWS automatically moves objects between access tiers based on usage.

| Lifecycle | Intelligent-Tiering |
|---|---|
| Configuration-based | Usage-based |
| Used to transition objects | Automatically optimizes tiers |
| You define lifecycle strategy | AWS monitors access patterns |

### Memory Trick

Lifecycle = You Define the Strategy

Intelligent-Tiering = AWS Watches Usage

---

## Cost Optimization

Lifecycle configurations can reduce storage costs by preventing older or infrequently accessed data from remaining unnecessarily in more expensive storage classes.

### Example

Frequently used customer report

→ S3 Standard

Report becomes old

→ Standard-IA

Report becomes archival

→ Glacier

Report must be retained long term

→ Deep Archive

---

## Common Use Cases

- Long-term backups
- Archives
- Old application data
- Compliance records
- Data that becomes less frequently accessed over time

---

## Exam Scenarios

A company stores files in S3 Standard, but the files are rarely accessed after they become old.

→ Use S3 Lifecycle configurations

---

A company wants older S3 objects automatically moved into archival storage.

→ S3 Lifecycle configuration

---

A company does not know how frequently its S3 objects will be accessed and wants AWS to optimize access tiers automatically.

→ S3 Intelligent-Tiering

---

A company wants long-term archival storage at the lowest cost.

→ S3 Glacier Deep Archive

---

## Exam Keywords

Lifecycle

Transition

Storage class

Cost optimization

Archive

Automatic movement

---

## Memory Tricks

Lifecycle = Move Data Over Time

Standard → IA → Glacier → Deep Archive

Lifecycle = Cost Optimization

Intelligent-Tiering = AWS Watches Usage