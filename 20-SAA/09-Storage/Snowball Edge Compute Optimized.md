## What Problem Does It Solve?

[[Snowball Edge Compute Optimized]] is designed for:

**Compute-intensive workloads at edge locations**

where connectivity to an AWS Region may be:

- Limited
- Intermittent
- Unavailable
- Too high-latency

It solves the problem of:

> **"How can I run substantial compute workloads close to where my data is generated when I cannot depend on continuous connectivity to an AWS Region?"**

Architecture:

Sensors / Cameras / Applications  
↓  
Snowball Edge Compute Optimized  
↓  
Local Compute + Storage  
↓  
Results / Data  
↓  
AWS Later

> [!tip] Memory Trick
> **Compute Optimized = Bring the COMPUTE to the data**

---

# What Is Snowball Edge Compute Optimized?

Snowball Edge Compute Optimized is part of:

[[Snowball Edge]]

within the:

[[Snow Family]]

It is a:

**Rugged physical edge-computing device**

optimized primarily for:

**Compute power**

rather than maximum storage capacity.

---

# Primary Exam Purpose

For SAA, the strongest association should be:

> **Remote location + substantial local processing + limited connectivity**
>
> → **Snowball Edge Compute Optimized**

Think:

Edge Location  
+
Poor Network  
+
Heavy Processing  
=
Snowball Edge Compute Optimized

---

# Edge Computing

Edge computing means processing data:

**Close to where the data is generated**

rather than sending all raw data to:

**An AWS Region**

Architecture:

Data Source  
↓  
Local Compute  
↓  
Process / Filter / Analyze  
↓  
Send Important Results to AWS

This reduces dependence on:

- Internet bandwidth
- WAN connectivity
- Region latency

---

# Why Compute at the Edge?

Imagine a remote factory generating:

**Large amounts of sensor and video data**

Sending everything to an AWS Region would require:

**Large amounts of bandwidth**

Instead:

Cameras + Sensors  
↓  
Snowball Edge Compute Optimized  
↓  
Process Locally  
↓  
Send Relevant Results to AWS

This can dramatically reduce:

**The amount of data that must cross the network**

---

# Compute Resources

Compute Optimized provides significantly more:

**Compute capability**

than a storage-focused Snow device.

For exam purposes, focus on:

- CPU-heavy workloads
- Local processing
- Edge analytics
- Machine learning inference
- Video processing

The exact hardware specifications can change over time.

> [!tip] Exam Strategy
> Memorize the **architectural purpose**, not every CPU or RAM number.

---

# EC2-Compatible Compute

Snowball Edge supports:

**EC2-compatible compute instances**

at the edge.

Conceptually:

Application  
↓  
EC2-Compatible Instance  
↓  
Snowball Edge Compute Optimized

This allows workloads to run using familiar AWS-style compute capabilities:

**Outside an AWS Region**

---

# Disconnected Operation

Snowball Edge Compute Optimized can operate in environments with:

**Limited or no network connectivity**

This makes it useful for:

- Remote industrial sites
- Ships
- Field operations
- Disaster-response locations
- Research sites
- Temporary remote environments

### Exam Pattern

> **Need substantial AWS-style compute where AWS Region connectivity is unreliable**
>
> → **Snowball Edge Compute Optimized**

---

# Video Processing

Video analytics is a classic use case.

Architecture:

Cameras  
↓  
Massive Video Streams  
↓  
Snowball Edge Compute Optimized  
↓  
Local Analysis  
↓  
Relevant Results  
↓  
AWS

Instead of uploading:

**Every second of raw video**

the device can process the data:

**Locally**

---

# Machine Learning Inference

Another strong use case is:

**ML inference at the edge**

Architecture:

Trained Model  
↓  
Snowball Edge  
↓  
Local Data  
↓  
Inference  
↓  
Prediction / Result

This is useful when:

- Low latency is required
- Connectivity is unreliable
- Raw data should remain local
- Sending every request to AWS is impractical

---

# Industrial IoT

Imagine:

Factory Machines  
↓  
Sensors  
↓  
Generate Continuous Data  
↓  
Snowball Edge Compute Optimized  
↓  
Analyze Locally

The device can help detect:

- Equipment anomalies
- Operational events
- Important patterns

without requiring every sensor reading to first reach:

**An AWS Region**

---

# Local Data Filtering

Sometimes the goal is not to keep all raw data.

Example:

1 TB Raw Data  
↓  
Snowball Edge  
↓  
Local Processing  
↓  
50 GB Relevant Data  
↓  
AWS

This reduces:

**Network transfer requirements**

### Memory Trick

**Process first, upload later**

---

# Low-Latency Processing

If a workload requires:

**Fast local responses**

sending every request to a distant AWS Region may introduce unacceptable latency.

Snowball Edge Compute Optimized allows:

**Processing close to the source**

### Exam Clue

> **Edge + low latency + substantial compute**
>
> → Compute Optimized

---

# Data Transfer

Although the device is optimized for compute, it can still support:

**Data storage and transfer**

The distinction is not:

> Compute Optimized cannot store data.

The distinction is:

> **Compute is the primary design emphasis.**

---

# Compute Optimized vs Storage Optimized

This is the most important comparison.

## [[Snowball Edge Storage Optimized]]

Primary emphasis:

**Storage**

Think:

- Large migration
- Large local dataset
- Storage-heavy workload

---

## Snowball Edge Compute Optimized

Primary emphasis:

**Compute**

Think:

- Video analytics
- ML inference
- Local processing
- CPU-intensive edge workloads

### Master Memory Trick

**DATA SIZE problem**
→ Storage Optimized

**PROCESSING problem**
→ Compute Optimized

---

# Compute Optimized vs Snowcone

## [[Snowcone]]

Think:

- Small
- Portable
- Lightweight edge
- Limited physical space
- Smaller workloads

---

## Compute Optimized

Think:

- Larger
- More powerful
- Substantial compute
- Heavier edge workloads

### Exam Decision

Need portability  
→ Snowcone

Need horsepower  
→ Snowball Edge Compute Optimized

---

# Compute Optimized vs Lambda

[[02-Compute/Lambda]] normally runs:

**Inside AWS infrastructure**

and requires connectivity to AWS services.

Snowball Edge allows compute to run:

**At the edge**

where connectivity may be unavailable.

### Exam Thinking

Need normal serverless compute in AWS  
→ Lambda

Need substantial compute in disconnected remote location  
→ Snowball Edge Compute Optimized

---

# Compute Optimized vs EC2

[[EC2]] normally runs:

**In an AWS Region**

Snowball Edge can provide:

**EC2-compatible compute at the edge**

### Memory Trick

**EC2 = Compute in AWS**

**Snowball Edge = AWS-style compute brought to you**

---

# Compute Optimized vs Outposts

These can both provide compute outside a normal AWS Region.

## Snowball Edge Compute Optimized

Think:

- Portable
- Rugged
- Remote
- Disconnected
- Temporary / mobile environments

---

## AWS Outposts

Think:

- Installed at customer data center
- Long-term hybrid infrastructure
- Consistent AWS experience on-premises

### Memory Trick

**Outposts = AWS installed at your building**

**Snowball Edge = AWS compute you can take into the field**

---

# Compute Optimized vs DataSync

## [[DataSync]]

Purpose:

**Move data**

---

## Snowball Edge Compute Optimized

Purpose:

**Process data locally**

### Exam Decision

Migrate NFS dataset  
→ DataSync

Analyze remote camera footage locally  
→ Compute Optimized

---

# Compute Optimized vs Storage Gateway

## [[Storage Gateway]]

Purpose:

**Hybrid storage access**

---

## Compute Optimized

Purpose:

**Edge compute**

### Memory Trick

**Gateway = Storage bridge**

**Compute Optimized = Edge server**

---

# Compute Optimized vs Local Zones

AWS Local Zones bring certain AWS services:

**Closer to metropolitan users**

but still depend on:

**AWS infrastructure and network connectivity**

Snowball Edge Compute Optimized is designed for situations where the environment may be:

**Remote or disconnected**

### Exam Decision

Low-latency AWS compute near a major city  
→ Local Zone

Disconnected field location  
→ Snowball Edge Compute Optimized

---

# Architecture Thinking

## Scenario 1 — Remote Video Analytics

A remote industrial facility has hundreds of cameras.

Internet bandwidth is limited.

Video must be analyzed locally before selected results are uploaded.

**Choose → Snowball Edge Compute Optimized**

---

## Scenario 2 — ML Inference

A remote site needs:

**Machine learning inference**

with very low latency.

Connectivity to AWS is unreliable.

**Choose → Snowball Edge Compute Optimized**

---

## Scenario 3 — Oil Platform

An offshore platform generates:

**Large amounts of sensor data**

It needs substantial local compute and cannot rely on continuous internet connectivity.

**Choose → Snowball Edge Compute Optimized**

---

## Scenario 4 — Large Offline Migration

A company primarily needs to move:

500 TB

to AWS.

The main problem is:

**Storage capacity**

not processing.

Choose:

[[Snowball Edge Storage Optimized]]

---

## Scenario 5 — Small Field Device

A field worker needs:

**Maximum portability**

for a relatively lightweight edge workload.

Choose:

[[Snowcone]]

---

## Scenario 6 — Normal Cloud Application

An application has reliable connectivity and simply needs scalable compute inside AWS.

Do NOT choose Snowball Edge.

Think:

[[EC2]]

or another normal AWS compute service.

---

# Scenario Recognition

Immediately think:

[[Snowball Edge Compute Optimized]]

when you see:

- Edge computing
- Heavy local processing
- Remote location
- Poor connectivity
- Disconnected environment
- Video analytics
- ML inference
- Sensor processing
- Low-latency local processing
- EC2-compatible edge compute
- Rugged hardware

### Strongest Exam Pattern

> **"A remote site with unreliable connectivity needs substantial compute resources to process data locally before sending results to AWS."**
>
> → **Snowball Edge Compute Optimized**

---

# Exam Traps

## Trap 1 — Compute Optimized Is Primarily for Maximum Storage

False.

Think:

**Compute power**

For maximum storage emphasis:

[[Snowball Edge Storage Optimized]]

---

## Trap 2 — Compute Optimized Requires Continuous Internet

False.

It is useful specifically for:

**Disconnected or intermittently connected environments**

---

## Trap 3 — Compute Optimized Cannot Store or Transfer Data

False.

It can.

The distinction is:

**Compute is the priority.**

---

## Trap 4 — Any Edge Workload Automatically Means Snowcone

False.

Ask:

**Portability or horsepower?**

Portability  
→ Snowcone

Horsepower  
→ Compute Optimized

---

## Trap 5 — Snowball Edge Is Needed for Normal EC2 Workloads

False.

If the workload can simply run in an AWS Region:

Use normal AWS compute.

Snowball Edge becomes relevant when:

**The compute must happen at the edge.**

---

## Trap 6 — Snowball Edge and Outposts Are Identical

False.

Snowball Edge:

**Portable / remote / disconnected**

Outposts:

**Long-term AWS infrastructure installed on-premises**

---

# Quick Cheat Sheet

| Requirement | Best Choice |
|---|---|
| Heavy Edge Compute | Compute Optimized |
| Video Analytics at Edge | Compute Optimized |
| ML Inference at Edge | Compute Optimized |
| Remote Sensor Processing | Compute Optimized |
| Poor / No Connectivity | Compute Optimized |
| Low-Latency Local Compute | Compute Optimized |
| Maximum Storage Focus | Storage Optimized |
| Large Offline Migration | Storage Optimized |
| Small Portable Edge Device | Snowcone |
| Standard Cloud Compute | EC2 |
| Long-Term AWS On-Prem Infrastructure | Outposts |

---

## Master Memory Trick

> [!tip] Master Memory Trick
> Imagine a remote factory has:
>
> **1,000 cameras**
>
> but:
>
> **Terrible internet**
>
> Sending every video stream to AWS is impossible.
>
> So AWS sends the factory:
>
> **COMPUTE POWER IN A BOX**
>
> ↓
> Snowball Edge Compute Optimized
>
> The box:
>
> **Processes locally**
> ↓
> **Filters the data**
> ↓
> **Sends only useful results to AWS**

Then ask:

> **WHAT'S THE PROBLEM?**

If:

> **"I have too much DATA to move."**
>
> → [[Snowball Edge Storage Optimized]]

If:

> **"I need more PROCESSING at the edge."**
>
> → **Snowball Edge Compute Optimized**

And remember:

> **SNOWCONE**
> → Portable
>
> **STORAGE OPTIMIZED**
> → Data
>
> **COMPUTE OPTIMIZED**
> → Processing

---

## Related Notes

- [[Snow Family]]
- [[Snowball Edge]]
- [[Snowball Edge Storage Optimized]]
- [[Snowcone]]
- [[Snowmobile]]
- [[EC2]]
- [[02-Compute/Lambda]]
- [[DataSync]]
- [[Storage Gateway]]
- [[AWS Outposts]]
- [[Local Zones]]
- [[S3]]