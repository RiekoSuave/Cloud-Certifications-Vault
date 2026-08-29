## Core Concept

A major SAA architecture decision is whether application servers are:

**Stateless**

or:

**Stateful**

The exam strongly favors:

**Stateless application tiers whenever practical**

because stateless systems are easier to:

- Scale
- Replace
- Load balance
- Recover
- Deploy across Availability Zones
- Deploy across Regions

> [!tip] Memory Trick
> **Stateless = Any Server Can Handle Any Request**

---

# What Is Stateless?

A stateless application server does NOT depend on:

**Locally stored user/session information**

between requests.

Example:

User Request  
↓  
Load Balancer  
↓  
EC2 A

Next Request  
↓  
Load Balancer  
↓  
EC2 B

The application still works because:

**The state lives somewhere shared**

### Killer Exam Clue

> **Instances must scale horizontally and be replaceable without losing user sessions**
>
> → **Use a stateless application tier**

---

# What Is State?

State is information that must persist between:

**Requests or interactions**

Examples:

- User session
- Shopping cart
- Authentication state
- Workflow progress
- Application data

The problem is not that state exists.

The problem is:

**Where the state is stored**

---

# Stateful Application Server

A stateful server stores important state:

**Locally**

Example:

User  
↓  
EC2 A  
↓  
Session stored on EC2 A

If the user's next request goes to:

EC2 B

EC2 B may not know:

**The user's session**

### Memory Trick

**Stateful = User Gets Attached to a Server**

---

# The Scaling Problem

Suppose an application stores sessions locally.

Architecture:

ALB  
↓  
├── EC2 A — Session 1
├── EC2 B — Session 2
└── EC2 C — Session 3

Now:

EC2 A fails.

The users whose sessions were stored there may:

**Lose session state**

### Killer Exam Principle

> **Local server state makes horizontal scaling and failover harder**

---

# Externalize State

A better architecture moves state into:

**Shared durable services**

Architecture:

Users  
↓  
[[Application Load Balancer]]  
↓  
Stateless EC2 Fleet  
↓  
Shared State Store

Possible shared stores include:

- [[ElastiCache]]
- [[DynamoDB]]
- [[RDS]]
- [[Aurora]]
- [[S3]]

### Memory Trick

> **Compute Can Die**
>
> **State Must Survive**

---

# Session State in ElastiCache

[[ElastiCache]] can store:

**Fast in-memory session state**

Architecture:

ALB  
↓  
EC2 Fleet  
↓  
ElastiCache

Any EC2 instance can retrieve:

**The same session**

### Killer Exam Clue

> **Need fast shared user-session storage across Auto Scaling instances**
>
> → **ElastiCache**

---

# Session State in DynamoDB

[[DynamoDB]] can also store:

**Shared application/session state**

Advantages include:

- Managed scaling
- High availability
- Serverless operation
- Durable storage

### Killer Exam Clue

> **Need highly scalable shared session state without managing servers**
>
> → **DynamoDB**

---

# ElastiCache vs DynamoDB for Sessions

## ElastiCache

Think:

- Very low latency
- In-memory
- Fast session/cache access

## DynamoDB

Think:

- Durable
- Serverless
- Massive scale
- Persistent key-value state

### Killer Shortcut

**Ultra-fast temporary session/cache**
→ ElastiCache

**Durable serverless session/state**
→ DynamoDB

---

# Local Files Are State

An application may also become stateful by storing:

**Uploaded files locally on EC2**

Example:

User Upload  
↓  
EC2 A  
↓  
Local Disk

Another instance cannot automatically access:

**That file**

### Better Pattern

User Upload  
↓  
Application  
↓  
[[S3]]

Now every application instance can access:

**The shared object**

---

# S3 for Shared Objects

[[S3]] is ideal for:

- Images
- Documents
- Videos
- Static assets
- User uploads

because these objects should not depend on:

**One EC2 instance's local disk**

### Killer Exam Clue

> **Users upload files to Auto Scaling EC2 instances and uploads must survive instance replacement**
>
> → Store uploads in **S3**

---

# EFS for Shared Files

[[EFS]] provides:

**Shared file storage**

that multiple Linux EC2 instances can mount.

Architecture:

EC2 A  
↘  
[[EFS]]

EC2 B  
↗

Use when applications specifically require:

**A shared filesystem**

### Killer Exam Clue

> **Multiple Linux EC2 instances require access to the same POSIX-style files**
>
> → **EFS**

---

# S3 vs EFS

## S3

Think:

**Object storage**

Best when applications can interact through:

**Object APIs**

## EFS

Think:

**Shared filesystem**

Best when applications require:

**Mounted file semantics**

### Memory Trick

**S3 = Objects**

**EFS = Filesystem**

---

# EBS and Stateful Compute

[[EBS]] provides:

**Block storage**

commonly attached to EC2.

EBS can preserve data beyond an instance's lifetime depending on:

**Configuration**

but an EBS-backed architecture can still create tighter coupling between:

**Compute and storage**

### Exam Principle

> **Do not assume EBS automatically makes an application horizontally stateless**

---

# Databases Are Stateful

Databases are naturally:

**Stateful systems**

because they store:

**Persistent application data**

That is fine.

The key architecture goal is usually:

**Keep the application tier stateless while placing state in managed data services**

### Killer Pattern

Stateless App Tier  
↓  
Stateful Managed Data Tier

---

# Stateless + Auto Scaling

Stateless design works extremely well with:

[[Auto Scaling]]

Because instances do not contain unique user state:

New instances can be:

**Added at any time**

Old/unhealthy instances can be:

**Removed at any time**

### Memory Trick

**Stateless = Disposable Compute**

---

# Disposable Compute

A strong cloud architecture treats application instances as:

**Replaceable**

If an instance fails:

Auto Scaling  
↓  
Launch Replacement  
↓  
Application Continues

No manual restoration of:

**Local session state**

should be necessary.

---

# Stateless + Load Balancer

With stateless servers:

[[Application Load Balancer]]

can distribute requests freely across:

**Healthy targets**

There is no need for a user to always return to:

**The same instance**

### Killer Exam Principle

> **Stateless architecture reduces dependence on sticky sessions**

---

# Sticky Sessions

Load balancer stickiness can send a user repeatedly to:

**The same backend target**

This can help when an application is:

**Stateful**

However:

**It does not remove the underlying architectural coupling**

### Exam Trap

> Sticky sessions can mask local-session architecture problems, but they are not the same as truly stateless design.

---

# Sticky Sessions Failure Problem

Suppose:

User  
↓  
Sticky Session  
↓  
EC2 A

If EC2 A fails:

The user can still lose:

**Locally stored session state**

Therefore:

**Stickiness is not a substitute for externalizing critical state**

---

# Stateless Architecture + Multi-AZ

Stateless compute can easily run across:

**Multiple Availability Zones**

Architecture:

ALB  
↓  
EC2 — AZ A  
EC2 — AZ B  
↓  
Shared Data Layer

If one AZ fails:

Traffic continues through:

**The surviving application tier**

### Killer Exam Clue

> **Need application tier to survive AZ failure and scale horizontally**
>
> → Stateless compute across multiple AZs

---

# Stateless Architecture + Multi-Region

Stateless applications are also easier to deploy across:

**Multiple Regions**

because application servers do not depend on:

**Local server-specific state**

The challenge becomes:

**Replicating the shared state/data layer appropriately**

---

# Authentication State

Authentication should generally not depend on:

**Local application-server memory**

Better patterns may use:

- [[Cognito]]
- Signed tokens
- Shared session stores

### Exam Principle

> **Authentication architecture should support backend replacement and scaling**

---

# Cookies

A cookie may store:

**A session identifier**

while the actual session state resides in:

**A shared backend store**

Architecture:

Browser Cookie  
↓  
Session ID  
↓  
Any App Server  
↓  
Shared Session Store

This remains compatible with:

**Stateless application servers**

---

# Token-Based Authentication

Token-based authentication can further reduce:

**Server-side session dependence**

The application validates:

**The token**

rather than requiring local session memory.

### Exam Principle

> **Token-based systems can simplify horizontally scaled architectures**

---

# Stateful Workloads

Not every workload can be made completely stateless.

Examples include:

- Databases
- Legacy applications
- Certain file-based systems
- Applications requiring local state

In those cases, architecture should provide:

**Appropriate replication, persistence, and failover**

---

# Managed Stateful Services

AWS provides managed services to handle difficult stateful components.

Examples:

[[RDS]]  
→ Relational database

[[Aurora]]  
→ Highly available relational database

[[DynamoDB]]  
→ Managed NoSQL

[[EFS]]  
→ Shared filesystem

[[ElastiCache]]  
→ In-memory state/cache

### Memory Trick

**Keep Compute Simple**

**Let Managed Services Hold State**

---

# Stateful vs Stateless Scaling

## Stateless

Scale out:

**Easily**

because every instance is equivalent.

## Stateful

Scale out:

**More carefully**

because data/state may require:

- Replication
- Synchronization
- Partitioning
- Session affinity

### Killer Exam Principle

> **State creates coordination**

---

# Stateful vs Stateless Failure Recovery

## Stateless Server Fails

Replace it.

## Stateful Server Fails

Potentially must recover:

- Local data
- Sessions
- Replication state
- Persistent storage

### Memory Trick

**Stateless Failure = Replace**

**Stateful Failure = Recover**

---

# Decoupling State From Compute

A strong AWS pattern:

Compute Layer  
↓  
Shared Cache / Database / Object Storage

This means:

**Compute lifecycle**

and:

**Data lifecycle**

are independent.

### Killer Exam Clue

> **Application instances should be replaced without affecting user data**
>
> → Separate compute from persistent state

---

# Immutable Infrastructure

Stateless design works well with:

**Immutable infrastructure**

Instead of fixing a running EC2 instance:

Old Instance  
↓  
Replace  
↓  
New Instance From AMI/Image

### Exam Principle

> **Replace infrastructure rather than manually repairing unique servers**

---

# Containers

Containerized architectures commonly benefit from:

**Stateless containers**

Containers can be:

- Started
- Stopped
- Rescheduled
- Replaced

while persistent state remains in:

**External services**

### Killer Exam Clue

> **Containers must be freely rescheduled across hosts**
>
> → Externalize persistent state

---

# Lambda

[[Lambda]] should generally be treated as:

**Stateless compute**

A Lambda execution environment may be reused, but applications should NOT rely on:

**Local memory or local filesystem state being permanently available**

### Killer Exam Trap

> **Do not design Lambda assuming the same execution environment handles the next invocation**

---

# Lambda Temporary Storage

Lambda can use temporary local storage during:

**An invocation/execution environment**

but persistent application state should be stored in:

- S3
- DynamoDB
- RDS/Aurora
- Other durable stores

### Memory Trick

**Lambda Memory Is Temporary**

---

# ECS and EKS

Containers running on:

[[ECS]]

or:

[[EKS]]

should ideally separate:

**Application compute**

from:

**Persistent storage**

Use appropriate storage such as:

- EFS
- EBS where supported/appropriate
- S3
- Databases

---

# Architecture Thinking

## Scenario 1 — Sessions Lost During Scaling

Auto Scaling removes EC2 instances and users:

**Lose sessions**

Cause:

Sessions stored:

**Locally**

Better:

Store sessions in:

**ElastiCache or DynamoDB**

---

## Scenario 2 — User Uploads

Users upload images to:

**EC2 local disk**

Images disappear when instances terminate.

Better:

**S3**

---

## Scenario 3 — Shared Linux Files

Several EC2 instances need:

**The same mounted directory**

Choose:

**EFS**

---

## Scenario 4 — Load Balancing

Application must distribute requests freely among:

**Any healthy EC2 instance**

Best architecture:

**Stateless application servers**

---

## Scenario 5 — Sticky Sessions

Application requires:

**Sticky sessions**

because user state lives on individual servers.

The exam asks for:

**A more scalable resilient redesign**

Choose:

**Externalize session state**

rather than relying solely on:

**Stickiness**

---

## Scenario 6 — Lambda

Developer stores critical state in:

`/tmp`

and expects it to exist on:

**Next invocation**

Bad design.

Use:

**Durable external storage**

---

## Scenario 7 — Multi-Region

Application tier must run in:

**Two Regions**

Keep compute:

**Stateless**

and design the data tier for:

**Cross-Region replication**

---

# Scenario Recognition

Immediately think:

**Stateless Architecture**

when you see:

- Auto Scaling
- Replaceable servers
- Horizontal scaling
- Load balancing
- Multi-AZ compute
- Multi-Region compute
- Containers
- Serverless

---

## Think ElastiCache When You See

- Fast session state
- Cache
- Repeated reads
- In-memory access

---

## Think DynamoDB When You See

- Durable shared state
- Massive scale
- Serverless key-value state

---

## Think S3 When You See

- User uploads
- Shared objects
- Static files
- Durable object storage

---

## Think EFS When You See

- Shared filesystem
- Multiple Linux EC2 instances
- Mounted POSIX storage

---

# Exam Traps

## Trap 1 — Stateless Means the Application Has No Data

❌

It means:

**Application servers do not keep critical unique state locally**

---

## Trap 2 — Sticky Sessions Make an Application Truly Stateless

❌

They can keep users attached to:

**One stateful server**

but the architecture remains:

**Stateful**

---

## Trap 3 — Local EC2 Disk Is Good Shared Session Storage

❌

Use:

**A shared state service**

---

## Trap 4 — S3 Is a Mounted POSIX Filesystem

❌

Think:

**EFS**

---

## Trap 5 — EFS Is Object Storage

❌

Think:

**S3**

---

## Trap 6 — Lambda Local State Is Durable

❌

Treat Lambda compute as:

**Ephemeral/stateless**

---

## Trap 7 — Databases Should Be Stateless

❌

Databases are intentionally:

**Stateful**

The application tier is what you often want:

**Stateless**

---

# Quick Cheat Sheet

| Exam Clue | Answer |
|---|---|
| Replaceable App Servers | Stateless |
| Easy Horizontal Scaling | Stateless |
| Local User Sessions | Stateful Problem |
| Fast Shared Sessions | ElastiCache |
| Durable Shared State | DynamoDB |
| User Uploads | S3 |
| Shared Linux Files | EFS |
| Database | Stateful Managed Service |
| Sticky Sessions | Statefulness Workaround |
| Auto Scaling Friendly | Stateless |
| Lambda Persistent State | External Store |
| Containers | Prefer Stateless |

---

# State Storage Decision Map

Need:

**Fast session/cache**

→ ElastiCache

Need:

**Durable key-value state**

→ DynamoDB

Need:

**Object/file uploads**

→ S3

Need:

**Shared mounted Linux filesystem**

→ EFS

Need:

**Relational persistent data**

→ RDS / Aurora

---

# Stateless Architecture Map

> **USERS**
> ↓
> LOAD BALANCER
> ↓
> STATELESS COMPUTE
>
> EC2 A
>
> EC2 B
>
> EC2 C
> ↓
> SHARED STATE
>
> ElastiCache / DynamoDB / RDS / S3 / EFS

### Core Rule

> **Any compute instance should be replaceable without losing important application state**

---

# Final Exam Rapid-Fire

> **AUTO SCALING APP TIER**
> → STATELESS
>
> **REPLACEABLE COMPUTE**
> → STATELESS
>
> **SESSION STORE**
> → ELASTICACHE / DYNAMODB
>
> **UPLOADS**
> → S3
>
> **SHARED FILESYSTEM**
> → EFS
>
> **RELATIONAL DATA**
> → RDS / AURORA
>
> **LOCAL SESSION**
> → STATEFUL COUPLING
>
> **STICKY SESSION**
> → WORKAROUND, NOT TRUE STATELESSNESS
>
> **LAMBDA**
> → TREAT AS STATELESS
>
> **CONTAINERS**
> → PREFER STATELESS

---

## Master Memory Trick

> [!tip] Stateless vs Stateful Master Memory Trick
> Imagine a fast-food restaurant chain.
>
> A stateless customer can walk into:
>
> **ANY LOCATION**
>
> and the employee can retrieve the order information from:
>
> **A SHARED SYSTEM**
>
> No single restaurant owns:
>
> **THE CUSTOMER'S STATE**
>
> That's:
>
> **STATELESS COMPUTE**
>
> Now imagine the customer's entire order is written on:
>
> **A NOTE STUCK TO ONE CASH REGISTER**
>
> If that register breaks:
>
> **THE STATE IS GONE**
>
> That's:
>
> **STATEFUL COMPUTE**

So remember:

> **STATELESS**
> → ANY SERVER
>
> **STATEFUL**
> → SPECIFIC SERVER
>
> **ELASTICACHE**
> → FAST SESSION
>
> **DYNAMODB**
> → DURABLE STATE
>
> **S3**
> → OBJECTS
>
> **EFS**
> → SHARED FILES
>
> **RDS / AURORA**
> → RELATIONAL STATE
>
> **AUTO SCALING**
> → LOVES STATELESS COMPUTE

And the killer SAA question:

> **"Can this compute instance be terminated and replaced without losing important user or application state?"**
>
> YES
>
> → **Stateless architecture**
>
> NO
>
> → **Find a way to externalize the state**

---

## Related Notes

- [[Architecture Principles]]
- [[Application Load Balancer]]
- [[Auto Scaling]]
- [[ElastiCache]]
- [[DynamoDB]]
- [[RDS]]
- [[Aurora]]
- [[S3]]
- [[EFS]]
- [[Lambda]]
- [[ECS]]
- [[EKS]]