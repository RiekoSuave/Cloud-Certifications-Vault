## What Problem Does It Solve?

[[S3 Object Lock]] protects object versions from being deleted or overwritten for a specified period of time.

It solves the problem of:

> **"How can I make S3 objects immutable so they cannot be changed or deleted?"**

S3 Object Lock uses a:

**WORM model**

WORM means:

**Write Once, Read Many**

Think:

Object Written  
↓  
Locked  
↓  
Can Be Read  
↓  
Cannot Be Deleted or Overwritten During Protection Period

> [!tip] Memory Trick
> **Object Lock = Make S3 Data Untouchable**

---

## Versioning Is Required

[[S3 Object Lock]] requires:

[[S3 Versioning]]

Why?

Object Lock protects:

**Specific object versions**

Architecture:

S3 Bucket  
↓  
Versioning Enabled  
↓  
Object Versions  
↓  
Object Lock Protection

> [!warning] Exam Rule
> **Object Lock → Versioning Required**

---

# WORM — Write Once, Read Many

Object Lock implements:

**Write Once, Read Many**

This means:

Object Version Created  
↓  
Read Many Times ✅  
↓  
Overwrite / Delete Restricted ❌

WORM storage is commonly used for:

- Compliance records
- Financial data
- Legal records
- Audit logs
- Regulatory retention
- Immutable backups

### Memory Trick

**WORM = Write it once, then hands off**

---

# Retention Modes

S3 Object Lock has two major retention modes:

1. **Compliance Mode**
2. **Governance Mode**

These look similar but differ greatly in how difficult they are to bypass.

---

# Compliance Mode

**Compliance Mode** provides the strongest Object Lock protection.

When an object version is protected in Compliance Mode:

- It cannot be overwritten
- It cannot be deleted
- The retention mode cannot be changed
- The retention period cannot be shortened

This applies to:

**Everyone**

including:

**The root user**

> [!warning] Exam Rule
> **Compliance Mode → Even root cannot delete the protected object version**

---

## Compliance Mode Architecture

Object Version  
↓  
Compliance Mode  
↓  
Retention Period  
↓  
Everyone Blocked from Delete / Overwrite  
↓  
Including Root

This is ideal when regulations require:

**True immutable retention**

---

## Can Compliance Retention Be Shortened?

No.

If an object is locked until a specific date:

You cannot reduce that retention period.

Example:

Retention:

7 years

You cannot later change it to:

3 years

while the lock is active.

### Important

The retention period can be:

**Extended**

but not shortened.

### Memory Trick

**Compliance = Commitment**

Once committed:

**You cannot back out early.**

---

# Governance Mode

**Governance Mode** also prevents most users from:

- Deleting object versions
- Overwriting object versions
- Changing retention settings

However:

Certain users with special permissions can bypass the protection.

Architecture:

Normal User  
↓  
Delete Locked Object  
↓  
DENIED

Privileged User  
↓  
Special Permission  
↓  
Can Modify Retention / Delete

> [!tip] Memory Trick
> **Governance = Protected, but administrators can govern it**

---

# Compliance vs Governance

This is one of the most important Object Lock exam comparisons.

## Compliance Mode

Nobody can bypass the lock.

Even:

**Root**

cannot delete the protected version.

Think:

**Absolute protection**

---

## Governance Mode

Most users cannot bypass the lock.

But:

Authorized users with special permissions can.

Think:

**Administrative override exists**

---

## Comparison

| Feature | Compliance | Governance |
|---|---:|---:|
| Prevent Normal User Delete | ✅ | ✅ |
| Prevent Normal User Overwrite | ✅ | ✅ |
| Root Can Bypass | ❌ | Possible with proper permissions |
| Special Admin Can Override | ❌ | ✅ |
| Retention Can Be Shortened | ❌ | Possible with proper permissions |
| Strong Regulatory Lock | ✅ | Less strict |

### Master Difference

> **Compliance = Nobody**
>
> **Governance = Privileged Admin Can**

---

# Retention Period

A:

**Retention Period**

protects an object version for a fixed amount of time.

Example:

Object Created  
↓  
Retention = 5 Years  
↓  
Object Locked  
↓  
5 Years Pass  
↓  
Retention Protection Ends

The retention period can be:

**Extended**

if needed.

---

## Architecture Thinking

Suppose:

Document  
↓  
Retain Until 2033  
↓  
Object Lock

Before 2033:

Delete restricted

After retention expires:

The object is no longer protected by that retention setting.

---

# Legal Hold

[[S3 Object Lock]] also supports:

**Legal Hold**

A Legal Hold protects an object version:

**Indefinitely**

Unlike a retention period:

It does not depend on a specific expiration date.

Think:

Object  
↓  
Legal Hold ON  
↓  
Protected Indefinitely  
↓  
Legal Hold Removed  
↓  
Normal retention rules apply

> [!tip] Memory Trick
> **Retention = Until a date**
>
> **Legal Hold = Until someone removes the hold**

---

## Legal Hold Is Independent of Retention Period

A Legal Hold operates independently from:

**Retention Period**

Example:

Object Retention Ends  
↓  
But Legal Hold Still ON  
↓  
Object Remains Protected

Or:

No retention period  
+  
Legal Hold ON  
↓  
Object Protected

---

## Adding and Removing Legal Holds

Legal Holds can be placed or removed using the appropriate IAM permission:

`s3:PutObjectLegalHold`

This differs from Compliance Mode because Legal Hold itself can be removed by an authorized principal.

### Memory Trick

**Legal Hold = Switch**

ON → Protected

OFF → Hold removed

---

# Retention Period vs Legal Hold

## Retention Period

Protection lasts until:

**A defined date / duration**

Example:

7 years

---

## Legal Hold

Protection lasts:

**Indefinitely until explicitly removed**

### Exam Decision

**"Keep for X years" → Retention Period**

**"Keep until legal case is resolved" → Legal Hold**

---

# Architecture Thinking

## Scenario 1 — Regulatory Seven-Year Retention

A financial company must retain transaction records for seven years.

Nobody, including the root user, may delete the records during that period.

**Choose → S3 Object Lock in Compliance Mode**

Why?

Compliance Mode cannot be bypassed.

---

## Scenario 2 — Protect Backups but Allow Security Admin Override

A company wants backups protected against accidental deletion.

However, a small group of administrators must be able to remove the protection if necessary.

**Choose → Governance Mode**

---

## Scenario 3 — Ongoing Legal Investigation

A company must preserve certain files until a lawsuit is resolved.

The end date is unknown.

**Choose → Legal Hold**

Why?

Legal Hold protects the object:

**Indefinitely**

until explicitly removed.

---

## Scenario 4 — Root User Must Not Delete Records

A compliance requirement states that not even the AWS root account should be able to delete retained records.

**Choose → Compliance Mode**

This is one of the strongest exam giveaways.

---

## Scenario 5 — Fixed Retention Period

A company must retain audit records for:

**5 years**

After that, deletion is allowed.

**Choose → Object Lock Retention Period**

---

# Object Lock vs MFA Delete

These are easy to confuse.

## [[S3 MFA Delete]]

Requires:

**MFA before certain destructive operations**

But deletion can still occur with proper credentials and MFA.

---

## Object Lock

Can make object versions:

**Impossible to delete during the retention period**

especially in Compliance Mode.

### Memory Trick

**MFA Delete = Prove who you are before deleting**

**Object Lock = You cannot delete yet**

---

# Object Lock vs Versioning

## [[S3 Versioning]]

Creates:

**Previous object versions**

This helps recover from deletes or overwrites.

---

## Object Lock

Protects:

**Specific versions from being deleted or overwritten**

### Architecture Pattern

Versioning  
↓  
Creates History

Object Lock  
↓  
Makes History Immutable

---

# Object Lock vs Lifecycle Rules

[[S3 Lifecycle Rules]] can:

- Transition objects
- Delete objects
- Expire old versions

But lifecycle expiration cannot violate an active Object Lock.

Think:

Lifecycle Rule  
↓  
Delete Object  
↓  
Object Lock Active  
↓  
Deletion Blocked

### Architecture Thinking

**Lifecycle = What should happen eventually**

**Object Lock = What is allowed right now**

---

# Object Lock vs Glacier Vault Lock

These are related concepts but apply to different storage models.

## S3 Object Lock

Applies to:

**S3 object versions**

Supports:

- Compliance
- Governance
- Retention periods
- Legal Holds

---

## Glacier Vault Lock

Historically applies retention controls to Glacier vaults.

For modern S3 scenarios, the exam is more likely to emphasize:

**S3 Object Lock + WORM**

### Memory Trick

**Object Lock = Object Versions**

**Vault Lock = Glacier Vault Policy**

---

# Defense in Depth

A highly protected S3 architecture might use:

[[S3 Versioning]]  
+  
[[S3 Object Lock]]  
+  
[[S3 MFA Delete]]  
+  
[[S3 Encryption]]  
+  
[[S3 Block Public Access]]

Each protects against a different threat.

### Versioning

Recover old copies

### Object Lock

Prevent modification/deletion

### MFA Delete

Require MFA for destructive versioning operations

### Encryption

Protect confidentiality

### Block Public Access

Prevent public exposure

---

# Scenario Recognition

## Immediately Think Object Lock When You See

- WORM
- Immutable data
- Cannot delete for X years
- Compliance retention
- Regulatory records
- Root must not delete
- Governance Mode
- Compliance Mode
- Legal Hold
- Retention period
- Write Once Read Many

### Strongest Exam Phrases

> **"Cannot be deleted even by root"**
>
> → **Compliance Mode**

> **"Admins may override"**
>
> → **Governance Mode**

> **"Unknown retention end date"**
>
> → **Legal Hold**

---

# Exam Traps

## Trap 1 — Object Lock Works Without Versioning

False.

[[S3 Versioning]] must be enabled.

---

## Trap 2 — Root Can Delete Compliance Mode Objects

False.

Compliance Mode applies even to:

**Root**

---

## Trap 3 — Compliance Retention Can Be Shortened

False.

It can be extended, but:

**Not shortened**

---

## Trap 4 — Governance Mode Cannot Be Bypassed

False.

Users with special permissions can alter or bypass governance retention.

---

## Trap 5 — Legal Hold Requires a Fixed End Date

False.

Legal Hold protects:

**Indefinitely until removed**

---

## Trap 6 — Legal Hold and Retention Period Are the Same

False.

Retention Period:

**Time based**

Legal Hold:

**Indefinite / manually removed**

---

## Trap 7 — MFA Delete and Object Lock Are Equivalent

False.

MFA Delete adds:

**Authentication**

Object Lock adds:

**Immutability**

---

# Quick Cheat Sheet

| Requirement | Best Choice |
|---|---|
| WORM storage | S3 Object Lock |
| Versioning required | ✅ |
| Nobody can delete, including root | Compliance Mode |
| Admin override allowed | Governance Mode |
| Protect for fixed period | Retention Period |
| Protect indefinitely | Legal Hold |
| Retention can be extended | ✅ |
| Compliance retention shortened | ❌ |
| Require MFA before delete | MFA Delete |
| Immutable regulatory records | Compliance Mode |

---

## Master Memory Trick

> [!tip] Master Memory Trick
> **Object Lock = S3 Time Vault**
>
> Ask:
>
> **"How hard should it be to remove the object?"**
>
> **Nobody, even root**
>
> → **Compliance**
>
> **Admins can override**
>
> → **Governance**
>
> **Protect until a date**
>
> → **Retention Period**
>
> **Protect until someone removes the hold**
>
> → **Legal Hold**

And remember:

> **Versioning creates the version**
>
> **Object Lock makes the version immutable**

The ultimate exam giveaway:

> **WORM = S3 Object Lock**

---

## Related Notes

- [[S3]]
- [[S3 Versioning]]
- [[S3 MFA Delete]]
- [[S3 Lifecycle Rules]]
- [[S3 Encryption]]
- [[S3 Block Public Access]]
- [[S3 Glacier]]
- [[S3 Glacier Vault Lock]]
- [[IAM]]