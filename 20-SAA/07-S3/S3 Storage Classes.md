## What Problem Does It Solve?

[[S3 Storage Classes]] let you choose the right balance between:

- Storage cost
- Availability
- Access frequency
- Retrieval speed
- Retrieval cost
- Resiliency requirements

The architecture question is:

> **"How often will I access this data, how quickly must I retrieve it, and how much resilience do I need?"**

Different workloads have very different storage patterns.

Example:

Frequently Accessed Data  
↓  
[[S3 Standard]]

Unknown Access Pattern  
↓  
[[S3 Intelligent-Tiering]]

Infrequently Accessed but Must Be Immediately Available  
↓  
[[S3 Standard-IA]]

Recreatable Infrequent Data  
↓  
[[S3 One Zone-IA]]

Archive + Immediate Retrieval  
↓  
[[S3 Glacier Instant Retrieval]]

Long-Term Archive  
↓  
[[S3 Glacier Flexible Retrieval]]

Very Long-Term Archive  
↓  
[[S3 Glacier Deep Archive]]

> [!tip] Memory Trick
> **S3 Storage Class = How HOT or COLD is the data?**

---

## S3 Storage Class Family

The major storage classes to recognize for the SAA exam are:

- [[S3 Standard]]
- [[S3 Intelligent-Tiering]]
- [[S3 Standard-IA]]
- [[S3 One Zone-IA]]
- [[S3 Glacier Instant Retrieval]]
- [[S3 Glacier Flexible Retrieval]]
- [[S3 Glacier Deep Archive]]

You can move objects between storage classes:

- Manually
- Automatically with [[S3 Lifecycle Rules]]

---

## Durability vs Availability

Do not confuse these two terms.

### Durability

Durability asks:

> **"Will my object still exist?"**

S3 storage classes are designed for extremely high durability:

**99.999999999%**

Also called:

**11 9's durability**

### Memory Trick

**Durability = Don't lose my DATA**

---

### Availability

Availability asks:

> **"Can I access my object right now?"**

Availability varies by storage class.

For example:

[[S3 Standard]]

has:

**99.99% availability**

while:

[[S3 One Zone-IA]]

has:

**99.5% availability**

### Memory Trick

**Availability = Can I ACCESS it?**

> [!tip] Exam Distinction
> **Durability → Object survives**
>
> **Availability → Object is reachable**

---

# S3 Standard

[[S3 Standard]] is the general-purpose storage class for:

**Frequently accessed data**

Characteristics:

- 99.99% availability
- Low latency
- High throughput
- Stored across at least 3 Availability Zones
- Designed to sustain 2 concurrent facility failures
- No minimum storage duration charge
- No retrieval fee

Common workloads:

- Big data analytics
- Mobile applications
- Gaming applications
- Content distribution
- Frequently accessed application data

---

## Architecture Thinking — S3 Standard

Use S3 Standard when:

> **"The application accesses this data frequently and needs consistently low-latency access."**

Example:

Application  
↓ frequent reads/writes  
[[S3 Standard]]

Do not overthink it.

If the data is:

**Hot + Frequently Accessed**

think:

**S3 Standard**

---

# S3 Standard-IA

[[S3 Standard-IA]] means:

**Standard Infrequent Access**

Designed for data that:

- Is accessed less frequently
- Must still be retrieved quickly when needed

Characteristics:

- 99.9% availability
- Stored across at least 3 Availability Zones
- Lower storage cost than S3 Standard
- Retrieval fee
- 30-day minimum storage duration charge
- 128 KB minimum billable object size

Common use cases:

- Disaster recovery
- Backups
- Long-lived files accessed occasionally

> [!tip] Memory Trick
> **Standard-IA = Rarely needed, but READY immediately**

---

## Architecture Thinking — Standard-IA

Suppose a company stores disaster recovery files.

They rarely access them.

But during an outage:

**The files must be available immediately.**

Choose:

[[S3 Standard-IA]]

Why?

The requirement combines:

**Infrequent Access + Immediate Retrieval + Multi-AZ Resilience**

---

# S3 One Zone-IA

[[S3 One Zone-IA]] stores infrequently accessed data in:

**One Availability Zone**

Characteristics:

- 99.5% availability
- Single AZ
- Lower cost
- Retrieval fee
- 30-day minimum storage duration charge
- 128 KB minimum billable object size

Critical architecture rule:

> **If the Availability Zone is destroyed, the data can be lost.**

Therefore, use One Zone-IA for data that can be:

**Recreated**

or where another copy exists elsewhere.

---

## Good One Zone-IA Workloads

Examples:

- Secondary backup copies
- Re-creatable data
- Copies of on-premises data
- Non-critical infrequently accessed objects

### Memory Trick

**One Zone = One Basket**

If that basket disappears:

**Your data may disappear with it.**

---

## Standard-IA vs One Zone-IA

This is a major exam comparison.

### Standard-IA

Stored across:

**At least 3 AZs**

Use when:

Data must survive an AZ failure.

---

### One Zone-IA

Stored in:

**1 AZ**

Use when:

Data can be recreated.

### Exam Decision

> **Infrequent + Must survive AZ failure → Standard-IA**
>
> **Infrequent + Re-creatable + Cheapest → One Zone-IA**

---

# S3 Glacier Storage Classes

The Glacier family is designed for:

**Archiving and backups**

Think:

Hot Data  
↓  
S3 Standard  
↓  
Standard-IA  
↓  
Glacier  
↓  
Deep Archive  
↓  
Colder and Cheaper

The colder the data becomes:

**Storage cost generally decreases**

but:

**Retrieval considerations increase**

---

# S3 Glacier Instant Retrieval

[[S3 Glacier Instant Retrieval]] is designed for archived data that still requires:

**Millisecond retrieval**

Great for data accessed roughly:

**Once per quarter**

Characteristics:

- Millisecond retrieval
- At least 3 AZs
- Retrieval fee
- 90-day minimum storage duration
- 128 KB minimum billable object size

---

## Architecture Thinking — Glacier Instant Retrieval

Scenario:

A company stores medical imaging archives.

The data is rarely accessed.

However, when requested:

**It must be available immediately.**

Choose:

[[S3 Glacier Instant Retrieval]]

### Memory Trick

**Glacier Instant = Frozen but instantly reachable**

---

# S3 Glacier Flexible Retrieval

[[S3 Glacier Flexible Retrieval]] is designed for cold archival data where retrieval can take longer.

Formerly known as:

**S3 Glacier**

Retrieval options:

### Expedited

**1–5 minutes**

### Standard

**3–5 hours**

### Bulk

**5–12 hours**

The Maarek slides identify Bulk retrieval as:

**Free**

Minimum storage duration:

**90 days**

Minimum billable object size:

**40 KB**

> [!tip] Memory Trick
> **Flexible = Pick your thawing speed**

---

## Architecture Thinking — Glacier Flexible Retrieval

Scenario:

A company stores historical backups.

The data may occasionally need to be restored.

Waiting several hours is acceptable.

Choose:

[[S3 Glacier Flexible Retrieval]]

Why?

The workload is:

**Cold + Archived + Retrieval delay acceptable**

---

# S3 Glacier Deep Archive

[[S3 Glacier Deep Archive]] is designed for:

**Very long-term archival storage**

This is the coldest traditional S3 storage class.

Retrieval options:

### Standard

**12 hours**

### Bulk

**48 hours**

Minimum storage duration:

**180 days**

Minimum billable object size:

**40 KB**

Common workloads:

- Long-term compliance archives
- Records retention
- Data rarely expected to be retrieved
- Long-term backup archives

---

## Architecture Thinking — Deep Archive

Scenario:

A financial company must retain records for seven years.

The records are almost never accessed.

Retrieval within hours or days is acceptable.

The priority is:

**Lowest long-term archival storage cost**

Choose:

[[S3 Glacier Deep Archive]]

> [!tip] Memory Trick
> **Deep Archive = Digital Basement**
>
> Cheapest place for data you almost never touch.

---

# S3 Intelligent-Tiering

[[S3 Intelligent-Tiering]] automatically moves objects between access tiers based on usage patterns.

Use it when:

> **Access patterns are unknown or unpredictable.**

There is:

- Small monthly monitoring / auto-tiering fee
- No retrieval charges for Intelligent-Tiering

---

## Intelligent-Tiering Access Tiers

### Frequent Access Tier

Automatic.

Default tier.

---

### Infrequent Access Tier

Automatic.

Objects not accessed for:

**30 days**

---

### Archive Instant Access Tier

Automatic.

Objects not accessed for:

**90 days**

---

### Archive Access Tier

Optional.

Configurable from approximately:

**90 days to 700+ days**

---

### Deep Archive Access Tier

Optional.

Configurable from approximately:

**180 days to 700+ days**

---

## Architecture Thinking — Intelligent-Tiering

Scenario:

A company stores millions of objects.

Some are accessed frequently.

Others become cold.

The company cannot predict which objects will become inactive.

They want AWS to automatically optimize storage costs.

Choose:

[[S3 Intelligent-Tiering]]

### Memory Trick

**Unknown Pattern = Intelligent-Tiering**

S3 watches the access pattern and handles the tiering.

---

# Storage Class Architecture Spectrum

Think of S3 storage as a temperature scale:

**HOT**

↓  

[[S3 Standard]]

Frequently accessed

↓  

[[S3 Intelligent-Tiering]]

Unknown / changing access

↓  

[[S3 Standard-IA]]

Rarely accessed, immediate retrieval, Multi-AZ

↓  

[[S3 One Zone-IA]]

Rarely accessed, recreatable, Single-AZ

↓  

[[S3 Glacier Instant Retrieval]]

Archive + milliseconds

↓  

[[S3 Glacier Flexible Retrieval]]

Archive + minutes/hours

↓  

[[S3 Glacier Deep Archive]]

Long-term archive + hours

↓  

**COLD**

---

# Architecture Thinking

## Scenario 1 — Frequently Accessed Website Content

A website frequently reads images and application assets from S3.

The application requires low latency and high throughput.

**Choose → [[S3 Standard]]**

---

## Scenario 2 — Disaster Recovery Backups

Backups are rarely accessed.

But during a disaster:

They must be retrieved immediately.

The backups must survive the loss of an Availability Zone.

**Choose → [[S3 Standard-IA]]**

---

## Scenario 3 — Re-creatable Backup Copy

A company already maintains its primary backup elsewhere.

It wants the lowest-cost IA class for a secondary copy that can be recreated.

**Choose → [[S3 One Zone-IA]]**

---

## Scenario 4 — Archive with Immediate Retrieval

Archived records are accessed roughly once every few months.

When accessed, users need millisecond retrieval.

**Choose → [[S3 Glacier Instant Retrieval]]**

---

## Scenario 5 — Archive with Hours of Retrieval Time

Historical backups are rarely accessed.

A restore taking several hours is acceptable.

**Choose → [[S3 Glacier Flexible Retrieval]]**

---

## Scenario 6 — Seven-Year Compliance Archive

Records must be retained for years.

They are almost never accessed.

Retrieval can take many hours.

Cost must be minimized.

**Choose → [[S3 Glacier Deep Archive]]**

---

## Scenario 7 — Unknown Access Pattern

A data lake contains millions of objects.

The company does not know which objects will remain hot and which will become cold.

They want automatic cost optimization.

**Choose → [[S3 Intelligent-Tiering]]**

---

# Minimum Storage Duration

This matters in cost-optimization questions.

| Storage Class | Minimum Storage Duration |
|---|---:|
| S3 Standard | None |
| S3 Intelligent-Tiering | None |
| S3 Standard-IA | 30 days |
| S3 One Zone-IA | 30 days |
| Glacier Instant Retrieval | 90 days |
| Glacier Flexible Retrieval | 90 days |
| Glacier Deep Archive | 180 days |

### Memory Trick

**IA = 30**

**Glacier = 90**

**Deep Archive = 180**

---

# Retrieval Fees

| Storage Class | Retrieval Fee |
|---|---|
| S3 Standard | ❌ |
| S3 Intelligent-Tiering | ❌ |
| S3 Standard-IA | ✅ |
| S3 One Zone-IA | ✅ |
| Glacier Instant Retrieval | ✅ |
| Glacier Flexible Retrieval | ✅ |
| Glacier Deep Archive | ✅ |

### Architecture Lesson

Lower storage cost does not automatically mean:

**Lower total cost**

If you constantly retrieve objects from an infrequent-access or archive class:

Retrieval fees can erase the storage savings.

---

# Availability Zone Comparison

| Storage Class | AZ Design |
|---|---|
| S3 Standard | ≥ 3 AZs |
| Intelligent-Tiering | ≥ 3 AZs |
| Standard-IA | ≥ 3 AZs |
| One Zone-IA | 1 AZ |
| Glacier Instant Retrieval | ≥ 3 AZs |
| Glacier Flexible Retrieval | ≥ 3 AZs |
| Glacier Deep Archive | ≥ 3 AZs |

The giant exception:

> **One Zone-IA = ONE AZ**

---

# Scenario Recognition

## Immediately Think S3 Standard When You See

- Frequently accessed
- Low latency
- High throughput
- General-purpose storage

---

## Immediately Think Standard-IA When You See

- Infrequent access
- Immediate retrieval
- Backups
- Disaster recovery
- Multi-AZ resilience

---

## Immediately Think One Zone-IA When You See

- Re-creatable data
- Secondary backup
- Infrequent access
- Single AZ acceptable
- Reduce cost

---

## Immediately Think Glacier Instant Retrieval When You See

- Archive
- Rare access
- Millisecond retrieval
- Immediate archive access

---

## Immediately Think Glacier Flexible Retrieval When You See

- Archive
- Minutes or hours acceptable
- Expedited / Standard / Bulk retrieval

---

## Immediately Think Deep Archive When You See

- Long-term retention
- Compliance
- Years
- Lowest archive cost
- Retrieval delay acceptable

---

## Immediately Think Intelligent-Tiering When You See

- Unknown access pattern
- Unpredictable access
- Automatically optimize storage cost
- Objects become hot and cold unpredictably

---

# Exam Traps

## Trap 1 — All S3 Classes Have the Same Availability

False.

Availability varies by storage class.

---

## Trap 2 — Durability and Availability Are the Same

False.

**Durability = Will the object survive?**

**Availability = Can I access it right now?**

---

## Trap 3 — One Zone-IA Survives AZ Destruction

False.

The object is stored in:

**One Availability Zone**

If that AZ is destroyed:

**The data can be lost.**

---

## Trap 4 — Glacier Always Means Slow Retrieval

False.

[[S3 Glacier Instant Retrieval]] provides:

**Millisecond retrieval**

---

## Trap 5 — Intelligent-Tiering Has Retrieval Charges

The Maarek slides specifically emphasize:

**No retrieval charges in Intelligent-Tiering**

There is instead a:

**Small monitoring and auto-tiering fee**

---

## Trap 6 — Deep Archive Has a 90-Day Minimum

False.

Deep Archive:

**180 days**

Glacier Instant and Flexible:

**90 days**

---

## Trap 7 — Standard-IA Is Best for Short-Lived Temporary Data

Be careful.

Standard-IA has a:

**30-day minimum storage duration charge**

For short-lived objects, that can make it a poor cost choice.

---

## Trap 8 — Cheapest Storage Price Always Means Cheapest Architecture

False.

Consider:

- Retrieval fees
- Minimum storage duration
- Minimum billable object size
- Access frequency
- Availability requirements

The exam often asks for the:

**Most cost-effective solution that still meets the requirements**

---

# Quick Cheat Sheet

| Storage Class | Best For | Retrieval | Min Duration | AZs |
|---|---|---|---:|---:|
| [[S3 Standard]] | Frequent access | Milliseconds | None | ≥ 3 |
| [[S3 Intelligent-Tiering]] | Unknown access | Depends on tier | None | ≥ 3 |
| [[S3 Standard-IA]] | Infrequent + resilient | Milliseconds | 30 days | ≥ 3 |
| [[S3 One Zone-IA]] | Re-creatable IA | Milliseconds | 30 days | 1 |
| [[S3 Glacier Instant Retrieval]] | Archive + immediate access | Milliseconds | 90 days | ≥ 3 |
| [[S3 Glacier Flexible Retrieval]] | Cold archive | Minutes–hours | 90 days | ≥ 3 |
| [[S3 Glacier Deep Archive]] | Long-term archive | Hours | 180 days | ≥ 3 |

---

## Master Memory Trick

> [!tip] Master Memory Trick
> Ask three questions:
>
> **1. How often is the data accessed?**
>
> **2. How fast must retrieval be?**
>
> **3. Can I tolerate losing one AZ?**

Then:

**Hot → Standard**

**Unknown → Intelligent-Tiering**

**Cold + Instant + Multi-AZ → Standard-IA**

**Cold + Re-creatable + One AZ → One Zone-IA**

**Archive + Instant → Glacier Instant**

**Archive + Hours → Glacier Flexible**

**Almost Never + Cheapest Long-Term → Deep Archive**

And memorize:

> **IA = 30 days**
>
> **Glacier = 90 days**
>
> **Deep Archive = 180 days**
>
> **One Zone-IA = ONE AZ**

---

## Related Notes

- [[S3]]
- [[S3 Standard]]
- [[S3 Standard-IA]]
- [[S3 One Zone-IA]]
- [[S3 Intelligent-Tiering]]
- [[S3 Glacier Instant Retrieval]]
- [[S3 Glacier Flexible Retrieval]]
- [[S3 Glacier Deep Archive]]
- [[S3 Lifecycle Rules]]
- [[03-Storage/S3 Replication]]
- [[Availability Zones]]
- [[Disaster Recovery]]