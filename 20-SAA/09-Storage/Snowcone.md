## What Problem Does It Solve?

[[Snowcone]] is the smallest and most portable device in the:

[[Snow Family]]

It is designed for:

- Edge computing
- Data collection
- Smaller offline data transfers
- Remote or disconnected environments

It solves the problem of:

> **"How can I collect, process, or move data in a remote location where connectivity, space, or power may be limited?"**

Think:

Remote Location  
↓  
Snowcone  
↓  
Store / Process Data  
↓  
Transfer or Ship to AWS

> [!tip] Memory Trick
> **SnowCONE = Small, portable Snow device**

---

# What Is Snowcone?

Snowcone is a:

**Small, rugged, secure edge computing and data-transfer device**

It can be used in environments such as:

- Factories
- Remote offices
- Vehicles
- Ships
- Field locations
- Research sites
- Areas with limited connectivity

The key exam idea is:

> **Snowcone is optimized for portability.**

---

# Snowcone Size

Snowcone is much smaller than:

[[Snowball Edge]]

Think:

Snowcone  
→ Portable

Snowball Edge  
→ Larger

### Memory Trick

**Cone < Ball**

---

# Storage Capacity

The Maarek course highlights Snowcone with approximately:

**8 TB of usable HDD storage**

It also discusses:

**Snowcone SSD**

with higher-performance solid-state storage.

For the SAA exam, the exact number is less important than remembering:

> **Snowcone has much less storage capacity than Snowball Edge.**

---

# Snowcone SSD

Snowcone SSD provides:

**Solid-state storage**

rather than traditional HDD storage.

This is useful when:

- Faster storage performance is needed
- The workload benefits from SSD
- Portability is still important

### Memory Trick

**Snowcone SSD = Small Snow + Faster Disk**

---

# Edge Computing

One of Snowcone's major purposes is:

**Edge Computing**

Edge computing means processing data:

**Near where the data is generated**

instead of requiring constant connectivity to an AWS Region.

Architecture:

Sensors / Cameras / Machines  
↓  
Snowcone  
↓  
Local Processing  
↓  
AWS Later

---

# Why Edge Computing?

Imagine a remote research station.

Sensors generate:

**Large amounts of data**

but internet connectivity is:

**Slow or unreliable**

Instead of sending everything immediately:

Sensors  
↓  
Snowcone  
↓  
Process / Store Locally  
↓  
Send Important Results Later

This allows the workload to continue even when:

**AWS connectivity is unavailable**

---

# Disconnected Environments

Snowcone is especially useful for:

**Disconnected or intermittently connected environments**

Examples:

- Remote wilderness
- Ships at sea
- Disaster areas
- Military-style field environments
- Industrial locations
- Temporary field operations

### Exam Pattern

> **Small portable AWS device + remote location + poor connectivity**
>
> → **Snowcone**

---

# Rugged Design

Snowcone is designed to operate as:

**A rugged portable device**

This matters because edge environments may not look like:

**Traditional data centers**

Think:

Data Center  
❌

Remote Field Site  
✅

---

# Data Transfer

Snowcone can also be used to:

**Move data into AWS**

Architecture:

On-Premises / Edge  
↓  
Copy Data to Snowcone  
↓  
Ship Device  
↓  
AWS  
↓  
Import Data

This is similar conceptually to:

[[Snowball Edge]]

but at:

**Smaller scale**

---

# DataSync with Snowcone

A very important Snowcone feature is integration with:

[[DataSync]]

Data can be transferred from Snowcone to AWS:

**Over the network**

when connectivity becomes available.

Architecture:

Snowcone  
↓  
DataSync  
↓  
AWS

This gives two ways to move data:

1. Ship the device
2. Transfer data online using DataSync

> [!tip] Memory Trick
> **Snowcone can SHIP or SYNC**

---

# Ship the Device

When network connectivity is poor:

Data  
↓  
Snowcone  
↓  
Physical Shipment  
↓  
AWS

This allows data to reach AWS without depending on:

**Internet bandwidth**

---

# Transfer with DataSync

When sufficient connectivity exists:

Data  
↓  
Snowcone  
↓  
[[DataSync]]  
↓  
AWS

This avoids physically shipping the device when:

**Online transfer becomes practical**

---

# Snowcone Compute

Snowcone can support:

**Edge compute capabilities**

allowing applications to process data locally.

The main exam takeaway is:

> Snowcone is not simply a portable hard drive.

It is an:

**AWS edge computing device**

---

# Snowcone vs Snowball Edge

This is the most important Snowcone comparison.

## Snowcone

Think:

- Small
- Portable
- Lightweight edge
- Smaller datasets
- Limited space
- Remote locations

---

## [[Snowball Edge]]

Think:

- Larger
- More storage
- More compute
- Large migrations
- Heavier edge workloads

### Memory Trick

**Snowcone = Backpack**

**Snowball Edge = Server box**

---

# Snowcone vs Snowball Edge Storage Optimized

## Snowcone

Best when:

**Portability matters most**

---

## Snowball Edge Storage Optimized

Best when:

**Large data capacity matters most**

### Exam Decision

Small remote device  
→ Snowcone

Large offline migration  
→ Snowball Edge Storage Optimized

---

# Snowcone vs Snowball Edge Compute Optimized

## Snowcone

Provides:

**Portable edge computing**

---

## Snowball Edge Compute Optimized

Provides:

**More substantial edge compute capability**

### Exam Decision

Lightweight / portable edge workload  
→ Snowcone

Compute-intensive edge workload  
→ Snowball Edge Compute Optimized

---

# Snowcone vs DataSync

## [[DataSync]]

Provides:

**Online data movement**

using a network.

---

## Snowcone

Provides:

**Physical data movement + edge computing**

They can also:

**Work together**

### Memory Trick

**DataSync = Network**

**Snowcone = Device**

**Snowcone + DataSync = Device can sync when connected**

---

# Snowcone vs Storage Gateway

## [[Storage Gateway]]

Provides:

**Ongoing hybrid storage access**

---

## Snowcone

Provides:

- Edge computing
- Portable storage
- Physical data transfer

### Exam Decision

On-premises application continuously accesses AWS storage  
→ Storage Gateway

Remote location needs portable AWS compute/storage  
→ Snowcone

---

# Snowcone vs Outposts

Both can involve:

**AWS infrastructure outside an AWS Region**

but they solve very different problems.

## Snowcone

Think:

- Portable
- Temporary
- Rugged
- Remote
- Disconnected
- Data transfer

---

## AWS Outposts

Think:

- AWS infrastructure installed at a customer site
- Long-term hybrid infrastructure
- Data-center environment

### Memory Trick

**Snowcone = Take AWS with you**

**Outposts = Install AWS at your site**

---

# Architecture Thinking

## Scenario 1 — Remote Research Team

Scientists work in a remote location with:

**Poor internet connectivity**

They need to:

- Collect data
- Process some data locally
- Eventually move it into AWS

Portability is important.

**Choose → Snowcone**

---

## Scenario 2 — Ship Data from Remote Site

A field office has several TB of data.

Its network connection is too slow to upload the data.

**Choose → Snowcone**

Load the data and:

**Ship the device to AWS**

---

## Scenario 3 — Connectivity Returns

A Snowcone device contains collected field data.

The site now has sufficient network connectivity.

The organization wants to send the data to AWS without shipping the device.

**Choose:**

Snowcone  
+  
[[DataSync]]

---

## Scenario 4 — 500 TB Migration

A data center needs to migrate:

500 TB

to AWS.

Snowcone is probably too small.

Choose:

[[Snowball Edge]]

---

## Scenario 5 — Heavy Edge Compute

A remote industrial site needs substantial compute resources for:

**Compute-intensive processing**

Do not automatically choose Snowcone just because it is an edge workload.

Consider:

**Snowball Edge Compute Optimized**

---

## Scenario 6 — Continuous Hybrid NFS

An application needs continuous NFS access to S3.

Do NOT choose Snowcone.

Choose:

[[S3 File Gateway]]

---

# Scenario Recognition

Immediately think:

[[Snowcone]]

when you see:

- Smallest Snow device
- Portable
- Rugged
- Remote location
- Limited space
- Limited connectivity
- Disconnected environment
- Edge computing
- Smaller data migration
- DataSync integration

### Strongest Exam Pattern

> **"A small, portable, rugged AWS device is required for edge computing in a remote location with unreliable connectivity."**
>
> → **Snowcone**

---

# Exam Traps

## Trap 1 — Snowcone Is Only a Data-Transfer Device

False.

It can also support:

**Edge computing**

---

## Trap 2 — Snowcone Requires Continuous Internet Access

False.

It is designed for environments with:

**Limited or unavailable connectivity**

---

## Trap 3 — Snowcone Is Best for Huge Petabyte Migrations

False.

Think:

[[Snowball Edge]]

for much larger migration jobs.

---

## Trap 4 — Snowcone and DataSync Cannot Work Together

False.

Snowcone can use:

[[DataSync]]

for online data transfer.

---

## Trap 5 — Snowcone Is the Same as Storage Gateway

False.

Storage Gateway:

**Ongoing hybrid storage**

Snowcone:

**Portable edge + data transfer**

---

## Trap 6 — Snowcone Is Just an External Hard Drive

False.

It provides:

**AWS edge capabilities**

in addition to storage.

---

# Quick Cheat Sheet

| Requirement | Snowcone |
|---|---|
| Smallest Snow Device | ✅ |
| Portable | ✅ |
| Rugged | ✅ |
| Edge Computing | ✅ |
| Remote Locations | ✅ |
| Poor Connectivity | ✅ |
| Disconnected Operation | ✅ |
| Physical Data Transfer | ✅ |
| DataSync Integration | ✅ |
| Smaller Migration Jobs | ✅ |
| Large 500 TB Migration | ❌ |
| Heavy Edge Compute | Prefer Snowball Edge |
| Ongoing Hybrid File Access | ❌ |

---

## Master Memory Trick

> [!tip] Master Memory Trick
> Imagine an AWS engineer shrinking a Snowball until you can carry it around.
>
> That's:
>
> **SNOWCONE**
>
> Take it to:
>
> **Remote Site**
> ↓
> Collect Data
> ↓
> Process Locally
> ↓
> No Internet? → **SHIP IT**
>
> Internet Available? → **DATASYNC IT**

So remember:

> **SMALL**
>
> **PORTABLE**
>
> **RUGGED**
>
> **EDGE**
>
> **REMOTE**
>
> = **SNOWCONE**

And for the Snow family:

> **Snowcone**
> → Small / Portable
>
> **Snowball Edge**
> → Large / Powerful
>
> **Snowmobile**
> → Massive

---

## Related Notes

- [[Snow Family]]
- [[Snowball Edge]]
- [[Snowmobile]]
- [[DataSync]]
- [[Storage Gateway]]
- [[S3 File Gateway]]
- [[S3]]