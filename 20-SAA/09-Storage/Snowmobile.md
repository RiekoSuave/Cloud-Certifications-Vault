## What Problem Does It Solve?

[[Snowmobile]] is designed for:

**Extremely large-scale offline data migration**

It solves the problem of:

> **"How can an organization migrate an enormous amount of data—potentially an entire data center—to AWS when network transfer or smaller Snow devices are impractical?"**

Architecture:

Data Center  
↓  
AWS Snowmobile  
↓  
Physical Transportation  
↓  
AWS  
↓  
Cloud Storage

> [!tip] Memory Trick
> **Snowmobile = Data-center-sized migration**

---

# What Is Snowmobile?

Snowmobile is historically part of the:

[[Snow Family]]

It is a:

**Truck-scale secure data-transfer solution**

designed for extremely large migrations.

Instead of shipping individual portable devices:

Data Center  
↓  
Snowmobile  
↓  
AWS

Think:

**Massive physical data migration**

---

# Classic Capacity

Classic AWS course material describes each Snowmobile as capable of transferring up to approximately:

**100 PB**

of data.

That is:

**100 Petabytes**

### Memory Trick

> **Snowball → Terabytes**
>
> **Snowmobile → Petabytes**

For the exam, the architectural scale matters more than memorizing every hardware specification.

---

# When Would You Use Snowmobile?

Think:

- Entire data-center migration
- Tens of petabytes
- Extremely large datasets
- Network transfer would take far too long
- Large-scale physical migration

### Strong Exam Pattern

> **"A company needs to migrate tens of petabytes from its data center to AWS."**
>
> → **Snowmobile**

---

# Physical Data Transfer

Snowmobile avoids sending the entire dataset through:

**The Internet**

Instead:

Data  
↓  
Loaded onto Snowmobile  
↓  
Physically transported  
↓  
AWS

This can dramatically reduce migration time when compared with:

**Very large network transfers**

---

# Why Not Use the Network?

Imagine a company needs to migrate:

**50 PB**

Even with substantial bandwidth, moving that amount of data across a network can take:

**A very long time**

and consume:

**Enormous network capacity**

Snowmobile allows the organization to:

**Physically transport the dataset**

---

# Secure Migration

Because Snowmobile physically transports:

**Extremely valuable enterprise data**

security is a major design consideration.

Classic Snowmobile security concepts include:

- Encryption
- Physical security
- Tracking
- Monitoring
- Secure chain of custody

### Exam Thinking

Do not think:

> **Truck full of unencrypted hard drives**

Think:

> **Highly secured AWS data-transfer system**

---

# Encryption

Data transferred using Snowmobile is:

**Encrypted**

This helps protect the dataset during:

- Loading
- Storage
- Transportation
- Migration

AWS encryption services such as:

[[06-Security/KMS]]

are relevant to Snow Family security concepts.

---

# Snowmobile vs Snowball Edge

This is the biggest comparison.

## [[Snowball Edge]]

Think:

- Large migration
- Individual portable/rugged devices
- TB-scale datasets
- Edge computing

---

## Snowmobile

Think:

- Massive migration
- Truck-scale system
- Tens of PB
- Entire data center

### Memory Trick

**SnowBALL**
→ Carry / ship devices

**SnowMOBILE**
→ The truck itself

---

# Snowmobile vs Snowcone

## [[Snowcone]]

Think:

- Small
- Portable
- Remote
- Edge computing
- Smaller datasets

---

## Snowmobile

Think:

- Massive
- Data-center migration
- Petabyte scale

### Scale Memory Trick

**Snowcone**
↓  
Small

**Snowball Edge**
↓  
Large

**Snowmobile**
↓  
Massive

---

# Snowmobile vs DataSync

## [[DataSync]]

Uses:

**Network transfer**

Best when:

- Bandwidth is sufficient
- Online migration is practical
- Recurring synchronization is needed

---

## Snowmobile

Uses:

**Physical transportation**

Best for:

**Extremely large one-time migrations**

### Memory Trick

**DataSync = Send it**

**Snowmobile = Drive it**

---

# Snowmobile vs Direct Connect

## [[05-Networking/Direct Connect]]

Provides:

**Dedicated network connectivity**

Best when an organization needs:

**Ongoing connectivity**

---

## Snowmobile

Provides:

**Physical offline migration**

Best when an organization needs:

**Massive one-time data movement**

### Exam Decision

Long-term hybrid network  
→ Direct Connect

Massive one-time migration  
→ Snowmobile

---

# Snowmobile vs Storage Gateway

## [[Storage Gateway]]

Provides:

**Ongoing hybrid storage access**

---

## Snowmobile

Provides:

**Massive physical migration**

### Memory Trick

**Gateway = Keep using both environments**

**Snowmobile = Move the mountain**

---

# Snowmobile vs S3 Transfer Acceleration

## [[S3 Transfer Acceleration]]

Improves:

**Network-based uploads to S3**

---

## Snowmobile

Avoids the network bottleneck by:

**Physically transporting the dataset**

### Exam Decision

Global application uploads  
→ S3 Transfer Acceleration

50 PB data-center migration  
→ Snowmobile

---

# When Snowball Edge May Be Better

Do not automatically choose Snowmobile for every:

**Large migration**

Example:

200 TB

This is large, but it is nowhere near:

**Tens of petabytes**

Multiple:

[[Snowball Edge Storage Optimized]]

devices may be more appropriate.

### Exam Thinking

Ask:

> **How big is BIG?**

Hundreds of TB  
→ Snowball Edge

Tens of PB  
→ Classic Snowmobile territory

---

# Migration Decision Scale

Conceptually:

Small / Portable  
↓  
[[Snowcone]]

Large  
↓  
[[Snowball Edge Storage Optimized]]

Extremely Massive  
↓  
Snowmobile

---

# Architecture Thinking

## Scenario 1 — 50 PB Migration

A large enterprise needs to migrate:

**50 PB**

from its existing data center into AWS.

Network transfer cannot meet the migration deadline.

**Choose → Snowmobile**

---

## Scenario 2 — Entire Data Center

A company is closing a major data center.

It needs to migrate an enormous amount of stored data into AWS.

The dataset is:

**Tens of petabytes**

**Choose → Snowmobile**

---

## Scenario 3 — 200 TB Migration

A company needs to migrate:

**200 TB**

with poor network bandwidth.

Snowmobile would likely be excessive.

Think:

[[Snowball Edge Storage Optimized]]

---

## Scenario 4 — Nightly Synchronization

A company needs to synchronize changed files:

**Every night**

Do NOT choose Snowmobile.

Choose:

[[DataSync]]

---

## Scenario 5 — Ongoing Hybrid Storage

An on-premises application needs continuous access to AWS-backed storage.

Do NOT choose Snowmobile.

Choose:

[[Storage Gateway]]

---

## Scenario 6 — Remote Edge Compute

A remote factory needs substantial local processing.

Do NOT choose Snowmobile.

Choose:

[[Snowball Edge Compute Optimized]]

---

# Scenario Recognition

Immediately associate classic Snowmobile material with:

- 100 PB per Snowmobile
- Tens of petabytes
- Exabyte-scale migration
- Entire data-center migration
- Truck-scale data transfer
- Massive offline migration

### Strongest Classic Exam Pattern

> **"Migrate tens of petabytes from a data center to AWS without relying on network transfer."**
>
> → **Snowmobile**

---

# Important Current-Service Note

> [!warning] Current AWS Context
> Snowmobile is important to recognize because it appears in older AWS training material and comparison questions.
>
> AWS stopped accepting new Snowmobile customers in **March 2024**.
>
> For current AWS architectures, do not assume Snowmobile is available for a new deployment simply because older course material lists it.
>
> For the SAA exam, understand the **classic Snowmobile concept**, but prioritize the requirements and current AWS service options presented in the question.

---

# Exam Traps

## Trap 1 — Snowmobile Is the Best Choice for 50 TB

False.

That scale does not justify a truck-scale solution.

Think about:

- DataSync
- Snowball Edge

depending on network conditions.

---

## Trap 2 — Snowmobile Provides Edge Computing Like Snowball Edge

Do not treat them as equivalent.

Snowball Edge is strongly associated with:

**Edge computing**

Snowmobile's classic purpose is:

**Massive data migration**

---

## Trap 3 — Snowmobile Provides Ongoing Hybrid Storage

False.

Think:

[[Storage Gateway]]

---

## Trap 4 — Snowmobile Is for Recurring Data Synchronization

False.

Think:

[[DataSync]]

---

## Trap 5 — Snowmobile Is a Dedicated Network Connection

False.

That is:

[[05-Networking/Direct Connect]]

Snowmobile is:

**Physical data transportation**

---

## Trap 6 — Snowmobile Is Currently a Normal New-Customer AWS Offering

No.

AWS stopped accepting:

**New Snowmobile customers in March 2024**

Treat it primarily as:

**Legacy/classic exam knowledge**

---

# Quick Cheat Sheet

| Requirement | Best Association |
|---|---|
| Classic 100 PB Device | Snowmobile |
| Tens of PB | Snowmobile |
| Entire Data Center Migration | Snowmobile |
| Truck-Scale Transfer | Snowmobile |
| Extreme Offline Migration | Snowmobile |
| Hundreds of TB | Snowball Edge |
| Edge Computing | Snowball Edge |
| Small Portable Edge Device | Snowcone |
| Recurring Online Transfer | DataSync |
| Ongoing Hybrid Storage | Storage Gateway |
| Dedicated Network | Direct Connect |

---

## Master Memory Trick

> [!tip] Master Memory Trick
> Imagine the migration keeps getting bigger:
>
> **Snowcone**
>
> → "I can carry this."
>
> **Snowball Edge**
>
> → "We're shipping boxes."
>
> **Snowmobile**
>
> → "Forget the boxes. Bring the truck."

So remember the classic hierarchy:

> **CONE**
> → Small / Portable
>
> **BALL**
> → Large
>
> **MOBILE**
> → Massive

And the killer Snowmobile clue:

> **TENS OF PETABYTES**
>
> +
>
> **ENTIRE DATA CENTER**
>
> +
>
> **OFFLINE MIGRATION**
>
> =
>
> **SNOWMOBILE**

But add one modern footnote to your memory:

> **Snowmobile = Classic / Legacy AWS Exam Knowledge**
>
> AWS stopped accepting new customers in **2024**.

---

## Related Notes

- [[Snow Family]]
- [[Snowcone]]
- [[Snowball Edge]]
- [[Snowball Edge Storage Optimized]]
- [[Snowball Edge Compute Optimized]]
- [[DataSync]]
- [[Storage Gateway]]
- [[05-Networking/Direct Connect]]
- [[S3]]
- [[S3 Transfer Acceleration]]
- [[06-Security/KMS]]