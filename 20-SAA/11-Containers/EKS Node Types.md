## Why This Matters

In [[EKS]], Kubernetes needs:

**Worker compute**

to actually run:

**Pods**

The main worker-compute options are:

- Self-Managed EC2 Nodes
- Managed Node Groups
- [[Fargate]]

The SAA exam often tests:

> **"Who manages the worker nodes, and how much control does the customer need?"**

> [!tip] Master Memory Trick
> **SELF-MANAGED = MOST CONTROL**
>
> **MANAGED NODE GROUP = LESS MANAGEMENT**
>
> **FARGATE = NO NODES TO MANAGE**

---

## EKS Control Plane vs Worker Nodes

AWS manages the:

**EKS Control Plane**

But your workloads still need:

**Compute**

Architecture:

EKS Control Plane  
↓  
Worker Compute  
↓  
Pods

Possible worker compute:

- EC2
- Managed Node Groups
- Fargate

---

## Self-Managed EC2 Nodes

With:

**Self-Managed Nodes**

you create and manage the EC2 worker instances yourself.

Architecture:

EKS  
↓  
Customer-Managed EC2 Nodes  
↓  
Pods

You control:

- EC2 instance type
- AMI
- Patching
- Node configuration
- Auto Scaling Groups
- Upgrade process
- Specialized hardware

### Killer Exam Clue

> **Need maximum control over Kubernetes worker nodes**
>
> → **Self-Managed EC2 Nodes**

---

## Why Use Self-Managed Nodes?

Choose self-managed nodes when:

- Custom AMIs are required
- Specific host configuration is required
- Specialized software must run on nodes
- Maximum infrastructure control is required

Tradeoff:

**More operational responsibility**

---

## Self-Managed Node Responsibilities

You are responsible for:

- Provisioning EC2 instances
- Joining nodes to the EKS cluster
- Patching
- Updating AMIs
- Replacing failed nodes
- Scaling capacity
- Maintaining worker-node configuration

### Memory Trick

**Self-Managed = You own the worker-node lifecycle**

---

## Managed Node Groups

**EKS Managed Node Groups**

provide:

**AWS-managed lifecycle operations for EC2 worker nodes**

The nodes still run on:

**EC2**

but AWS simplifies:

- Provisioning
- Updates
- Node replacement
- Lifecycle management

Architecture:

EKS  
↓  
Managed Node Group  
↓  
EC2 Worker Nodes  
↓  
Pods

### Killer Exam Clue

> **Need EC2 worker nodes but want less operational overhead**
>
> → **Managed Node Group**

---

## Managed Node Groups Still Use EC2

A managed node group is NOT:

**Serverless**

It still uses:

**EC2 instances**

This means you can still choose characteristics such as:

- Instance families
- Capacity type
- Node sizing

### Exam Trap

> **Managed Node Group ≠ Fargate**

Managed Node Group:

**Managed EC2 workers**

Fargate:

**No customer-managed worker nodes**

---

## Managed Node Group Benefits

Managed Node Groups help simplify:

- Node creation
- Node draining
- Updates
- Replacement
- Integration with Auto Scaling

This reduces:

**Manual Kubernetes infrastructure work**

while preserving:

**EC2 worker-node flexibility**

---

## Fargate

[[Fargate]] provides:

**Serverless compute for EKS pods**

Architecture:

EKS  
↓  
Fargate  
↓  
Pods

You do NOT manage:

- EC2 worker nodes
- Node patching
- Node operating systems
- EC2 Auto Scaling Groups

### Killer Exam Clue

> **Run Kubernetes pods without managing worker nodes**
>
> → **EKS + Fargate**

---

## Node Type Comparison

| Requirement | Self-Managed EC2 | Managed Node Group | Fargate |
|---|---:|---:|---:|
| EC2 Worker Nodes | ✅ | ✅ | ❌ |
| Customer Manages Nodes | ✅ | Reduced | ❌ |
| Serverless | ❌ | ❌ | ✅ |
| Custom Host Configuration | ✅ | More Limited | ❌ |
| Choose EC2 Instance Types | ✅ | ✅ | ❌ Host Selection |
| Host-Level Access | ✅ | ✅ | ❌ |
| Minimum Operations | ❌ | Better | ✅ |
| Kubernetes Pods | ✅ | ✅ | ✅ |

---

## Choosing Between the Three

Use:

**Self-Managed Nodes**

when:

> **Control matters most**

Use:

**Managed Node Groups**

when:

> **You still need EC2 workers but want AWS to simplify node management**

Use:

**Fargate**

when:

> **You want to avoid managing worker nodes entirely**

---

## Spot Instances with EKS

EKS worker nodes can use:

**EC2 Spot Instances**

This can reduce:

**Compute cost**

for workloads that can tolerate interruption.

Best for:

- Stateless applications
- Batch workloads
- Fault-tolerant jobs
- Flexible worker pools

---

## On-Demand Nodes

Use:

**On-Demand EC2 instances**

when workloads require:

- Stable baseline capacity
- Less interruption risk
- Critical application availability

---

## Mixed Capacity Strategy

A common architecture combines:

- On-Demand nodes
- Spot nodes

Example:

Critical Pods  
↓  
On-Demand Nodes

Flexible Pods  
↓  
Spot Nodes

This provides:

**Reliability + Cost Optimization**

---

## Managed Node Groups + Spot

Managed Node Groups can use:

**Spot capacity**

for cost-sensitive workloads.

Architecture:

EKS  
↓  
Managed Node Group  
↓  
Spot EC2 Instances  
↓  
Pods

### Exam Pattern

> **Managed Kubernetes EC2 workers with reduced cost and interruption tolerance**
>
> → **Managed Node Group + Spot**

---

## Specialized Hardware

If Kubernetes workloads require:

- GPUs
- High-memory instances
- Compute-optimized instances
- Specialized EC2 capabilities

think:

**EC2-based worker nodes**

rather than:

Fargate

### Killer Exam Clue

> **Kubernetes workload requires GPUs**
>
> → **EKS with EC2 worker nodes**

---

## Node Groups

A node group represents:

**A collection of worker nodes with similar configuration**

Example:

General Node Group  
→ m-family instances

GPU Node Group  
→ p-family instances

Spot Node Group  
→ Spot capacity

Different workloads can be directed toward:

**Different node groups**

---

## Scheduling Workloads to Different Nodes

Kubernetes can use concepts such as:

- Node labels
- Node selectors
- Taints
- Tolerations

to influence:

**Where pods are scheduled**

For SAA, the broad concept is:

> **Different workloads can target different worker-node types**

---

## Example — GPU Workload

Architecture:

EKS  
↓  
├── General Node Group
└── GPU Node Group  
    ↓  
    ML Pods

Machine learning pods can be scheduled onto:

**GPU-capable nodes**

---

## Auto Scaling Worker Nodes

EC2-based EKS worker capacity can be:

**Scaled**

as demand changes.

Architecture:

More Pods Needed  
↓  
Insufficient Node Capacity  
↓  
More EC2 Worker Nodes  
↓  
Pods Scheduled

This is separate from:

**Pod scaling**

---

## Pod Scaling vs Node Scaling

### Pod Scaling

Changes:

**Number of Pods**

Example:

Horizontal Pod Autoscaler

### Node Scaling

Changes:

**Number of EC2 Worker Nodes**

### Memory Trick

**PODS = APPLICATION CAPACITY**

**NODES = INFRASTRUCTURE CAPACITY**

---

## Pending Pods

A major clue for insufficient worker-node capacity:

**Pods remain Pending**

Example:

Desired Pods = 20

Schedulable = 10

Remaining = Pending

Potential reason:

**Not enough worker resources**

### Exam Pattern

> **Pods cannot be scheduled because the cluster lacks compute capacity**
>
> → **Scale worker nodes**

---

## Fargate and Node Scaling

With Fargate:

There is no customer-managed:

**Node scaling layer**

You request pods.

AWS provides:

**Underlying compute**

This reduces:

**Infrastructure management**

---

## EKS Node IAM

EC2 worker nodes have:

**IAM roles**

that allow the nodes to participate in:

**EKS cluster operations**

But application-specific AWS permissions should generally be handled with:

**Workload-specific IAM**

rather than placing every app permission on:

**The node role**

---

## Why Broad Node Roles Are Risky

Suppose:

Node Role  
↓  
S3 Full Access

DynamoDB Full Access

KMS Full Access

Every pod running on those nodes may potentially have:

**Too much effective access**

Better:

Use:

**Workload-specific roles**

### SAA Principle

> **Keep node permissions separate from application permissions**

---

## EKS Node Storage

EC2 worker nodes may use:

**Local or attached storage**

but important application data should generally use:

**Persistent storage abstractions**

such as:

- [[EBS]]
- [[EFS]]

depending on workload requirements.

---

## EBS with Nodes

[[EBS]] provides:

**Persistent block storage**

Best for:

- Single-workload block storage
- Databases
- Stateful applications requiring block devices

---

## EFS with Nodes

[[EFS]] provides:

**Shared file storage**

Best for:

**Multiple pods requiring shared files**

Architecture:

Pods  
↓  
EFS

---

## Architecture Thinking

### Scenario 1 — Maximum Control

A company requires:

- Custom worker AMI
- Specific kernel configuration
- Full host management

Choose:

**Self-Managed EC2 Nodes**

---

### Scenario 2 — EC2 with Less Management

A company wants:

- EC2-based workers
- Specific instance types
- AWS-managed node lifecycle

Choose:

**Managed Node Groups**

---

### Scenario 3 — No Worker Nodes

A company wants:

- Kubernetes
- No EC2 management
- Minimum operational overhead

Choose:

**EKS + Fargate**

---

### Scenario 4 — GPU Workload

Machine learning pods require:

**GPU instances**

Choose:

**EKS + EC2 Worker Nodes**

---

### Scenario 5 — Cost Optimization

Stateless Kubernetes workloads can tolerate interruption.

Choose:

**Spot-based worker nodes**

---

### Scenario 6 — Stable Baseline + Cheap Burst

Critical baseline workloads must remain stable.

Additional workloads can tolerate interruption.

Choose:

- On-Demand baseline
- Spot burst capacity

---

### Scenario 7 — Pods Pending

Pods cannot schedule because worker nodes are full.

Choose:

**Scale EC2 worker-node capacity**

---

### Scenario 8 — Minimal Ops but Kubernetes Required

The application must use:

**Kubernetes APIs**

but the company does not want to patch workers.

Choose:

**EKS + Fargate**

---

## Scenario Recognition

Immediately think:

**Self-Managed Nodes**

when you see:

- Custom AMI
- Maximum host control
- Custom node configuration
- Full lifecycle responsibility

---

## Immediately Think Managed Node Groups When You See

- EC2 worker nodes
- Less node-management overhead
- Managed upgrades / lifecycle
- Need EC2 flexibility

---

## Immediately Think Fargate When You See

- No worker-node management
- Serverless Kubernetes
- Minimum infrastructure operations

---

## Exam Traps

### Trap 1 — Managed Node Groups Are Serverless

False.

They use:

**EC2 worker nodes**

---

### Trap 2 — Fargate Gives Host-Level Access

False.

AWS manages:

**The underlying infrastructure**

---

### Trap 3 — Self-Managed Nodes Mean AWS Manages Patching

False.

You manage:

**Worker-node lifecycle**

---

### Trap 4 — Kubernetes Pod Scaling and Node Scaling Are the Same

False.

Pods:

**Application capacity**

Nodes:

**Compute capacity**

---

### Trap 5 — Pending Pods Always Mean Application Failure

False.

They can indicate:

**Insufficient worker capacity**

---

### Trap 6 — Node Role Should Contain All App Permissions

Bad least-privilege architecture.

Prefer:

**Workload-level IAM**

---

### Trap 7 — Fargate Is Always Better

False.

Use EC2 workers when you need:

- GPUs
- Specific instance types
- Host control
- Specialized capabilities

---

### Trap 8 — Spot Nodes Are Good for Non-Interruptible Critical Workloads

False.

Spot can:

**Be interrupted**

---

## Quick Cheat Sheet

| Exam Clue | Best Choice |
|---|---|
| Maximum Worker Control | Self-Managed Nodes |
| AWS-Managed EC2 Node Lifecycle | Managed Node Groups |
| Serverless Kubernetes Workers | Fargate |
| Custom AMI | Self-Managed Nodes |
| GPU Kubernetes Workload | EC2 Nodes |
| Cost-Optimized Interruptible Workers | Spot Nodes |
| Stable Baseline Capacity | On-Demand Nodes |
| Pods Stuck Pending | Check / Scale Node Capacity |
| App-Level AWS Permissions | Workload-Specific IAM |
| Shared Files | EFS |
| Persistent Block Storage | EBS |

---

## Node Type Decision Table

| Requirement | Answer |
|---|---|
| Full Host Control | Self-Managed EC2 |
| Less EC2 Node Management | Managed Node Group |
| No Nodes to Manage | Fargate |
| Specialized EC2 Hardware | EC2 Nodes |
| Lowest Infrastructure Ops | Fargate |
| EC2 + Managed Lifecycle | Managed Node Groups |

---

## Final Exam Rapid-Fire

> **CUSTOM WORKER AMI**
> → SELF-MANAGED NODES
>
> **EC2 WORKERS + LESS MANAGEMENT**
> → MANAGED NODE GROUP
>
> **NO WORKER NODES**
> → FARGATE
>
> **GPU**
> → EC2 WORKER NODES
>
> **INTERRUPTIBLE LOW-COST WORKLOAD**
> → SPOT NODES
>
> **PODS PENDING**
> → CHECK NODE CAPACITY
>
> **MORE PODS**
> → POD AUTOSCALING
>
> **MORE WORKER CAPACITY**
> → NODE SCALING
>
> **APP AWS ACCESS**
> → WORKLOAD-SPECIFIC IAM

---

## Master Memory Trick

> [!tip] EKS Node Types Master Memory Trick
> Imagine Kubernetes needs cars for its passengers.
>
> **Self-Managed Nodes**
>
> → You buy, repair, fuel, and maintain the cars yourself.
>
> **Managed Node Groups**
>
> → You still use cars, but AWS helps manage the fleet.
>
> **Fargate**
>
> → You request a ride and AWS provides the vehicle automatically.

So remember:

> **SELF-MANAGED**
> → CONTROL
>
> **MANAGED NODE GROUP**
> → EC2 + SIMPLIFIED MANAGEMENT
>
> **FARGATE**
> → SERVERLESS

And the killer exam question:

> **"How much control over the Kubernetes worker infrastructure is required?"**

Maximum control  
→ Self-Managed

EC2 flexibility + less management  
→ Managed Node Group

No worker management  
→ Fargate

---

## Related Notes

- [[EKS]]
- [[Fargate]]
- [[ECS]]
- [[ECR]]
- [[EBS]]
- [[EFS]]
- [[Auto Scaling Groups]]
- [[IAM]]
- [[07-Monitoring/CloudWatch]]