## What Problem Does It Solve?

[[S3 Versioning]] protects objects from:

- Accidental overwrites
- Unintended deletes
- Application mistakes
- User mistakes

It solves the problem of:

> **"How can I recover an older copy of an S3 object after it has been changed or deleted?"**

Think:

Original Object  
↓ overwrite  
New Version Created  
↓  
Old Version Still Exists

> [!tip] Memory Trick
> **Versioning = Undo Button for S3**

---

## Versioning Is Enabled at the Bucket Level

Versioning is configured on an:

**S3 Bucket**

Once enabled, S3 keeps multiple versions of objects that share the same key.

Example:

s3://my-bucket/report.pdf

Upload 1  
↓  
Version 1

Upload 2  
↓  
Version 2

Upload 3  
↓  
Version 3

The object key stays the same:

report.pdf

but S3 maintains different:

**Version IDs**

---

## Same Key Overwrite Creates a New Version

Without versioning:

report.pdf  
↓ overwrite  
Old content replaced

With versioning:

report.pdf  
↓ upload new content  
New Version Created

Conceptually:

report.pdf

├── Version 1  
├── Version 2  
└── Version 3 ← Current

The previous object is not immediately destroyed.

> [!tip] Architecture Thinking
> **Same key + Versioning = New version, not destructive overwrite**

---

## Why Versioning Is a Best Practice

The Maarek slides call versioning a:

**Best practice for S3 buckets**

because it makes recovery much easier.

Benefits include:

- Restore accidentally deleted objects
- Roll back accidental overwrites
- Recover previous application data
- Protect against human error

---

# Recovering from an Accidental Overwrite

Suppose:

Version 1:

Correct report

Then someone uploads:

Version 2:

Incorrect report

With Versioning:

report.pdf  
├── Version 1 → Correct  
└── Version 2 → Incorrect Current Version

You can restore the older version.

### Architecture Thinking

Accidental overwrite  
↓  
Find previous version  
↓  
Restore / Copy previous version  
↓  
Application recovers

Without Versioning:

The previous object may be lost.

---

# Recovering from Accidental Deletes

Versioning also protects against many accidental deletes.

When you delete the current object in a versioned bucket:

S3 generally adds a:

**Delete Marker**

instead of immediately destroying every previous version.

Example:

report.pdf  
├── Version 1
├── Version 2
└── Delete Marker ← Current

To normal requests:

report.pdf appears deleted.

But older versions remain in the bucket.

---

## Delete Marker

A Delete Marker effectively hides the previous versions.

Think:

Previous Versions  
↓  
Delete Marker placed on top  
↓  
Object appears deleted

The underlying versions can still be recovered.

> [!tip] Memory Trick
> **Delete Marker = Curtain, not shredder**

The object looks gone, but the previous versions are still behind the curtain.

---

## Restoring a Deleted Object

Suppose:

report.pdf  
├── Version 1
├── Version 2
└── Delete Marker

Removing the Delete Marker can expose the previous current version again.

Conceptually:

Delete Marker Removed  
↓  
Version 2 becomes visible again

This is why Versioning provides strong protection against accidental deletion.

---

# Permanently Deleting a Version

Versioning does not make objects impossible to delete.

An individual object version can still be:

**Permanently deleted**

If you explicitly delete a particular Version ID:

Version 1  
↓  
Permanent Delete  
↓  
Version 1 is gone

That is different from simply deleting the current object name and creating a Delete Marker.

### Exam Distinction

**Delete object normally → Delete Marker**

**Delete specific Version ID → Permanent deletion**

---

# Version IDs

Every versioned object receives a:

**Version ID**

Example:

report.pdf

Version ID:

abc123

Another upload:

report.pdf

Version ID:

xyz789

S3 uses these IDs to distinguish multiple copies that use the same object key.

---

# Objects Created Before Versioning

This is a sneaky exam detail.

Suppose a bucket contains objects before Versioning is enabled.

Those existing objects have:

**Version ID = null**

After Versioning is enabled:

New versions receive actual Version IDs.

Example:

Before Versioning:

report.pdf  
↓  
Version ID = null

After Versioning enabled and overwritten:

report.pdf  
├── Version ID = null
└── Version ID = abc123

> [!warning] Exam Rule
> **Pre-versioning objects → null version**

---

# Suspending Versioning

Once Versioning has been enabled, you can:

**Suspend Versioning**

Important:

Suspending Versioning does **not** delete previous versions.

Example:

Versioning Enabled  
↓  
Multiple versions created  
↓  
Versioning Suspended  
↓  
Previous versions remain

### Memory Trick

**Suspend ≠ Delete History**

---

## Why Suspension Matters

An exam question may imply:

> "Disable versioning and remove all old versions."

That is wrong.

Suspending Versioning only changes how future object writes are handled.

Existing versions remain unless explicitly removed.

---

# Versioning and Storage Cost

Every stored version consumes storage.

Example:

500 MB file

Version 1 → 500 MB

Version 2 → 500 MB

Version 3 → 500 MB

Total storage:

Approximately 1.5 GB

Therefore, Versioning improves recoverability but can increase:

**Storage cost**

This is why it is often paired with:

[[S3 Lifecycle Rules]]

---

# Versioning + Lifecycle Rules

A strong architecture is:

Versioning  
↓  
Protect Against Mistakes  
↓  
Lifecycle Rules  
↓  
Move or Delete Old Versions

Example:

Current Version  
↓  
[[S3 Standard]]

Noncurrent Version  
↓ after 30 days  
[[S3 Standard-IA]]  
↓ later  
[[S3 Glacier Deep Archive]]  
↓ eventually  
Delete

> [!tip] Architecture Pattern
> **Versioning gives recovery**
>
> **Lifecycle controls the cost of that recovery**

---

# Versioning and Replication

[[03-Storage/S3 Replication]] requires:

**Versioning enabled on both source and destination buckets**

This applies to:

- [[S3 Cross-Region Replication]]
- [[S3 Same-Region Replication]]

Architecture:

Source Bucket  
Versioning ✅  
↓ asynchronous replication  
Destination Bucket  
Versioning ✅

### Exam Recognition

If a question asks why S3 replication cannot be configured:

Check:

> **Is Versioning enabled on both buckets?**

---

# Versioning and MFA Delete

[[S3 MFA Delete]] adds additional protection around sensitive versioning operations.

When MFA Delete is enabled, MFA is required to:

- Permanently delete an object version
- Suspend Versioning

MFA is not required simply to:

- Enable Versioning
- List deleted versions

Important:

**Versioning must already be enabled to use MFA Delete.**

---

## MFA Delete Ownership Rule

Only the:

**Bucket owner using the root account**

can enable or disable MFA Delete.

This is intentionally restrictive because MFA Delete protects highly sensitive destructive operations.

---

# Architecture Thinking

## Scenario 1 — Accidental Overwrite

A user uploads a corrupted file using the same S3 key as a valid production object.

The company needs to restore the previous copy.

**Choose → [[S3 Versioning]]**

Why?

The overwrite creates a new version while retaining the old one.

---

## Scenario 2 — Accidental Delete

An administrator accidentally deletes an object.

Versioning is enabled.

What happens?

A:

**Delete Marker**

is created.

Older versions remain available for recovery.

---

## Scenario 3 — Old Versions Cost Too Much

A bucket with Versioning enabled contains years of noncurrent object versions.

Storage costs continue to increase.

**Choose → [[S3 Lifecycle Rules]]**

Configure rules to:

- Transition old versions
- Delete old versions

---

## Scenario 4 — S3 Replication

A company wants objects automatically replicated between two buckets.

One bucket does not have Versioning enabled.

Replication configuration fails.

**Solution → Enable Versioning on both source and destination buckets**

---

## Scenario 5 — Strong Protection Against Permanent Deletes

A company wants to require an additional authentication factor before someone can permanently delete object versions.

**Choose → [[S3 MFA Delete]]**

---

# Versioning vs Replication

Do not confuse these.

## Versioning

Protects copies:

**Inside one bucket**

Example:

Version 1  
Version 2  
Version 3

---

## [[03-Storage/S3 Replication]]

Copies objects:

**To another bucket**

Example:

Bucket A  
↓  
Bucket B

### Memory Trick

**Versioning = History**

**Replication = Another Bucket**

---

# Versioning vs Backup

Versioning provides excellent recovery from:

- Deletes
- Overwrites
- Application mistakes

But do not automatically assume it solves every backup or disaster recovery requirement.

If the architecture requires:

- Separate Region
- Separate account
- Separate bucket
- Geographic resilience

you may also need:

[[03-Storage/S3 Replication]]

or another backup strategy.

---

# Scenario Recognition

## Immediately Think S3 Versioning When You See

- Recover deleted object
- Restore previous version
- Accidental overwrite
- Accidental deletion
- Roll back object
- Version ID
- Delete Marker
- Noncurrent version
- S3 replication prerequisite
- MFA Delete prerequisite

### Strongest Exam Pattern

> **"Recover from accidental overwrite/delete" → Versioning**

---

# Exam Traps

## Trap 1 — Overwriting Deletes the Previous Version

False when Versioning is enabled.

Same key overwrite:

**Creates a new version**

---

## Trap 2 — Normal Delete Permanently Erases Every Version

False.

A normal delete usually creates:

**Delete Marker**

Older versions remain.

---

## Trap 3 — Delete Marker Is the Same as Permanent Deletion

False.

Delete Marker:

**Hides versions**

Deleting a specific Version ID:

**Can permanently remove that version**

---

## Trap 4 — Suspending Versioning Deletes Existing Versions

False.

Existing versions remain.

---

## Trap 5 — Old Objects Automatically Receive New Version IDs When Versioning Is Enabled

False.

Objects that existed before Versioning have:

**Version ID = null**

---

## Trap 6 — Versioning Has No Cost Impact

False.

Every retained version consumes S3 storage.

Combine Versioning with:

[[S3 Lifecycle Rules]]

when cost optimization is important.

---

## Trap 7 — Replication Works Without Versioning

False.

S3 replication requires Versioning on:

**Source + Destination**

---

# Quick Cheat Sheet

| Feature | S3 Versioning |
|---|---|
| Enabled At | Bucket Level |
| Protects Against Overwrites | ✅ |
| Protects Against Deletes | ✅ |
| Same-Key Upload | Creates New Version |
| Restore Previous Version | ✅ |
| Normal Delete | Creates Delete Marker |
| Specific Version Delete | Permanent |
| Pre-Versioning Object | Version ID = null |
| Suspend Deletes Old Versions | ❌ |
| Storage Cost Can Increase | ✅ |
| Lifecycle Integration | ✅ |
| Required for Replication | ✅ |
| Required for MFA Delete | ✅ |

---

## Master Memory Trick

> [!tip] Master Memory Trick
> **S3 Versioning = Ctrl + Z for Objects**
>
> Upload same key?
>
> → **New Version**
>
> Delete object?
>
> → **Delete Marker**
>
> Need old copy?
>
> → **Restore Previous Version**
>
> Suspend Versioning?
>
> → **History stays**
>
> Old versions getting expensive?
>
> → **Lifecycle Rules**

And remember the exam combo:

> **Versioning = Recovery**
>
> **Lifecycle = Cost Control**
>
> **Replication = Another Bucket**
>
> **MFA Delete = Extra Protection**

---

## Related Notes

- [[S3]]
- [[S3 Lifecycle Rules]]
- [[03-Storage/S3 Replication]]
- [[S3 Cross-Region Replication]]
- [[S3 Same-Region Replication]]
- [[S3 MFA Delete]]
- [[S3 Storage Classes]]
- [[S3 Standard]]
- [[S3 Standard-IA]]
- [[S3 Glacier Deep Archive]]