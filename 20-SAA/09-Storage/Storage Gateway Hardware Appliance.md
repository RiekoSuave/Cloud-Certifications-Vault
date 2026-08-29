## What Problem Does It Solve?

[[Storage Gateway Hardware Appliance]] provides a physical hardware option for deploying:

[[Storage Gateway]]

in an on-premises environment.

It solves the problem of:

> **"We need Storage Gateway on-premises, but we don't have the virtualization infrastructure or resources required to run the gateway as a virtual machine."**

Instead of:

On-Premises Hypervisor  
↓  
Storage Gateway VM  
↓  
AWS

you can use:

Storage Gateway Hardware Appliance  
↓  
AWS

> [!tip] Memory Trick
> **No VM infrastructure? Use the hardware appliance.**

---

## Storage Gateway Deployment

Storage Gateway normally requires an:

**On-Premises Gateway**

The gateway can run as:

- A virtual appliance
- A physical hardware appliance

The hardware appliance provides:

**Storage Gateway functionality in dedicated physical hardware**

---

# Why Use the Hardware Appliance?

A company may not have:

**Virtualization infrastructure**

available at a location.

For example:

Branch Office  
↓  
No VMware / Hypervisor Capacity  
↓  
Need Storage Gateway  
↓  
Hardware Appliance

### Exam Pattern

> **"The company does not have virtualization resources available to deploy Storage Gateway."**
>
> → **Storage Gateway Hardware Appliance**

---

# Physical Appliance

Unlike a virtual gateway running on a hypervisor, the hardware appliance is:

**Physical hardware**

deployed:

**On-Premises**

Architecture:

On-Premises Applications  
↓  
Storage Gateway Hardware Appliance  
↓  
AWS Storage

---

# Preconfigured Hardware

The hardware appliance comes:

**Preconfigured**

for Storage Gateway deployment.

This reduces the need to provide:

- A separate server
- Hypervisor infrastructure
- Virtual-machine resources

### Memory Trick

**Hardware Appliance = Gateway in a box**

---

# Supported Gateway Types

The hardware appliance can support Storage Gateway workloads such as:

- File Gateway
- Volume Gateway
- Tape Gateway

The key exam concept is not usually the specific gateway type.

The important clue is:

> **Storage Gateway is required, but virtual infrastructure is unavailable or undesirable.**

---

# Branch Office Use Case

A branch office needs hybrid access to AWS storage.

However:

- It has limited IT infrastructure
- It does not have sufficient virtualization resources
- It still needs Storage Gateway

Architecture:

Branch Office  
↓  
Hardware Appliance  
↓  
AWS

This is a classic fit for:

[[Storage Gateway Hardware Appliance]]

---

# Data Center Use Case

A company may also use the hardware appliance in a:

**Data Center**

when it prefers dedicated physical infrastructure for:

Storage Gateway.

Architecture:

On-Premises Data Center  
↓  
Hardware Appliance  
↓  
AWS Storage

---

# Hardware Appliance + File Gateway

Example:

On-Premises Applications  
↓  
NFS / SMB  
↓  
Hardware Appliance  
↓  
[[S3 File Gateway]]  
↓  
[[S3]]

The hardware appliance provides the physical infrastructure on which the gateway functionality runs.

---

# Hardware Appliance + Volume Gateway

Example:

On-Premises Application  
↓  
iSCSI  
↓  
Hardware Appliance  
↓  
[[Volume Gateway]]  
↓  
AWS

This can provide:

**Hybrid block storage**

without requiring the organization to deploy a gateway VM.

---

# Hardware Appliance + Tape Gateway

Example:

Backup Software  
↓  
Virtual Tape Interface  
↓  
Hardware Appliance  
↓  
[[Tape Gateway]]  
↓  
AWS

This allows physical tape infrastructure to be replaced while using:

**Dedicated Storage Gateway hardware**

---

# Hardware Appliance vs Virtual Appliance

## Virtual Appliance

Storage Gateway runs as:

**A virtual machine**

Best when the organization already has:

**Virtualization infrastructure**

---

## Hardware Appliance

Storage Gateway runs on:

**Dedicated physical hardware**

Best when:

- Virtualization resources are unavailable
- Virtualization resources are limited
- Dedicated hardware is preferred

### Memory Trick

**Have VM infrastructure?**
→ Virtual Gateway

**No VM infrastructure?**
→ Hardware Appliance

---

# Hardware Appliance Is Not Snowball

This is an important conceptual distinction.

Both involve:

**Physical AWS-related hardware**

but they solve completely different problems.

---

## [[Snowball]]

Physical device used primarily for:

- Offline data migration
- Edge computing

The device can be:

**Shipped between customer and AWS**

---

## Storage Gateway Hardware Appliance

Physical device used for:

**Ongoing hybrid storage connectivity**

It remains:

**On-Premises**

### Memory Trick

**Snowball = Ship the box**

**Gateway Appliance = Keep the box**

---

# Hardware Appliance vs Storage Gateway

The hardware appliance is not a completely separate storage service.

It is a:

**Deployment option for Storage Gateway**

Think:

Storage Gateway  
↓  
Can Run As  
├── Virtual Appliance
└── Hardware Appliance

> [!warning] Exam Trap
> Do not think of the hardware appliance as another gateway type alongside:
>
> - File
> - Volume
> - Tape
>
> It is a **deployment method**.

---

# Hardware Appliance vs Direct Connect

[[05-Networking/Direct Connect]] provides:

**Dedicated network connectivity**

between:

On-Premises  
and  
AWS

The Storage Gateway Hardware Appliance provides:

**Storage Gateway functionality**

These services solve different layers of the architecture.

They can potentially work together.

Architecture:

Application  
↓  
Storage Gateway Appliance  
↓  
Direct Connect  
↓  
AWS

### Memory Trick

**Direct Connect = Network**

**Hardware Appliance = Storage Gateway**

---

# Hardware Appliance vs DataSync

## [[DataSync]]

Designed for:

**Moving data**

---

## Hardware Appliance

Provides infrastructure for:

**Ongoing Storage Gateway access**

### Exam Decision

Automated data migration  
→ DataSync

Hybrid storage without virtualization  
→ Storage Gateway Hardware Appliance

---

# Hardware Appliance vs Snowball

| Requirement | Hardware Appliance | Snowball |
|---|---:|---:|
| Physical Device | ✅ | ✅ |
| Stays On-Premises | ✅ | Temporary |
| Offline Migration | ❌ | ✅ |
| Hybrid Storage | ✅ | ❌ |
| Storage Gateway | ✅ | ❌ |
| Edge Computing | ❌ | ✅ |
| Ship Data Physically | ❌ | ✅ |

---

# Architecture Thinking

## Scenario 1 — No Virtualization

A company needs:

[[S3 File Gateway]]

at a branch office.

The office does not have:

**Virtualization infrastructure**

**Choose → Storage Gateway Hardware Appliance**

---

## Scenario 2 — Existing VMware Environment

A company already operates a large virtualization environment and has sufficient spare resources.

It needs Storage Gateway.

A:

**Virtual appliance**

may be appropriate.

The hardware appliance is not automatically required.

---

## Scenario 3 — Physical Data Migration

A company needs to migrate:

500 TB

with limited network bandwidth.

Do NOT choose the Storage Gateway Hardware Appliance merely because it is physical hardware.

Choose:

[[Snowball]]

---

## Scenario 4 — Dedicated Hybrid Storage Appliance

A company wants:

**Dedicated physical hardware**

for its Storage Gateway deployment.

**Choose → Storage Gateway Hardware Appliance**

---

## Scenario 5 — Backup Tape Replacement Without VM Capacity

A branch office needs:

[[Tape Gateway]]

but has insufficient resources to host the gateway as a VM.

**Choose:**

Storage Gateway Hardware Appliance  
+  
Tape Gateway

---

# Scenario Recognition

Immediately think:

[[Storage Gateway Hardware Appliance]]

when you see:

- Storage Gateway
- On-premises
- No virtualization
- Insufficient VM resources
- Physical appliance
- Dedicated hardware
- Branch office
- Hybrid storage

### Strongest Exam Pattern

> **"Storage Gateway is required, but the company does not have virtualization infrastructure available."**
>
> → **Storage Gateway Hardware Appliance**

---

# Exam Traps

## Trap 1 — Hardware Appliance Is a New Gateway Type

False.

The gateway types remain things such as:

- File Gateway
- Volume Gateway
- Tape Gateway

Hardware Appliance is a:

**Deployment option**

---

## Trap 2 — Hardware Appliance Is Snowball

False.

Snowball:

**Offline migration / edge computing**

Hardware Appliance:

**Ongoing Storage Gateway deployment**

---

## Trap 3 — Hardware Appliance Must Be Shipped Back to AWS After Data Transfer

False.

That sounds like:

[[Snowball]]

The Storage Gateway Hardware Appliance is deployed:

**On-Premises**

for ongoing use.

---

## Trap 4 — Hardware Appliance Provides Dedicated Network Connectivity

False.

That is closer to:

[[05-Networking/Direct Connect]]

The appliance provides:

**Storage Gateway functionality**

---

## Trap 5 — Hardware Appliance Is Required for Every Storage Gateway

False.

Storage Gateway can also run as:

**A virtual appliance**

---

# Quick Cheat Sheet

| Requirement | Answer |
|---|---|
| Storage Gateway + No VM Infrastructure | Hardware Appliance |
| Dedicated Physical Gateway | Hardware Appliance |
| Branch Office Without Hypervisor | Hardware Appliance |
| Existing VM Infrastructure | Virtual Appliance May Work |
| Offline Massive Migration | Snowball |
| Dedicated AWS Network | Direct Connect |
| Ongoing Hybrid Storage | Storage Gateway |
| Data Movement | DataSync |

---

## Master Memory Trick

> [!tip] Master Memory Trick
> Imagine Storage Gateway needs a house.
>
> Normally:
>
> **VM**
> → Gateway lives inside your virtualization environment.
>
> But there is no available VM infrastructure.
>
> AWS says:
>
> **"Fine. Here's the house too."**
>
> → Hardware Appliance

So memorize:

> **STORAGE GATEWAY**
>
> +
>
> **NO VIRTUALIZATION**
>
> =
>
> **HARDWARE APPLIANCE**

And never confuse:

> **Snowball**
> → Ship the box
>
> **Storage Gateway Hardware Appliance**
> → Keep the box and use it as your hybrid-storage gateway

---

## Related Notes

- [[Storage Gateway]]
- [[S3 File Gateway]]
- [[FSx File Gateway]]
- [[Volume Gateway]]
- [[Tape Gateway]]
- [[Snowball]]
- [[DataSync]]
- [[05-Networking/Direct Connect]]