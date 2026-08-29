## What Problem Does It Solve?

[[EKS]] stands for:

**Amazon Elastic Kubernetes Service**

It is AWS's:

**Managed Kubernetes service**

EKS solves the problem:

> **"How can I run Kubernetes on AWS without managing the Kubernetes control plane myself?"**

Architecture:

Kubernetes Application  
↓  
EKS Cluster  
↓  
Worker Compute  
↓  
Pods

> [!tip] Memory Trick
> **EKS = Kubernetes on AWS**
>
> AWS manages:
>
> **Kubernetes control plane**
>
> You choose how to run:
>
> **Worker compute**

---

## What Is Kubernetes?

Kubernetes is an:

**Open-source container orchestration platform**

It helps manage:

- Containers
- Deployments
- Scaling
- Networking
- Service discovery
- Rolling updates
- Self-healing

Think:

Container Images  
↓  
Kubernetes  
↓  
Pods  
↓  
Worker Nodes

---

## Why Use EKS?

Choose EKS when a company requires:

- Kubernetes APIs
- Kubernetes tooling
- Existing Kubernetes skills
- Portability between Kubernetes environments
- Kubernetes ecosystem compatibility

### Killer Exam Clue

> **The company requires Kubernetes**
>
> → **EKS**

---

## EKS vs ECS

This is the biggest comparison.

### [[ECS]]

Think:

**AWS-native container orchestration**

### EKS

Think:

**Managed Kubernetes**

### Exam Shortcut

**AWS-native containers**
→ ECS

**Kubernetes required**
→ EKS

### Memory Trick

**ECS = AWS way**

**EKS = Kubernetes way**

---

## EKS Control Plane

AWS manages the:

**Kubernetes control plane**

This includes the components responsible for:

- Cluster coordination
- API availability
- Control-plane management

The customer does NOT manually operate:

**The Kubernetes control plane infrastructure**

This reduces:

**Operational overhead**

---

## Worker Compute

EKS still needs compute to run:

**Pods**

Common compute options include:

- EC2 worker nodes
- Managed Node Groups
- Fargate

Architecture:

EKS Control Plane  
↓  
Worker Compute  
↓  
Pods

---

## EKS on EC2

With EC2 worker nodes:

You manage or select:

- EC2 instance types
- Node capacity
- Scaling
- Host characteristics

Architecture:

EKS  
↓  
EC2 Worker Nodes  
↓  
Pods

Choose this when you need:

- Host control
- Specific instance types
- Specialized hardware
- Greater infrastructure control

---

## Managed Node Groups

EKS Managed Node Groups simplify:

**EC2 worker node management**

AWS helps automate:

- Node provisioning
- Updates
- Lifecycle operations

You still use:

**EC2-based workers**

but with:

**Less operational overhead**

---

## EKS + Fargate

[[Fargate]] can provide:

**Serverless compute for EKS pods**

Architecture:

EKS  
↓  
Fargate  
↓  
Pods

You do NOT manage:

**EC2 worker nodes**

### Killer Exam Clue

> **Run Kubernetes pods without managing worker nodes**
>
> → **EKS + Fargate**

---

## EKS EC2 vs Fargate

| Requirement | EC2 Workers | Fargate |
|---|---:|---:|
| Manage Worker Nodes | ✅ | ❌ |
| Serverless | ❌ | ✅ |
| Choose Instance Type | ✅ | ❌ |
| Host-Level Control | ✅ | ❌ |
| Minimum Operations | ❌ | ✅ |
| Kubernetes | ✅ | ✅ |

### Memory Trick

**EKS + EC2 = Kubernetes with nodes**

**EKS + Fargate = Kubernetes without nodes**

---

## Pods

A:

**Pod**

is the smallest deployable unit in Kubernetes.

A pod can contain:

**One or more containers**

Architecture:

Pod  
├── Main Container
└── Sidecar Container

### Memory Trick

**ECS Task ≈ Kubernetes Pod**

Conceptually, both represent:

**Running container workloads**

---

## Deployment

A Kubernetes:

**Deployment**

manages:

**Replicated application pods**

Think:

Deployment  
↓  
Desired Replicas = 3  
↓  
├── Pod
├── Pod
└── Pod

If one pod fails:

Kubernetes creates:

**A replacement**

---

## Service

A Kubernetes:

**Service**

provides:

**Stable network access**

to pods.

Pods can be:

- Created
- Destroyed
- Replaced

The Service provides:

**A stable endpoint**

### Memory Trick

**Pods change**

**Service stays**

---

## EKS Networking

EKS integrates with:

**Amazon VPC networking**

Pods can communicate with:

- AWS services
- Other pods
- Load balancers
- Databases

depending on:

**Network configuration**

---

## VPC CNI

EKS commonly uses the:

**Amazon VPC CNI**

to integrate pods with:

**VPC networking**

This allows pods to receive:

**VPC-routable IP addresses**

The exam takeaway:

> **EKS integrates Kubernetes networking directly with the VPC.**

---

## EKS + Load Balancers

EKS workloads can integrate with:

- [[Application Load Balancer]]
- [[Network Load Balancer]]

Use ALB for:

- HTTP
- HTTPS
- Layer 7 routing

Use NLB for:

- TCP
- UDP
- High performance
- Layer 4 requirements

---

## Ingress

In Kubernetes, an:

**Ingress**

defines rules for:

**HTTP/HTTPS routing into applications**

Conceptually:

Internet  
↓  
ALB  
↓  
Ingress Rules  
↓  
Kubernetes Services  
↓  
Pods

### Exam Pattern

> **Route HTTP traffic to multiple Kubernetes applications**
>
> → **Ingress + ALB-style architecture**

---

## EKS + ECR

[[ECR]] can store:

**Container images**

used by EKS.

Architecture:

Developer  
↓  
Build Image  
↓  
ECR  
↓  
EKS  
↓  
Pods

### Memory Trick

**ECR = STORE**

**EKS = ORCHESTRATE**

---

## EKS + IAM

Kubernetes workloads often need access to:

**AWS services**

Examples:

- S3
- DynamoDB
- SQS
- Secrets Manager

The goal is to avoid giving:

**Every worker node the same broad permissions**

Instead, use:

**Workload-level IAM permissions**

---

## IAM Roles for Service Accounts

A common EKS security architecture uses:

**IAM Roles for Service Accounts**

Conceptually:

Kubernetes Service Account  
↓  
IAM Role  
↓  
AWS Service

This gives specific pods:

**Specific AWS permissions**

### Killer Exam Clue

> **Different EKS workloads need different AWS permissions**
>
> → **IAM role associated with the workload/service account**

### Memory Trick

**Pod needs AWS access**
→ Give the workload its own role

---

## Least Privilege

Example:

Orders Pods  
→ DynamoDB Access

Reporting Pods  
→ S3 Access

Payments Pods  
→ KMS Access

Each workload gets:

**Only its required permissions**

This is better than giving broad permissions to:

**All worker nodes**

---

## EKS Auto Scaling

EKS scaling has multiple layers.

Think:

1. Pod scaling
2. Worker-node scaling

This is similar conceptually to:

ECS task scaling vs cluster capacity scaling.

---

## Horizontal Pod Autoscaler

The:

**Horizontal Pod Autoscaler**

can change:

**The number of pods**

based on demand.

Example:

CPU ↑  
↓  
More Pods

CPU ↓  
↓  
Fewer Pods

### Memory Trick

**HPA = Scale Pods**

---

## Cluster Scaling

If more pods are needed but worker nodes lack capacity:

The cluster may need:

**More EC2 worker nodes**

Architecture:

More Pods Requested  
↓  
No Node Capacity  
↓  
Scale Worker Nodes  
↓  
Pods Scheduled

### Exam Principle

> **Pod scaling and node scaling are separate problems**

---

## EKS + Fargate Scaling

With Fargate:

You do NOT manage:

**EC2 worker-node capacity**

This simplifies scaling because AWS provides:

**Underlying compute**

---

## EKS + EBS

EKS can use:

[[EBS]]

for:

**Persistent block storage**

Think:

Pod  
↓  
Persistent Volume  
↓  
EBS

Best for:

**Block storage requirements**

---

## EKS + EFS

EKS can use:

[[EFS]]

for:

**Shared file storage**

Architecture:

Pod A  
↓  

Pod B  
↓  

Pod C  
↓  

EFS

### Killer Exam Clue

> **Multiple Kubernetes pods need shared persistent file storage**
>
> → **EFS**

---

## Persistent Volumes

Containers and pods can be:

**Ephemeral**

Important application data should not depend solely on:

**Local container storage**

Kubernetes uses concepts such as:

- Persistent Volumes
- Persistent Volume Claims

to attach:

**External storage**

---

## EKS + Secrets

Applications may need:

- Database passwords
- API keys
- Credentials

Do NOT hardcode these into:

**Container images**

Use secure secret-management approaches such as:

- Secrets Manager
- Kubernetes secrets with proper protection

depending on architecture.

---

## EKS + CloudWatch

EKS integrates with:

[[07-Monitoring/CloudWatch]]

for monitoring.

Container Insights can collect:

- Metrics
- Logs
- Cluster information
- Pod information

Architecture:

EKS  
↓  
CloudWatch Container Insights

### Exam Pattern

> **Monitor EKS cluster/container metrics and logs**
>
> → **CloudWatch Container Insights**

---

## EKS High Availability

The EKS control plane is managed by:

**AWS**

and designed for:

**High availability**

For application workloads:

Run pods across:

**Multiple Availability Zones**

using worker capacity distributed across:

**Multiple AZs**

---

## Multi-AZ Architecture

Load Balancer  
↓  
EKS  
↓  
├── AZ-A → Worker Nodes / Pods
└── AZ-B → Worker Nodes / Pods

This protects against:

**Single-AZ failure**

---

## EKS + Auto Scaling Groups

EC2 worker nodes may use:

[[Auto Scaling Groups]]

to:

- Add nodes
- Remove nodes
- Replace unhealthy nodes

This provides:

**Infrastructure scaling**

---

## EKS + Spot Instances

EKS worker nodes can use:

**EC2 Spot Instances**

for:

- Fault-tolerant workloads
- Batch workloads
- Stateless workloads
- Cost optimization

Do NOT depend entirely on Spot for:

**Critical non-interruptible workloads**

---

## Mixed Capacity

A common architecture can combine:

- On-Demand nodes
- Spot nodes

This provides:

**Baseline reliability + cost savings**

---

## EKS vs Fargate

Remember:

EKS is:

**Kubernetes orchestration**

Fargate is:

**Compute**

They can work together.

### Memory Trick

**EKS = Kubernetes brain**

**Fargate = Serverless muscle**

---

## EKS vs ECS

### ECS

Advantages:

- AWS-native
- Simpler if Kubernetes is unnecessary
- Tight AWS integration
- Less Kubernetes-specific complexity

### EKS

Advantages:

- Kubernetes compatibility
- Kubernetes ecosystem
- Portability
- Existing Kubernetes tooling

### SAA Rule

> Do NOT choose EKS just because containers are involved.
>
> Choose EKS when:
>
> **Kubernetes is actually required.**

---

## EKS vs Lambda

### EKS

Think:

- Containers
- Kubernetes
- Long-running applications
- More runtime flexibility

### [[02-Compute/Lambda]]

Think:

- Functions
- Event-driven
- Short-lived serverless execution

---

## EKS vs Elastic Beanstalk

Elastic Beanstalk:

**Application platform deployment**

EKS:

**Kubernetes orchestration**

If the question explicitly mentions:

- Kubernetes
- Pods
- Deployments
- Service Accounts

think:

**EKS**

---

## Architecture Thinking

### Scenario 1 — Kubernetes Migration

A company runs Kubernetes on-premises.

It wants to migrate to AWS while keeping:

- Kubernetes APIs
- Existing tooling
- Kubernetes expertise

**Choose → EKS**

---

### Scenario 2 — Kubernetes Without Worker Nodes

Company requires Kubernetes but wants:

**Minimum infrastructure management**

**Choose → EKS + Fargate**

---

### Scenario 3 — Host Control

Kubernetes workloads require:

- Specific EC2 types
- GPUs
- Host-level configuration

**Choose → EKS + EC2 worker nodes**

---

### Scenario 4 — Pod Needs S3

One Kubernetes workload requires:

`s3:GetObject`

Do NOT grant broad S3 permissions to:

**Every node**

Use:

**Workload-specific IAM role / service account architecture**

---

### Scenario 5 — Shared Files

Multiple pods need:

**Shared persistent files**

Choose:

**EFS**

---

### Scenario 6 — Block Storage

One workload needs:

**Persistent block storage**

Think:

**EBS**

---

### Scenario 7 — Public Web Application

Kubernetes application serves:

**HTTP traffic**

Use:

Load Balancer  
↓  
Ingress / Service  
↓  
Pods

ALB is often appropriate for:

**Layer 7 routing**

---

### Scenario 8 — More Pods Needed

CPU increases.

Need:

**More pod replicas**

Think:

**Horizontal Pod Autoscaler**

---

### Scenario 9 — No Node Capacity

More pods are required but:

**All EC2 worker nodes are full**

Need:

**Worker-node / cluster scaling**

---

### Scenario 10 — No Kubernetes Requirement

Company simply needs AWS-native container orchestration.

Do NOT automatically choose EKS.

Think:

[[ECS]]

---

## Scenario Recognition

Immediately think:

[[EKS]]

when you see:

- Kubernetes
- Kubernetes API
- Pods
- Deployments
- Service Accounts
- Managed Kubernetes
- Migrate Kubernetes to AWS
- Kubernetes ecosystem
- Kubernetes portability

---

## Think EKS + Fargate When You See

- Kubernetes
- No worker-node management
- Serverless pods
- Minimum infrastructure overhead

---

## Think EKS + EC2 When You See

- Specific instance type
- GPU
- Host control
- Custom worker nodes
- Specialized hardware

---

## Exam Traps

### Trap 1 — Every Container Workload Should Use EKS

False.

If Kubernetes is unnecessary:

[[ECS]]

may be simpler.

---

### Trap 2 — EKS Is Serverless by Default

False.

EKS manages:

**The Kubernetes control plane**

Worker compute can be:

- EC2
- Fargate

---

### Trap 3 — Fargate Replaces EKS

False.

Fargate provides:

**Compute**

EKS provides:

**Kubernetes orchestration**

---

### Trap 4 — Pods Should Store Important Data Only Locally

Bad architecture.

Use:

**Persistent external storage**

---

### Trap 5 — Node IAM Role Should Give Every Pod All AWS Permissions

Bad least-privilege design.

Prefer:

**Workload-specific IAM permissions**

---

### Trap 6 — Scaling Pods Automatically Adds EC2 Nodes

Not necessarily.

Pod scaling and:

**Node scaling**

are separate.

---

### Trap 7 — EKS Stores Container Images

False.

[[ECR]] stores:

**Container images**

EKS runs:

**Pods**

---

### Trap 8 — Kubernetes Service and AWS ECS Service Are the Same Concept

They are different platform constructs.

Kubernetes Service:

**Stable network access to pods**

ECS Service:

**Maintains desired ECS tasks**

---

### Trap 9 — EKS Is Better Than ECS Because Kubernetes Is More Powerful

Not automatically.

Choose based on:

**Requirements**

not technology prestige.

---

## Quick Cheat Sheet

| Exam Clue | Answer |
|---|---|
| Managed Kubernetes | EKS |
| Kubernetes on AWS | EKS |
| AWS-Native Container Orchestration | ECS |
| Kubernetes Without Worker Nodes | EKS + Fargate |
| Kubernetes with Host Control | EKS + EC2 |
| Store Container Images | ECR |
| Shared File Storage | EFS |
| Persistent Block Storage | EBS |
| Pod-Level AWS Permissions | IAM Role for Workload / Service Account |
| Scale Pod Count | Horizontal Pod Autoscaler |
| Scale EC2 Worker Capacity | Cluster / Node Scaling |
| Monitor Kubernetes Containers | CloudWatch Container Insights |

---

## ECS vs EKS Quick Comparison

| Requirement | ECS | EKS |
|---|---:|---:|
| Container Orchestration | ✅ | ✅ |
| AWS-Native | ✅ | ❌ Kubernetes-Based |
| Kubernetes API | ❌ | ✅ |
| Existing Kubernetes Tools | ❌ | ✅ |
| Easier Without K8s Requirement | ✅ | ❌ |
| Fargate Support | ✅ | ✅ |
| EC2 Worker Support | ✅ | ✅ |

---

## Container Platform Shortcut

> **STORE IMAGE**
> → [[ECR]]
>
> **AWS-NATIVE ORCHESTRATION**
> → [[ECS]]
>
> **KUBERNETES**
> → [[EKS]]
>
> **SERVERLESS CONTAINER COMPUTE**
> → [[Fargate]]

---

## Final Exam Rapid-Fire

> **KUBERNETES**
> → EKS
>
> **NO KUBERNETES REQUIREMENT**
> → CONSIDER ECS
>
> **KUBERNETES + NO WORKER NODES**
> → EKS + FARGATE
>
> **KUBERNETES + HOST CONTROL**
> → EKS + EC2
>
> **STORE IMAGE**
> → ECR
>
> **SHARED FILES**
> → EFS
>
> **BLOCK STORAGE**
> → EBS
>
> **POD AWS PERMISSIONS**
> → WORKLOAD-SPECIFIC IAM ROLE
>
> **MORE PODS**
> → HORIZONTAL POD AUTOSCALER
>
> **MORE EC2 NODE CAPACITY**
> → NODE / CLUSTER SCALING
>
> **MONITOR EKS**
> → CLOUDWATCH CONTAINER INSIGHTS

---

## Master Memory Trick

> [!tip] EKS Master Memory Trick
> Imagine Kubernetes is a shipping yard.
>
> **EKS**
> → Yard manager
>
> **Pods**
> → Shipping containers
>
> **Worker Nodes**
> → Trucks carrying containers
>
> **Deployment**
> → Makes sure enough containers are available
>
> **Service**
> → Stable address where traffic finds the containers
>
> **ECR**
> → Warehouse storing container images
>
> **EFS / EBS**
> → Persistent storage
>
> **Fargate**
> → AWS provides the trucks automatically

So remember:

> **EKS = KUBERNETES**
>
> **ECS = AWS-NATIVE**
>
> **ECR = STORE IMAGES**
>
> **FARGATE = NO WORKER SERVERS**
>
> **EC2 = CONTROL WORKER SERVERS**

And the killer SAA question:

> **"Does the requirement explicitly call for Kubernetes?"**

If:

**YES**
→ EKS

If:

**NO**
→ ECS may be the simpler answer.

---

## Related Notes

- [[ECS]]
- [[Fargate]]
- [[ECR]]
- [[EBS]]
- [[EFS]]
- [[Application Load Balancer]]
- [[Network Load Balancer]]
- [[Auto Scaling Groups]]
- [[07-Monitoring/CloudWatch]]
- [[IAM]]
- [[S3]]