## What Problem Does It Solve?

[[S3 Lifecycle Rules]] automate what happens to S3 objects as they age.

They solve questions such as:

> **"How can I automatically move old objects to cheaper storage?"**

and:

> **"How can I automatically delete objects when they are no longer needed?"**

Think:

New Object  
↓  
Frequently Accessed  
↓  
Older Object  
↓  
Cheaper Storage  
↓  
Archive  
↓  
Delete

> [!tip] Memory Trick
> **Lifecycle = Age-Based Automation**
>
> As objects get older:
>
> **Move them, archive them, or delete them.**

---

## Two Main Lifecycle Actions

There are two major lifecycle action categories:

1. **Transition Actions**
2. **Expiration Actions**

These solve different problems.

---

# Transition Actions

Transition Actions automatically move objects from one:

**S3 Storage Class → Another Storage Class**

Example:

[[S3 Standard]]  
↓ after 60 days  
[[S3 Standard-IA]]  
↓ after 6 months  
[[S3 Glacier Flexible Retrieval]]

This lets you reduce storage costs as objects become less frequently accessed.

---

## Transition Example

A company stores application logs.

Access pattern:

First 30 days:

Frequently accessed

After 30 days:

Rarely accessed

After 180 days:

Almost never accessed

Possible lifecycle:

[[S3 Standard]]  
↓ 30 days  
[[S3 Standard-IA]]  
↓ 180 days  
[[S3 Glacier Flexible Retrieval]]

The lifecycle rule handles the transition automatically.

> [!tip] Architecture Thinking
> **Known access pattern over time → Lifecycle Rule**

---

# Expiration Actions

Expiration Actions automatically:

**Delete objects after a configured period**

Example:

Access Logs  
↓  
Keep 365 Days  
↓  
Delete Automatically

This is useful when data has:

- Retention requirements
- Limited business value after a period
- Compliance-defined deletion dates
- Temporary processing requirements

---

## Expiration Example

A company stores web access logs.

Requirement:

Keep logs for:

**365 days**

Afterward:

They have no business value.

Configure:

Object Created  
↓  
365 Days  
↓  
Lifecycle Expiration  
↓  
Deleted

---

# Lifecycle Rules and Versioning

Lifecycle Rules work with:

[[03-Storage/S3 Versioning]]

This becomes extremely important when a bucket contains multiple versions of the same object.

You can configure lifecycle actions for:

- Current object versions
- Noncurrent object versions

---

## Current vs Noncurrent Versions

Suppose versioning is enabled.

Object:

report.pdf

Versions:

Version 1  
Version 2  
Version 3

Version 3 is:

**Current**

Versions 1 and 2 are:

**Noncurrent**

Lifecycle Rules can target the older noncurrent versions separately.

Example:

Current Version  
↓  
Keep in Standard

Noncurrent Version  
↓ after 30 days  
Standard-IA  
↓ later  
Glacier Deep Archive

---

## Deleting Old Object Versions

Lifecycle Rules can automatically remove:

**Old versions of objects**

This prevents a versioned bucket from accumulating unnecessary storage indefinitely.

Example:

Object Updated Many Times  
↓  
Old Versions Accumulate  
↓  
Lifecycle Rule  
↓  
Delete Old Noncurrent Versions

### Architecture Thinking

Versioning improves recoverability.

But without lifecycle management:

**Old versions can increase storage cost.**

---

# Incomplete Multipart Uploads

Lifecycle Rules can also delete:

**Incomplete Multipart Uploads**

This is a useful cost-control feature.

Suppose:

Large File Upload Begins  
↓  
Several Parts Uploaded  
↓  
Upload Never Completes

Those uploaded parts can remain in S3 and consume storage.

Lifecycle rule:

Incomplete Multipart Upload  
↓ after configured time  
Delete Parts

> [!tip] Memory Trick
> **Started but never finished upload → Lifecycle cleanup**

---

# Filtering Lifecycle Rules

Lifecycle Rules do not have to affect every object in a bucket.

You can target objects using:

- Prefix
- Object Tags

---

## Prefix Filtering

Example bucket:

mybucket

Objects:

logs/2026/file1.log

logs/2026/file2.log

images/photo1.jpg

A Lifecycle Rule can target:

logs/*

without affecting:

images/*

Conceptually:

Bucket  
├── logs/ → Lifecycle Rule
└── images/ → No Rule

---

## Tag Filtering

Lifecycle Rules can also target objects based on:

**Object Tags**

Example tag:

Department = Finance

Then:

Finance Objects  
↓  
Lifecycle Rule  
↓  
Archive after configured period

Other departments:

Unaffected

### Architecture Thinking

Use tags when lifecycle behavior depends on:

- Department
- Data classification
- Project
- Environment
- Compliance category

---

# Architecture Thinking — Scenario 1

This is directly modeled after the Maarek SAA scenario.

An application stores:

- Original profile photos
- Generated thumbnails

Requirements:

### Original Photos

- Must be immediately available for 60 days
- After 60 days, users can wait several hours

### Thumbnails

- Can easily be recreated
- Needed for only 60 days

Architecture:

Original Photo  
↓  
[[S3 Standard]]  
↓ after 60 days  
Glacier Storage

Thumbnail  
↓  
[[S3 One Zone-IA]]  
↓ after 60 days  
Delete

### Why?

Originals:

Need fast initial access but become archival.

Thumbnails:

Re-creatable + short-lived.

> [!tip] Architecture Pattern
> **Critical original → retain/archive**
>
> **Re-creatable derivative → cheaper storage + expire**

---

# Architecture Thinking — Scenario 2

Another important Maarek scenario:

A company requires deleted S3 objects to be:

- Immediately recoverable for 30 days
- Recoverable within 48 hours afterward
- Retained for up to 365 days

### Step 1

Enable:

[[03-Storage/S3 Versioning]]

Why?

Deleting a versioned object creates a:

**Delete Marker**

The previous object version still exists.

---

### Step 2

Transition noncurrent versions to:

[[S3 Standard-IA]]

for immediate recovery during the early period.

---

### Step 3

Later transition noncurrent versions to:

[[S3 Glacier Deep Archive]]

for cheap long-term retention.

Architecture:

Current Object  
↓ deleted  
Delete Marker  
↓  
Previous Version becomes Noncurrent  
↓  
Standard-IA  
↓ later  
Glacier Deep Archive

### Architecture Lesson

> **Versioning provides recovery**
>
> **Lifecycle controls recovery cost over time**

---

# Lifecycle Rules vs Intelligent-Tiering

These both help optimize S3 storage cost, but they solve different problems.

## Lifecycle Rules

Best when:

**You know how access changes over time**

Example:

After 30 days → IA

After 180 days → Glacier

---

## [[S3 Intelligent-Tiering]]

Best when:

**You do NOT know the access pattern**

AWS automatically monitors access and adjusts tiers.

### Exam Decision

> **Known age-based pattern → Lifecycle**
>
> **Unknown/unpredictable access → Intelligent-Tiering**

---

# Lifecycle Rules vs Manual Transitions

You can manually move objects between storage classes.

But that creates operational overhead.

If the behavior is predictable:

> **Automate it with Lifecycle Rules**

Example:

Every object older than 90 days  
↓  
Archive automatically

This is generally more operationally efficient than repeatedly moving objects manually.

---

# S3 Analytics — Storage Class Analysis

[[S3 Analytics]] can help determine when objects should transition between storage classes.

It analyzes access patterns and provides recommendations for:

- [[S3 Standard]]
- [[S3 Standard-IA]]

Important limitations:

It does **not** provide transition recommendations for:

- [[S3 One Zone-IA]]
- Glacier storage classes

---

## S3 Analytics Behavior

The report:

- Updates daily
- Can take 24–48 hours before analysis starts appearing
- Can help design or improve Lifecycle Rules

Think:

S3 Objects  
↓  
[[S3 Analytics]]  
↓  
Analyze Access Patterns  
↓  
Storage Class Recommendation  
↓  
Build Lifecycle Rule

> [!tip] Memory Trick
> **Analytics tells you WHEN**
>
> **Lifecycle performs the MOVE**

---

# Transition Strategy

A common lifecycle progression looks like:

[[S3 Standard]]  
↓  
[[S3 Standard-IA]]  
↓  
[[S3 Glacier Instant Retrieval]]  
↓  
[[S3 Glacier Flexible Retrieval]]  
↓  
[[S3 Glacier Deep Archive]]

But the correct path depends on:

- Access frequency
- Retrieval requirements
- Minimum storage duration
- Cost requirements

Do not assume every object should pass through every class.

---

# Architecture Thinking

## Scenario 1 — Logs Retained for One Year

Application logs are frequently analyzed for 30 days.

Afterward, they are rarely used.

They must be deleted after one year.

Possible architecture:

[[S3 Standard]]  
↓ 30 days  
[[S3 Standard-IA]]  
↓ later  
Glacier  
↓ 365 days  
Expiration

**Choose → S3 Lifecycle Rule**

---

## Scenario 2 — Temporary Thumbnails

Image thumbnails can be recreated.

They are needed for only 60 days.

**Choose:**

[[S3 One Zone-IA]]

+

Lifecycle Expiration after 60 days

---

## Scenario 3 — Old Object Versions

A versioned bucket contains thousands of old object versions that are increasing storage costs.

The company wants old versions automatically removed.

**Choose → Lifecycle Expiration for Noncurrent Versions**

---

## Scenario 4 — Abandoned Multipart Uploads

Users upload very large files.

Many uploads are started but never completed.

Storage costs are increasing.

**Choose → Lifecycle Rule to Abort Incomplete Multipart Uploads**

---

## Scenario 5 — Unknown Access Patterns

A company does not know which objects will remain frequently accessed.

**Do NOT choose fixed age-based transitions automatically.**

Consider:

[[S3 Intelligent-Tiering]]

---

# Scenario Recognition

## Immediately Think Lifecycle Rules When You See

- After X days
- Automatically transition
- Automatically archive
- Automatically delete
- Old object versions
- Noncurrent versions
- Retention period
- Expire logs
- Abort incomplete multipart uploads
- Known access pattern over time
- Move Standard → IA → Glacier

### Strongest Exam Pattern

> **"After N days..." → Lifecycle Rule**

---

# Exam Traps

## Trap 1 — Lifecycle Rules Only Delete Objects

False.

Lifecycle Rules can:

- Transition objects
- Expire objects
- Delete old versions
- Abort incomplete multipart uploads

---

## Trap 2 — Deleted Versioned Object Is Immediately Gone

Not necessarily.

With [[03-Storage/S3 Versioning]], deleting an object normally creates a:

**Delete Marker**

Older versions remain available.

---

## Trap 3 — Lifecycle Rules Must Apply to the Entire Bucket

False.

Rules can target:

- Prefixes
- Object Tags

---

## Trap 4 — Lifecycle and Intelligent-Tiering Are the Same

False.

**Lifecycle = Predefined age-based automation**

**Intelligent-Tiering = Access-pattern-based automatic optimization**

---

## Trap 5 — Lifecycle Ignores Noncurrent Versions

False.

Lifecycle Rules can specifically manage:

**Noncurrent versions**

---

## Trap 6 — Incomplete Multipart Uploads Automatically Disappear Immediately

Not necessarily.

Use Lifecycle Rules to automatically abort and remove incomplete multipart uploads.

---

## Trap 7 — S3 Analytics Automatically Moves Objects

No.

S3 Analytics:

**Analyzes and recommends**

Lifecycle Rules:

**Perform transitions**

---

# Quick Cheat Sheet

| Requirement | Lifecycle Capability |
|---|---|
| Move object to cheaper class | Transition Action |
| Delete object after time | Expiration Action |
| Delete old versions | Noncurrent Version Expiration |
| Archive old versions | Noncurrent Version Transition |
| Delete incomplete uploads | Abort Multipart Upload |
| Target folder-like path | Prefix |
| Target business category | Object Tag |
| Known access pattern | Lifecycle |
| Unknown access pattern | Intelligent-Tiering |
| Analyze Standard → Standard-IA | S3 Analytics |

---

## Master Memory Trick

> [!tip] Master Memory Trick
> **Lifecycle = What should happen when the object gets OLD?**

Ask:

**Still useful but less accessed?**

→ **Transition**

**No longer useful?**

→ **Expire**

**Old version?**

→ **Archive or delete**

**Incomplete upload?**

→ **Abort it**

And remember:

> **Known timeline → Lifecycle**
>
> **Unknown access → Intelligent-Tiering**

---

## Related Notes

- [[S3]]
- [[S3 Storage Classes]]
- [[S3 Standard]]
- [[S3 Standard-IA]]
- [[S3 One Zone-IA]]
- [[S3 Intelligent-Tiering]]
- [[S3 Glacier Instant Retrieval]]
- [[S3 Glacier Flexible Retrieval]]
- [[S3 Glacier Deep Archive]]
- [[03-Storage/S3 Versioning]]
- [[S3 Analytics]]
- [[S3 Multipart Upload]]