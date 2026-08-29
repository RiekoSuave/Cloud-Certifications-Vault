See also: [[S3]]

See also: [[03-Storage/S3 Replication]]

## What Problem Does It Solve?

Protects S3 objects from accidental deletion or overwriting by maintaining multiple versions of the same object.

---

## Type

Data Protection / Object Version Management

---

## What Is S3 Versioning?

S3 Versioning allows multiple versions of an object to exist inside the same bucket.

Versioning is enabled at the:

Bucket level

### Memory Trick

Versioning = Keep old copies

---

## How Versioning Works

Suppose a bucket contains:

report.pdf

You upload a new file using the same object key:

report.pdf

Instead of permanently replacing the previous object, S3 creates another version.

Example:

report.pdf

↓

Version 1

Version 2

Version 3

Each version has its own:

Version ID

---

## Why Use Versioning?

Versioning helps protect against:

- Accidental overwrites
- Unintended deletes
- Application mistakes

It also makes it easier to:

- Restore previous versions
- Roll back changes

---

## Accidental Overwrite

Without versioning:

Original Object

↓

Overwrite

↓

Original data may be lost

With versioning:

Original Object

↓

Upload New Version

↓

Previous Version Remains

---

## Accidental Delete Protection

Versioning helps protect against unintended deletion because previous object versions can be recovered.

### Memory Trick

Accidental delete?

Versioning can save you.

---

## Version ID

When versioning is enabled, different versions of an object receive:

Version IDs

This allows S3 to distinguish between versions of the same object key.

---

## Existing Objects

Objects that existed before versioning was enabled have the version:

null

### Exam Detail

Versioning does not retroactively assign normal version IDs to objects that existed before it was enabled.

---

## Suspending Versioning

Versioning can be:

Suspended

However:

Suspending versioning does NOT delete previous versions.

Existing versions remain stored.

### Memory Trick

Suspend ≠ Delete

---

## Versioning and Replication

S3 Replication requires versioning.

Versioning must be enabled on:

- Source bucket
- Destination bucket

This applies to:

- Cross-Region Replication
- Same-Region Replication

See:

[[03-Storage/S3 Replication]]

---

## Best Practice

Your course notes identify enabling versioning as a best practice for S3 buckets.

It provides an additional layer of protection for stored objects.

---

## Common Use Cases

- Protecting important files
- Recovering accidentally deleted objects
- Recovering overwritten objects
- Rolling back changes
- Supporting S3 Replication

---

## Versioning vs Replication

### Versioning

Maintains multiple versions of objects.

### Replication

Copies objects to another bucket.

| Versioning | Replication |
|---|---|
| Protects object history | Creates copies elsewhere |
| Multiple object versions | Multiple buckets |
| Helps rollback | Helps replicate data |
| Required for replication | Depends on versioning |

---

## Exam Scenarios

A user accidentally overwrites an important S3 object and needs the previous copy.

→ S3 Versioning

---

A company wants protection against unintended S3 object deletion.

→ S3 Versioning

---

A company wants to easily roll back an S3 object to an earlier version.

→ S3 Versioning

---

A company wants to configure Cross-Region Replication.

What must first be enabled?

→ Versioning on both source and destination buckets

---

Versioning is suspended on a bucket.

What happens to existing versions?

→ They remain stored

---

An object existed before versioning was enabled.

What version does the original object have?

→ null

---

## Exam Keywords

Versioning

Version ID

Accidental deletion

Overwrite protection

Rollback

Bucket level

null version

Replication

---

## Memory Tricks

Versioning = Keep Old Copies

Same Key = New Version

Versioning = Bucket Level

Suspend ≠ Delete

Old Object Before Versioning = null

Replication Requires Versioning