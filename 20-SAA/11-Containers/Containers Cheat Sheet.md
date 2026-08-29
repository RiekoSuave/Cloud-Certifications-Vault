## Core Container Services

| Service | Main Purpose | Killer Exam Clue |
|---|---|---|
| [[ECS]] | AWS-native container orchestration | Run/manage containers on AWS |
| [[EKS]] | Managed Kubernetes | Kubernetes required |
| [[ECR]] | Container image registry | Store container images |
| [[Fargate]] | Serverless container compute | No EC2/server management |
| [[App Runner]] | Managed web app/API deployment | Code/image → web service |
| [[App2Container]] | Application containerization | Existing app → container |

> [!tip] Master Container Memory Trick
> **APP2CONTAINER = CONVERT**
>
> **ECR = STORE**
>
> **ECS = ORCHESTRATE**
>
> **EKS = KUBERNETES**
>
> **FARGATE = SERVERLESS COMPUTE**
>
> **APP RUNNER = SIMPLE WEB DEPLOYMENT**

---

## Container Architecture Flow

Traditional Application  
↓  
[[App2Container]]  
↓  
Container Image  
↓  
[[ECR]]  
↓  
[[ECS]] / [[EKS]]  
↓  
EC2 / [[Fargate]]  
↓  
Running Application

---

# ECS

[[ECS]] is AWS's:

**Native container orchestration service**

Think:

> **AWS-native container management**

ECS manages:

- Tasks
- Services
- Deployments
- Container placement
- Scaling

### Killer Exam Clue

> **Run and orchestrate containers on AWS without requiring Kubernetes**
>
> → **ECS**

---

## ECS Task Definition

A:

**Task Definition**

is the:

**Blueprint for running containers**

It defines things such as:

- Container image
- CPU
- Memory
- Ports
- Environment configuration
- IAM roles
- Logging
- Volumes

### Memory Trick

**Task Definition = Recipe**

**Task = Running Meal**

---

## ECS Task

A:

**Task**

is:

**A running instance of a Task Definition**

Use standalone tasks for:

- One-time processing
- Batch jobs
- Scheduled jobs
- Event-driven jobs

### Killer Shortcut

**RUN AND FINISH**
→ ECS Task

---

## ECS Service

An:

**ECS Service**

maintains:

**A desired number of tasks**

Use for:

- Web applications
- APIs
- Long-running workers
- Microservices

### Killer Shortcut

**KEEP RUNNING**
→ ECS Service

---

# ECS Launch Options

ECS workloads commonly run on:

- EC2
- Fargate

---

## ECS on EC2

You manage:

- EC2 instances
- Host patching
- Cluster capacity
- Instance types
- Auto Scaling

Choose when:

**Host control matters**

### Killer Clues

- Specific instance type
- GPU
- Custom AMI
- Host-level configuration

→ **ECS on EC2**

---

## ECS on Fargate

AWS manages:

**Underlying servers**

You manage:

- Tasks
- Services
- CPU
- Memory
- Application configuration

### Killer Clue

> **Run ECS containers without managing EC2 instances**
>
> → **Fargate**

---

# ECS EC2 vs Fargate

| Requirement | ECS on EC2 | ECS on Fargate |
|---|---:|---:|
| Manage Hosts | ✅ | ❌ |
| Serverless | ❌ | ✅ |
| Host Control | ✅ | ❌ |
| Choose Instance Type | ✅ | ❌ |
| Minimum Operations | ❌ | ✅ |
| ECS Service Auto Scaling | ✅ | ✅ |

### Memory Trick

**EC2 = Manage Machines**

**Fargate = Manage Tasks**

---

# ECS IAM Roles

This distinction is extremely important.

## Task Role

Used by:

**Application code**

Examples:

ECS App  
→ S3

ECS App  
→ DynamoDB

ECS App  
→ SQS

### Memory Trick

**TASK ROLE = APP**

---

## Task Execution Role

Used by:

**ECS during task startup**

Examples:

ECS  
→ Pull ECR image

ECS  
→ Send logs to CloudWatch

ECS  
→ Retrieve startup secret

### Memory Trick

**EXECUTION ROLE = START**

---

## EC2 Instance Role

Used by:

**Underlying ECS EC2 host**

Only relevant when using:

**ECS on EC2**

### Master IAM Trick

> **APP**
> → Task Role
>
> **START**
> → Execution Role
>
> **HOST**
> → Instance Role

---

# ECS IAM Quick Table

| Requirement | Role |
|---|---|
| App Reads S3 | Task Role |
| App Writes DynamoDB | Task Role |
| App Polls SQS | Task Role |
| App Calls Secrets Manager | Task Role |
| ECS Pulls ECR Image | Execution Role |
| ECS Sends Logs | Execution Role |
| ECS Injects Startup Secret | Execution Role |
| EC2 Host Permissions | Instance Role |

---

# ECS Auto Scaling

ECS Service Auto Scaling changes:

**Number of running tasks**

Possible metrics:

- CPU
- Memory
- ALB requests per target
- Custom CloudWatch metrics

Architecture:

Demand ↑  
↓  
Metric ↑  
↓  
ECS Service Auto Scaling  
↓  
More Tasks

### Memory Trick

**Service Scaling = Scale Tasks**

---

## ECS on EC2 Double Scaling

With ECS on EC2:

Application Demand ↑  
↓  
Need More Tasks  
↓  
Service Auto Scaling  
↓  
Need More Host Capacity?  
↓  
EC2 / Cluster Scaling  
↓  
More Instances

### Killer Exam Concept

> **Task scaling and EC2 capacity scaling are separate**

---

# ECS + ALB

Classic web architecture:

Users  
↓  
[[Application Load Balancer]]  
↓  
ECS Service  
↓  
Tasks

ALB is ideal for:

- HTTP
- HTTPS
- Host-based routing
- Path-based routing
- Microservices

### Killer Exam Pattern

> **Containerized HTTP/HTTPS web application**
>
> → **ALB + ECS Service**

---

# ECS Microservices

Example:

ALB  
↓  
`/orders` → Orders ECS Service

`/payments` → Payments ECS Service

`/users` → Users ECS Service

Think:

**ALB Path-Based Routing**

---

# ECS + SQS

Classic worker architecture:

Producer  
↓  
[[SQS]]  
↓  
ECS Worker Service  
↓  
Tasks

SQS provides:

**Buffering**

ECS provides:

**Workers**

### Memory Trick

**SQS = Work Waiting**

**ECS = Workers**

---

## Queue-Based Scaling

SQS Queue Depth ↑  
↓  
CloudWatch Metric  
↓  
ECS Service Auto Scaling  
↓  
More Workers

### Killer Exam Pattern

> **Scale container workers based on message backlog**
>
> → **SQS + ECS Auto Scaling**

---

# ECS + EventBridge

[[20-SAA/10-Messaging/EventBridge]] can trigger:

**ECS tasks**

Use for:

- Scheduled jobs
- Event-driven jobs
- One-time processing

Architecture:

Event / Schedule  
↓  
EventBridge  
↓  
ECS Task

### Killer Shortcut

**CLOCK / EVENT**
→ EventBridge + ECS Task

---

# ECS + EFS

Multiple tasks need:

**Shared persistent files**

Architecture:

ECS Task A  
↓  

ECS Task B  
↓  

[[EFS]]

### Killer Exam Clue

> **Multiple ECS tasks need shared persistent file storage**
>
> → **EFS**

---

# ECR

[[ECR]] is:

**AWS's managed container image registry**

It stores:

- Docker images
- OCI-compatible images
- Image tags
- Image metadata

### Killer Exam Clue

> **Store container images**
>
> → **ECR**

---

## ECR Important Features

Remember:

- Private repositories
- Public repositories
- IAM integration
- Image scanning
- Lifecycle policies
- Tag immutability
- Cross-Region replication
- Cross-account access

---

## ECR Image Scanning

Need:

**Container vulnerability detection**

→ ECR Image Scanning

### Killer Shortcut

**IMAGE VULNERABILITIES**
→ ECR SCANNING

---

## ECR Lifecycle Policies

Need:

**Automatic cleanup of old images**

→ Lifecycle Policy

### Killer Shortcut

**OLD IMAGES**
→ LIFECYCLE POLICY

---

## ECR Tag Immutability

Need:

**Prevent image tags from being overwritten**

→ Tag Immutability

### Memory Trick

**IMMUTABLE = TAG CANNOT MOVE**

---

# Fargate

[[Fargate]] is:

**Serverless compute for containers**

Works with:

- ECS
- EKS

Fargate does NOT:

**Orchestrate containers**

Instead it provides:

**Compute**

### Memory Trick

**ECS / EKS = Brain**

**Fargate = Muscle**

---

## Fargate Best Clues

Immediately think Fargate when you see:

- Serverless containers
- No EC2 management
- No host patching
- Minimum infrastructure management
- Task-level CPU/memory

---

# Fargate Spot

Fargate Spot provides:

**Lower-cost interruptible container compute**

Good for:

- SQS workers
- Batch jobs
- Fault-tolerant workloads
- Background processing

Bad for:

**Critical non-interruptible workloads**

### Memory Trick

**Fargate Spot = Cheap + Interruptible**

---

# Capacity Providers

ECS Capacity Providers help determine:

**Where ECS tasks run**

Examples:

- Fargate
- Fargate Spot
- EC2 capacity

A strategy can use:

- Base
- Weight

### Memory Trick

**BASE = Minimum**

**WEIGHT = Distribution Ratio**

---

# EKS

[[EKS]] is:

**Managed Kubernetes on AWS**

AWS manages:

**Kubernetes control plane**

You choose:

**Worker compute**

### Killer Exam Clue

> **Kubernetes required**
>
> → **EKS**

---

# EKS Worker Options

Main options:

- Self-Managed EC2 Nodes
- Managed Node Groups
- Fargate

---

## Self-Managed Nodes

Choose when:

**Maximum host control**

is required.

Think:

- Custom AMI
- Custom configuration
- Full lifecycle control

### Shortcut

**MAX CONTROL**
→ Self-Managed

---

## Managed Node Groups

Choose when:

**EC2 workers are needed but AWS should simplify node management**

### Shortcut

**EC2 + LESS MANAGEMENT**
→ Managed Node Group

---

## EKS + Fargate

Choose when:

**Kubernetes is required without worker-node management**

### Shortcut

**KUBERNETES + SERVERLESS**
→ EKS + Fargate

---

# EKS Node Type Comparison

| Requirement | Self-Managed | Managed Node Group | Fargate |
|---|---:|---:|---:|
| EC2 Nodes | ✅ | ✅ | ❌ |
| Maximum Host Control | ✅ | Partial | ❌ |
| AWS Helps Node Lifecycle | ❌ | ✅ | N/A |
| Serverless | ❌ | ❌ | ✅ |
| GPU / Specialized Hardware | ✅ | ✅ | Limited |
| Minimum Infrastructure Ops | ❌ | Better | ✅ |

---

# EKS Scaling

Remember two layers:

### Pod Scaling

Changes:

**Number of pods**

Think:

**Horizontal Pod Autoscaler**

### Node Scaling

Changes:

**EC2 worker capacity**

### Memory Trick

**PODS = APP CAPACITY**

**NODES = INFRASTRUCTURE CAPACITY**

---

# EKS Data Volumes

The big storage decision:

**Block vs Shared File**

---

## EBS

[[EBS]]

Think:

- Block storage
- Persistent disk
- One AZ
- Stateful workloads

### Killer Shortcut

**BLOCK + ONE AZ**
→ EBS

---

## EFS

[[EFS]]

Think:

- NFS
- Shared files
- Multiple pods
- Multi-AZ

### Killer Shortcut

**SHARED FILES + MULTI-AZ**
→ EFS

---

## FSx

[[FSx]]

Think:

**Specialized file systems**

Examples:

[[FSx for Lustre]]

→ HPC / high-performance parallel filesystem

[[FSx for NetApp ONTAP]]

→ NetApp / multiprotocol

[[FSx for OpenZFS]]

→ ZFS workloads

---

# Kubernetes Storage Concepts

### PV

PersistentVolume

→ Actual persistent storage

### PVC

PersistentVolumeClaim

→ Request for storage

### StorageClass

→ Defines how storage is provisioned

### CSI Driver

→ Connects Kubernetes to storage provider

### Memory Trick

> **POD ASKS**
> → PVC
>
> **STORAGE EXISTS**
> → PV
>
> **HOW TO CREATE**
> → StorageClass
>
> **AWS CONNECTION**
> → CSI Driver

---

# App Runner

[[App Runner]] is a:

**Fully managed web application/API service**

You provide:

- Source code
- Container image

AWS handles much of:

- Deployment
- Compute
- Scaling
- Load balancing
- HTTPS

### Killer Exam Clue

> **Deploy a web app/API with minimal infrastructure management**
>
> → **App Runner**

---

# App Runner vs ECS + Fargate

### App Runner

Think:

**Simplicity**

### ECS + Fargate

Think:

**More container control**

### Shortcut

**JUST RUN MY WEB APP**
→ App Runner

**I NEED CONTAINER ORCHESTRATION CONTROL**
→ ECS + Fargate

---

# App Runner vs Lambda

### App Runner

→ Long-running web service/API

### [[02-Compute/Lambda]]

→ Event-driven function

### Shortcut

**WEB SERVICE**
→ App Runner

**FUNCTION**
→ Lambda

---

# App2Container

[[App2Container]] helps:

**Convert existing applications into containers**

Think:

Existing Java / .NET Application  
↓  
App2Container  
↓  
Container Image  
↓  
ECR  
↓  
ECS / EKS

### Killer Exam Clue

> **Modernize existing server application into containers**
>
> → **App2Container**

---

# App2Container vs Application Migration Service

### App2Container

**Modernize application**

Server App  
→ Container

### Application Migration Service

**Rehost server**

Server  
→ AWS Server

### Memory Trick

**APP2CONTAINER = MODERNIZE**

**MIGRATION SERVICE = LIFT & SHIFT**

---

# Container Service Decision Tree

Need containers?  
↓

Already have container image?

No, existing traditional application  
→ **App2Container**

Yes  
↓

Need Kubernetes?

Yes  
→ **EKS**

No  
↓

Need detailed AWS-native container orchestration?

Yes  
→ **ECS**

No  
↓

Simple web application/API?

Yes  
→ **App Runner**

---

## Compute Decision

Using ECS/EKS?  
↓

Need host control?

Yes  
→ **EC2**

No  
↓

Want serverless compute?

Yes  
→ **Fargate**

---

# Storage Decision

Container needs persistent data?  
↓

Block storage?

→ **EBS**

Shared files?

→ **EFS**

Object storage?

→ **S3**

Specialized filesystem?

→ **FSx**

---

# IAM Decision

ECS application needs AWS API?

→ **Task Role**

ECS needs image/startup/logging permissions?

→ **Task Execution Role**

EC2 host needs infrastructure permissions?

→ **Instance Role**

---

# High-Value Architecture Patterns

## Web Application

Internet  
↓  
ALB  
↓  
ECS Service  
↓  
Fargate Tasks

Think:

**Highly available serverless container web app**

---

## Async Workers

Producer  
↓  
SQS  
↓  
ECS Service  
↓  
Fargate Workers

Think:

**Decoupled asynchronous processing**

---

## Scheduled Job

EventBridge  
↓  
ECS Task  
↓  
Fargate

Think:

**Container runs on schedule and exits**

---

## Kubernetes

ECR  
↓  
EKS  
↓  
Managed Nodes / Fargate  
↓  
Pods

Think:

**Managed Kubernetes**

---

## Modernization

Existing App  
↓  
App2Container  
↓  
ECR  
↓  
ECS / EKS

Think:

**Server app → container**

---

## Simple Web Deployment

Source / ECR  
↓  
App Runner  
↓  
HTTPS Web Service

Think:

**Minimal infrastructure management**

---

# Killer Exam Traps

## Trap 1 — ECR Runs Containers

❌

ECR:

**Stores images**

---

## Trap 2 — Fargate Is an Orchestrator

❌

Fargate:

**Provides compute**

---

## Trap 3 — EKS Is Automatically Serverless

❌

EKS can use:

- EC2
- Fargate

---

## Trap 4 — ECS Requires EC2

❌

ECS can use:

**Fargate**

---

## Trap 5 — Managed Node Groups Are Serverless

❌

They use:

**EC2**

---

## Trap 6 — Task Role Pulls ECR Images

❌

Think:

**Execution Role**

---

## Trap 7 — Execution Role Gives App S3 Access

❌

Think:

**Task Role**

---

## Trap 8 — EBS Is Multi-AZ Shared Storage

❌

EBS:

**One AZ**

EFS:

**Shared Multi-AZ**

---

## Trap 9 — Fargate Spot Is Guaranteed

❌

It is:

**Interruptible**

---

## Trap 10 — App2Container Runs Production Containers

❌

It:

**Containerizes applications**

---

## Trap 11 — App Runner Is Kubernetes

❌

Kubernetes:

**EKS**

---

## Trap 12 — Pod Scaling Automatically Adds EC2 Nodes

❌

Pod scaling and node scaling are:

**Separate**

---

# Master Comparison Table

| Requirement | Service / Feature |
|---|---|
| AWS Container Orchestration | ECS |
| Kubernetes | EKS |
| Store Container Images | ECR |
| Serverless Container Compute | Fargate |
| Simple Managed Web App/API | App Runner |
| Existing App → Container | App2Container |
| Host Control | EC2 |
| Serverless Kubernetes | EKS + Fargate |
| Managed EC2 Kubernetes Workers | Managed Node Groups |
| Shared Container Files | EFS |
| Block Storage | EBS |
| Specialized Filesystem | FSx |
| ECS App AWS Access | Task Role |
| ECS Startup Permissions | Execution Role |
| Async Workers | SQS + ECS |
| Scheduled Container Job | EventBridge + ECS Task |
| HTTP Container Routing | ALB |
| Container Vulnerability Scan | ECR Image Scanning |
| Delete Old Images | ECR Lifecycle Policy |

---

# Final Exam Rapid-Fire

> **AWS-NATIVE CONTAINERS**
> → ECS
>
> **KUBERNETES**
> → EKS
>
> **IMAGE REGISTRY**
> → ECR
>
> **NO SERVER MANAGEMENT**
> → FARGATE
>
> **SIMPLE WEB APP/API**
> → APP RUNNER
>
> **EXISTING APP → CONTAINER**
> → APP2CONTAINER
>
> **APP NEEDS AWS ACCESS**
> → TASK ROLE
>
> **ECS NEEDS ECR IMAGE**
> → EXECUTION ROLE
>
> **WEB TRAFFIC**
> → ALB + ECS
>
> **ASYNC WORKERS**
> → SQS + ECS
>
> **SCHEDULED CONTAINER**
> → EVENTBRIDGE + ECS TASK
>
> **SHARED FILES**
> → EFS
>
> **BLOCK DISK**
> → EBS
>
> **HPC FILESYSTEM**
> → FSx FOR LUSTRE
>
> **SERVERLESS KUBERNETES**
> → EKS + FARGATE
>
> **EC2 KUBERNETES + LESS MANAGEMENT**
> → MANAGED NODE GROUP
>
> **CHEAP INTERRUPTIBLE CONTAINERS**
> → FARGATE SPOT
>
> **SCAN IMAGE**
> → ECR IMAGE SCANNING
>
> **DELETE OLD IMAGES**
> → ECR LIFECYCLE POLICY

---

# Ultimate Container Memory Map

> [!tip] If You Remember Nothing Else
>
> **App2Container**
> → Convert an existing app
>
> **ECR**
> → Store the image
>
> **ECS**
> → AWS-native orchestration
>
> **EKS**
> → Kubernetes orchestration
>
> **Fargate**
> → Run containers without managing servers
>
> **App Runner**
> → Simplest web app/API deployment
>
> **ALB**
> → Route web traffic
>
> **SQS**
> → Queue work
>
> **EventBridge**
> → Trigger/schedule work
>
> **EBS**
> → Block storage
>
> **EFS**
> → Shared file storage

Then ask four questions:

> **1. WHO ORCHESTRATES IT?**
>
> AWS-native → ECS  
> Kubernetes → EKS
>
> **2. WHERE DOES IT RUN?**
>
> Host control → EC2  
> No servers → Fargate
>
> **3. WHERE DOES DATA LIVE?**
>
> Block → EBS  
> Shared files → EFS  
> Objects → S3
>
> **4. WHAT KIND OF WORKLOAD?**
>
> Web → ALB + Service  
> Queue → SQS + Workers  
> Schedule/Event → EventBridge + Task

---

## Related Notes

- [[ECS]]
- [[ECS Auto Scaling]]
- [[ECS Solutions Architectures]]
- [[ECS IAM Roles]]
- [[ECR]]
- [[Fargate]]
- [[EKS]]
- [[EKS Node Types]]
- [[EKS Data Volumes]]
- [[App Runner]]
- [[App2Container]]
- [[Application Load Balancer]]
- [[SQS]]
- [[20-SAA/10-Messaging/EventBridge]]
- [[EBS]]
- [[EFS]]
- [[FSx]]
- [[S3]]
- [[02-Compute/Lambda]]