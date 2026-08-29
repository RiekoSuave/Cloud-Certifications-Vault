## What Problem Does It Solve?

[[S3 Glacier Vault Lock]] enforces immutable retention rules on data stored in a Glacier vault.

It solves the problem of:

> **"How can I make archived data impossible to delete or alter in violation of a retention policy?"**

Glacier Vault Lock uses a:

**WORM model**

WORM means:

**Write Once, Read Many**

Think:

Archive Data  
↓  
Vault Lock Policy  
↓  
Policy Locked  
↓  
Data Retention Enforced

> [!tip] Memory Trick
> **Vault Lock = Lock the RULES around the archive**

---

## WORM — Write Once, Read Many

Glacier Vault Lock supports:

**Write Once, Read Many**

This is useful when data must remain immutable for:

- Compliance
- Regulatory retention
- Legal requirements
- Long-term archival
- Records preservation

Conceptually:

Object Written  
↓  
Retention Policy Applied  
↓  
Read Allowed  
↓  
Deletion Restricted

---

# Core Architecture

The basic pattern is:

Glacier Vault  
↓  
Create Vault Lock Policy  
↓  
Review Policy  
↓  
Lock Policy  
↓  
Policy Becomes Immutable

After the Vault Lock Policy is locked:

It can no longer be:

- Changed
- Deleted

> [!warning] Exam Rule
> **Locked Vault Lock Policy = Cannot be modified or deleted**

---

# Vault Lock Policy

The Vault Lock Policy defines the retention controls that must be enforced.

Example concept:

Archive  
↓  
Retention Requirement  
↓  
Vault Lock Policy  
↓  
Delete Blocked Until Requirement Is Met

The policy can enforce rules such as:

- Minimum retention period
- Restrictions on deletion
- Compliance controls

---

# The Critical Difference — Locking the Policy

This is the most important idea.

A normal policy can potentially be changed.

A locked Vault Lock Policy cannot.

Think:

Create Policy  
↓  
Test / Review  
↓  
LOCK IT  
↓  
Policy Frozen

### Memory Trick

> **Object Lock locks OBJECTS**
>
> **Vault Lock locks the POLICY**

---

# Compliance Use Case

Glacier Vault Lock is particularly useful when regulatory requirements state:

> **"Archived records must not be deleted before the required retention period expires."**

Example:

Financial Records  
↓  
Glacier Vault  
↓  
Vault Lock Policy  
↓  
7-Year Retention  
↓  
Early Delete Blocked

This provides enforceable data-retention controls.

---

# Architecture Thinking

Suppose a financial institution archives regulatory documents.

Requirement:

- Keep records for 7 years
- Prevent premature deletion
- Prevent administrators from changing the retention policy after it is locked

**Choose → S3 Glacier Vault Lock**

Architecture:

Compliance Archive  
↓  
Glacier Vault  
↓  
Vault Lock Policy  
↓  
Policy Locked  
↓  
Retention Enforced

---

# Vault Lock vs Object Lock

These are closely related and easy to confuse.

Both support:

**WORM**

But they operate differently.

---

## [[S3 Object Lock]]

Protects:

**Individual S3 object versions**

Requires:

[[S3 Versioning]]

Supports:

- Compliance Mode
- Governance Mode
- Retention Periods
- Legal Holds

Think:

**Protect this object version**

---

## Glacier Vault Lock

Protects:

**The retention policy governing a Glacier vault**

The important concept is:

**The policy itself becomes immutable**

Think:

**Protect the archive rules**

---

# Object Lock vs Vault Lock

| Feature | Object Lock | Glacier Vault Lock |
|---|---|---|
| WORM | ✅ | ✅ |
| Protects S3 Object Versions | ✅ | ❌ |
| Protects Vault Policy | ❌ | ✅ |
| Versioning Required | ✅ | Not the core concept |
| Compliance / Governance Modes | ✅ | ❌ |
| Legal Hold | ✅ | ❌ |
| Policy Cannot Be Changed After Lock | Not the primary mechanism | ✅ |
| Compliance Retention | ✅ | ✅ |

### Memory Trick

**Object Lock = Lock the FILE**

**Vault Lock = Lock the RULEBOOK**

---

# Vault Lock vs MFA Delete

## [[S3 MFA Delete]]

Requires:

**MFA before certain destructive operations**

The operation can still happen if proper authentication is supplied.

---

## Glacier Vault Lock

Enforces:

**Retention policy restrictions**

The goal is not merely:

> "Prove who you are"

The goal is:

> **"The retention rules cannot be bypassed by editing the policy after it is locked."**

### Exam Decision

**Require MFA before delete**
→ MFA Delete

**Enforce immutable archive-retention policy**
→ Glacier Vault Lock

---

# Vault Lock vs Lifecycle Rules

## [[S3 Lifecycle Rules]]

Automate:

- Transitions
- Expiration
- Archival

Example:

After 180 days  
↓  
Move to Glacier

---

## Glacier Vault Lock

Enforces:

**Retention and immutability requirements**

### Memory Trick

**Lifecycle = Move/Delete when scheduled**

**Vault Lock = Prevent illegal deletion**

---

# Vault Lock vs Glacier Storage Classes

Do not confuse:

**Glacier storage class**

with:

**Glacier Vault Lock**

A Glacier storage class answers:

> **"How cheaply can I archive this data?"**

Vault Lock answers:

> **"How do I enforce immutable retention rules?"**

Storage Class  
↓  
Cost / Retrieval Characteristics

Vault Lock  
↓  
Compliance / Retention Controls

---

# Architecture Thinking

## Scenario 1 — Regulatory Archive

A company must retain archived financial data according to a mandatory retention policy.

The policy itself must not be changed after approval.

**Choose → Glacier Vault Lock**

---

## Scenario 2 — WORM Archive

A compliance question explicitly requires:

**Write Once, Read Many**

for archived data.

**Think → Glacier Vault Lock or S3 Object Lock**

Then determine what is being protected.

If:

**Object versions**
→ [[S3 Object Lock]]

If:

**Glacier vault policy**
→ Glacier Vault Lock

---

## Scenario 3 — Prevent Root From Deleting S3 Object Version

The requirement applies to an individual S3 object version and even root cannot delete it during retention.

**Do NOT choose → Glacier Vault Lock**

Choose:

[[S3 Object Lock]] in Compliance Mode

---

## Scenario 4 — Archive Policy Must Never Be Edited Again

A vault retention policy has been reviewed and approved.

After activation, the company requires that nobody can modify or delete the policy.

**Choose → Glacier Vault Lock**

---

# Scenario Recognition

## Immediately Think Glacier Vault Lock When You See

- Glacier vault
- WORM
- Archive compliance
- Data retention
- Vault Lock Policy
- Policy cannot be changed
- Policy cannot be deleted
- Immutable retention rules
- Regulatory archive

### Strongest Exam Pattern

> **"Lock the retention policy so it can never be edited"**
>
> → **Glacier Vault Lock**

---

# Exam Traps

## Trap 1 — Vault Lock and Object Lock Are the Same

False.

Both support WORM, but:

**Object Lock protects object versions**

**Vault Lock protects vault retention policy**

---

## Trap 2 — Vault Lock Policy Can Be Edited After It Is Locked

False.

Once locked:

**It cannot be changed or deleted**

---

## Trap 3 — Vault Lock Is Just an Encryption Feature

False.

Vault Lock is about:

**Retention + Compliance + Immutability**

Encryption is handled separately.

---

## Trap 4 — Vault Lock Automatically Moves Objects into Glacier

False.

That is a storage-management question.

Use:

[[S3 Lifecycle Rules]]

for transitions.

Vault Lock controls:

**Retention policy**

---

## Trap 5 — WORM Always Means Object Lock

Not necessarily.

Both:

- [[S3 Object Lock]]
- Glacier Vault Lock

support WORM-style protection.

Read whether the question emphasizes:

**Object version**

or:

**Vault policy**

---

# Quick Cheat Sheet

| Requirement | Glacier Vault Lock |
|---|---|
| WORM | ✅ |
| Compliance Archive | ✅ |
| Data Retention | ✅ |
| Vault Lock Policy | ✅ |
| Policy Locked Against Changes | ✅ |
| Policy Can Be Deleted After Lock | ❌ |
| Protect Individual S3 Version | Use Object Lock |
| Legal Hold | Use Object Lock |
| Compliance/Governance Modes | Use Object Lock |
| Move Data to Glacier Automatically | Use Lifecycle Rules |

---

## Master Memory Trick

> [!tip] Master Memory Trick
> **Vault Lock = Lock the RULEBOOK**
>
> First:
>
> **Create the retention policy**
>
> Then:
>
> **Lock the policy**
>
> After that:
>
> **No edits**
>
> **No deletion**

Remember:

**Object Lock**
→ Protects the **OBJECT**

**Vault Lock**
→ Protects the **VAULT POLICY**

And both scream:

> **WORM + COMPLIANCE**

---

## Related Notes

- [[S3]]
- [[S3 Object Lock]]
- [[S3 MFA Delete]]
- [[S3 Lifecycle Rules]]
- [[S3 Glacier Flexible Retrieval]]
- [[S3 Glacier Deep Archive]]
- [[S3 Versioning]]
- [[Compliance]]