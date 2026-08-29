## What Problem Does It Solve?

**Lambda SnapStart**

helps reduce:

**Cold-start latency**

for supported [[Lambda]] runtimes by initializing the function ahead of time and creating a:

**Snapshot of the initialized execution environment**

When Lambda needs a new execution environment:

Instead of performing the entire initialization process again:

Snapshot  
↓  
Restore  
↓  
Function Ready

> [!tip] Memory Trick
> **SnapStart = SNAPSHOT → RESTORE → START FAST**

---

## The Cold Start Problem

When Lambda creates a new execution environment, initialization can include:

1. Starting the runtime
2. Loading function code
3. Loading dependencies
4. Running initialization code
5. Preparing the execution environment

Architecture:

Request  
↓  
New Environment Needed  
↓  
Initialize Runtime  
↓  
Load Code  
↓  
Run Initialization  
↓  
Invoke Handler

This can create:

**Cold-start latency**

---

## Why Some Functions Have Larger Cold Starts

Cold starts can become more noticeable when a function has:

- Large dependencies
- Large frameworks
- Significant initialization code
- Runtime initialization overhead
- Complex startup logic

The result can be:

**Higher latency on new execution environments**

---

# How SnapStart Works

With SnapStart enabled, Lambda performs initialization when you:

**Publish a function version**

Conceptually:

Publish Version  
↓  
Lambda Initializes Function  
↓  
Snapshot Created  
↓  
Snapshot Cached

Later:

Invocation  
↓  
New Environment Needed  
↓  
Restore Snapshot  
↓  
Function Runs

### Memory Trick

**Initialize ONCE → Snapshot → Restore MANY**

---

# Without SnapStart

New Environment  
↓  
Runtime Initialization  
↓  
Function Initialization  
↓  
Handler

---

# With SnapStart

New Environment  
↓  
Restore Initialized Snapshot  
↓  
Handler

The goal is to reduce:

**Initialization work during cold starts**

---

# Published Versions

SnapStart works with:

**Published Lambda versions**

not simply the mutable:

`$LATEST`

version.

### Killer Exam Clue

> **SnapStart must be enabled and a new function version published**
>
> → Lambda creates an optimized snapshot for that version.

---

## Why Published Versions Matter

Published versions are:

**Immutable**

That makes them suitable for:

**Creating reusable initialization snapshots**

Example:

Version 7  
↓  
SnapStart Snapshot

Alias:

`prod`  
↓  
Version 7

Production invocations can then use:

**The SnapStart-enabled version**

---

# SnapStart and Aliases

Aliases can point to:

**SnapStart-enabled published versions**

Architecture:

Client  
↓  
Alias `prod`  
↓  
Version 12  
↓  
SnapStart Restore  
↓  
Lambda

This allows aliases to continue providing:

- Stable endpoints
- Version management
- Deployment control

while the referenced version uses:

**SnapStart**

---

# Supported Runtimes

SnapStart is available only for:

**Supported managed Lambda runtimes**

Runtime support has expanded over time, so do NOT memorize SnapStart as:

**A Java-only feature**

for current architecture decisions.

### SAA Exam Principle

The important concept is:

> **SnapStart reduces initialization latency for supported Lambda runtimes by restoring pre-initialized snapshots.**

---

# SnapStart vs Provisioned Concurrency

This is the most important comparison.

Both can help with:

**Lambda startup latency**

but they work differently.

---

## SnapStart

Think:

**Snapshot initialized environment**

New environments can:

**Restore from the snapshot**

Primary goal:

**Reduce cold-start initialization time**

---

## Provisioned Concurrency

Think:

**Keep execution environments already initialized and ready**

Architecture:

Provisioned Environment  
↓  
Already Warm  
↓  
Immediate Invocation

Primary goal:

**Predictable low latency**

---

# SnapStart vs Provisioned Concurrency

| Feature | SnapStart | Provisioned Concurrency |
|---|---:|---:|
| Helps Cold Starts | ✅ | ✅ |
| Uses Snapshot Restore | ✅ | ❌ |
| Keeps Environments Pre-Warmed | ❌ | ✅ |
| Requires Published Version | ✅ | Typically Version / Alias Configuration |
| Primary Goal | Faster Initialization | Predictable Low Latency |
| Additional Provisioned Capacity | ❌ | ✅ |

### Memory Trick

**SNAPSTART = RESTORE FAST**

**PROVISIONED = ALREADY READY**

---

# SnapStart vs Reserved Concurrency

These solve:

**Completely different problems**

### SnapStart

Controls:

**Startup performance**

### Reserved Concurrency

Controls:

**Concurrency capacity**

and:

**Maximum function concurrency**

### Killer Distinction

**Cold start problem**
→ SnapStart / Provisioned Concurrency

**Scaling limit problem**
→ Reserved Concurrency

---

# SnapStart Does Not Reserve Capacity

Enabling SnapStart does NOT:

- Reserve concurrency
- Guarantee concurrency
- Limit maximum concurrency
- Protect downstream databases

For those requirements:

Think:

**Reserved Concurrency**

---

# SnapStart Does Not Mean Always Warm

This is an important exam trap.

SnapStart does NOT mean:

**The execution environment is permanently running**

Instead:

Lambda can create new environments by:

**Restoring a pre-initialized snapshot**

### Memory Trick

**Provisioned = Warm**

**SnapStart = Fast Restore**

---

# Initialization Code

Lambda code placed outside the handler often runs during:

**Initialization**

Example concept:

Initialize SDK Client  
Load Framework  
Read Static Configuration  
↓  
Handler

With SnapStart:

This initialized state can become part of:

**The snapshot**

---

# Snapshot State Considerations

Because SnapStart captures:

**Initialized execution state**

applications must be careful with values that should be:

**Unique after restoration**

Examples can include:

- Random values
- Unique identifiers
- Network connections
- Temporary credentials
- Time-sensitive state

The application may need to:

**Re-establish or regenerate certain state after restoration**

---

# Unique State

Imagine initialization creates:

`unique_id = random()`

Then Lambda snapshots:

**That initialized state**

If restored environments reuse inappropriate initialization state:

The application could behave incorrectly.

### SAA Principle

> **Snapshot-based initialization requires awareness of state that must remain unique or fresh**

---

# Network Connections

Connections created during initialization may not remain valid forever after:

**Snapshot restoration**

Applications should use:

**Resilient connection logic**

and reconnect when necessary.

This is especially important for:

- Databases
- External APIs
- Network sockets

---

# Temporary Credentials

Applications should not assume credentials captured during initialization remain:

**Valid indefinitely**

AWS SDKs and supported integrations generally manage credentials appropriately, but custom code should avoid treating:

**Snapshot-time credentials as permanent**

---

# SnapStart and Function Versions

Suppose:

Version 4  
→ SnapStart Enabled

You modify code in:

`$LATEST`

Version 4 does NOT change.

To use the new code with SnapStart:

Update Function  
↓  
Publish New Version  
↓  
New Snapshot

### Memory Trick

**NEW CODE → NEW VERSION → NEW SNAPSHOT**

---

# SnapStart and Deployment

Deployment pattern:

Code Update  
↓  
Configure SnapStart  
↓  
Publish Version  
↓  
Snapshot Optimization  
↓  
Alias Points to Version  
↓  
Production Traffic

This fits naturally with:

**Versioned Lambda deployments**

---

# SnapStart and Cost Thinking

SnapStart can reduce startup latency without requiring you to maintain:

**A fixed number of pre-initialized environments**

like Provisioned Concurrency.

However:

Architecture decisions should still consider:

- Runtime support
- Workload characteristics
- Pricing
- Latency requirements

### Exam Thinking

If the question specifically emphasizes:

**Pre-initialized capacity ready for predictable latency**

think:

**Provisioned Concurrency**

If it emphasizes:

**Faster initialization through snapshot/restore**

think:

**SnapStart**

---

# SnapStart + API Gateway

Architecture:

Client  
↓  
[[API Gateway]]  
↓  
SnapStart-Enabled Lambda  
↓  
Backend

This can help reduce:

**Cold-start latency**

for supported Lambda functions behind:

**Interactive APIs**

---

# SnapStart + Event-Driven Workloads

SnapStart is not limited to:

**API Gateway**

It can help supported Lambda workloads where:

**Initialization latency matters**

The key issue is:

**Function initialization**

not:

**Which event source invoked it**

---

# SnapStart Does Not Replace SQS

SnapStart improves:

**Startup performance**

[[SQS]] provides:

**Message buffering and decoupling**

Completely different problems.

---

# SnapStart Does Not Replace RDS Proxy

SnapStart:

**Reduces initialization latency**

[[RDS Proxy]]:

**Pools and manages database connections**

If Lambda connects to RDS:

You may potentially need:

**Both types of optimization**

depending on the problem.

---

# SnapStart Does Not Replace Lambda Layers

SnapStart:

**Optimizes initialization**

[[Lambda Layers]]:

**Package shared code and dependencies**

A large dependency may contribute to initialization time, but Layers themselves are not:

**A cold-start elimination mechanism**

---

# Architecture Thinking

## Scenario 1 — Initialization Latency

A supported Lambda runtime has:

**Heavy initialization**

and cold starts are causing latency.

The question specifically mentions:

**Snapshotting initialized execution state**

Choose:

**Lambda SnapStart**

---

## Scenario 2 — Predictable Low Latency

A financial API requires:

**Consistently low startup latency**

and the company wants:

**Execution environments already initialized before requests arrive**

Choose:

**Provisioned Concurrency**

---

## Scenario 3 — Protect Database

Lambda scales too quickly and overwhelms:

RDS.

Do NOT choose:

SnapStart.

Choose:

**Reserved Concurrency**

and potentially:

[[RDS Proxy]]

---

## Scenario 4 — Shared Dependency

Multiple functions use:

**The same library**

Do NOT choose:

SnapStart.

Choose:

[[Lambda Layers]]

---

## Scenario 5 — Queue Backlog

Need to buffer:

**Thousands of requests**

Do NOT choose:

SnapStart.

Choose:

[[SQS]]

---

## Scenario 6 — New Function Code

SnapStart-enabled Version 3 is deployed.

Developer modifies:

`$LATEST`

Need production to use new code.

Process:

Publish New Version  
↓  
New SnapStart Snapshot  
↓  
Update Alias

---

## Scenario 7 — Random Initialization State

Function generates:

**Unique state during initialization**

SnapStart restores initialized snapshots.

Developer should ensure:

**State requiring uniqueness is safely regenerated after restore**

---

# Scenario Recognition

Immediately think:

**Lambda SnapStart**

when you see:

- Cold-start reduction
- Snapshot initialized environment
- Restore execution environment
- Heavy function initialization
- Faster startup through snapshotting
- Published Lambda version
- Supported runtime startup optimization

---

## Think Provisioned Concurrency When You See

- Pre-warmed environments
- Already initialized capacity
- Predictable low latency
- Critical interactive workload

---

## Think Reserved Concurrency When You See

- Limit Lambda scaling
- Guarantee concurrency
- Protect downstream system
- Maximum simultaneous executions

---

# Exam Traps

## Trap 1 — SnapStart Reserves Lambda Concurrency

❌

Use:

**Reserved Concurrency**

---

## Trap 2 — SnapStart Keeps Environments Permanently Warm

❌

It uses:

**Snapshot restoration**

---

## Trap 3 — SnapStart and Provisioned Concurrency Are Identical

❌

SnapStart:

**Restore pre-initialized snapshot**

Provisioned Concurrency:

**Maintain initialized environments**

---

## Trap 4 — SnapStart Is Only Relevant to `$LATEST`

❌

Think:

**Published Versions**

---

## Trap 5 — SnapStart Eliminates Every Source of Lambda Latency

❌

It primarily targets:

**Initialization / cold-start latency**

The function can still be slow because of:

- Database calls
- API calls
- Inefficient code
- Network latency

---

## Trap 6 — SnapStart Protects RDS from Too Many Connections

❌

Think:

- Reserved Concurrency
- RDS Proxy

---

## Trap 7 — SnapStart Replaces Lambda Layers

❌

Layers:

**Dependency packaging**

SnapStart:

**Initialization optimization**

---

## Trap 8 — SnapStart Means Snapshot State Never Needs Validation

❌

Applications must consider:

**Freshness and uniqueness after restoration**

---

# Quick Cheat Sheet

| Exam Clue | Answer |
|---|---|
| Snapshot Initialized Lambda | SnapStart |
| Restore Instead of Full Initialization | SnapStart |
| Reduce Cold-Start Initialization | SnapStart |
| Pre-Warmed Environments | Provisioned Concurrency |
| Predictable Low Latency | Provisioned Concurrency |
| Limit Maximum Executions | Reserved Concurrency |
| Protect RDS | Reserved Concurrency / RDS Proxy |
| Shared Dependencies | Lambda Layers |
| Buffer Work | SQS |
| SnapStart Deployment Unit | Published Version |
| New Code | Publish New Version / Snapshot |

---

# Cold-Start Decision Table

| Requirement | Best Match |
|---|---|
| Faster Snapshot-Based Startup | SnapStart |
| Pre-Initialized Capacity | Provisioned Concurrency |
| Maximum Concurrency Control | Reserved Concurrency |
| Shared Libraries | Lambda Layers |
| Database Connection Pooling | RDS Proxy |

---

# SnapStart vs Provisioned vs Reserved

| Feature | SnapStart | Provisioned | Reserved |
|---|---:|---:|---:|
| Cold-Start Optimization | ✅ | ✅ | ❌ |
| Snapshot Restore | ✅ | ❌ | ❌ |
| Pre-Warmed Capacity | ❌ | ✅ | ❌ |
| Max Concurrency Control | ❌ | ❌ | ✅ |
| Capacity Reservation | ❌ | ❌ | ✅ |
| Protect Downstream Scale | ❌ | ❌ | ✅ |

---

# Final Exam Rapid-Fire

> **SNAPSHOT + RESTORE**
> → SNAPSTART
>
> **HEAVY INITIALIZATION**
> → SNAPSTART
>
> **REDUCE COLD-START INITIALIZATION**
> → SNAPSTART
>
> **ALREADY-WARM ENVIRONMENTS**
> → PROVISIONED CONCURRENCY
>
> **PREDICTABLE LOW LATENCY**
> → PROVISIONED CONCURRENCY
>
> **LIMIT SCALE**
> → RESERVED CONCURRENCY
>
> **PROTECT DATABASE**
> → RESERVED CONCURRENCY
>
> **POOL DB CONNECTIONS**
> → RDS PROXY
>
> **SHARED CODE**
> → LAMBDA LAYERS
>
> **SNAPSTART VERSION**
> → PUBLISHED VERSION
>
> **NEW CODE**
> → NEW VERSION + NEW SNAPSHOT

---

## Master Memory Trick

> [!tip] Lambda SnapStart Master Memory Trick
> Imagine starting a huge video game.
>
> Normally:
>
> **Start Game**
> → Load Everything
> → Initialize Everything
> → Finally Play
>
> That's:
>
> **COLD START**
>
> Now imagine saving the game immediately after everything finishes loading:
>
> **SNAPSHOT**
>
> Next time:
>
> **Restore Save**
> → Start Playing
>
> That's:
>
> **SNAPSTART**

But:

> **Provisioned Concurrency**
>
> is like leaving the game:
>
> **Already running**
>
> waiting for you.

So remember:

> **SNAPSTART**
> → Snapshot + Restore
>
> **PROVISIONED**
> → Already Ready
>
> **RESERVED**
> → Limit / Reserve Capacity
>
> **LAYERS**
> → Shared Dependencies
>
> **RDS PROXY**
> → Database Connections

And the killer SAA question:

> **"Does the architecture restore an initialized Lambda snapshot, or keep environments already running?"**
>
> **Restore Snapshot**
> → SnapStart
>
> **Already Running**
> → Provisioned Concurrency

---

## Related Notes

- [[Lambda]]
- [[Lambda Concurrency]]
- [[Lambda Layers]]
- [[Lambda Environment Variables]]
- [[Lambda Execution Roles]]
- [[API Gateway]]
- [[SQS]]
- [[RDS]]
- [[RDS Proxy]]