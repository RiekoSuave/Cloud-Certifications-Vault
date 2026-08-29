## What Problem Does It Solve?

[[Fargate]] is AWS's:

**Serverless compute engine for containers**

It allows you to run containers without:

- Provisioning EC2 instances
- Managing container hosts
- Patching host operating systems
- Managing EC2 cluster capacity

Fargate works with:

- [[ECS]]
- [[02-Compute/EKS]]

Architecture:

Container Image  
↓  
ECS / EKS  
↓  
Fargate  
↓  
Running Container

> [!tip] Memory Trick
> **Fargate = Containers without managing servers**
>
> You manage:
>
> **Containers**
>
> AWS manages:
>
> **Servers**

---

## Fargate Is Compute, Not Orchestration

This is one of the most important distinctions.

Fargate does NOT replace:

- [[ECS]]
- [[02-Compute/EKS]]

Instead:

ECS / EKS  
↓  
Orchestration

Fargate  
↓  
Compute

### Memory Trick

**ECS / EKS = WHAT runs**

**Fargate = WHERE it runs**

---

## ECS + Fargate

A common architecture:

[[ECR]]  
↓  
ECS Task Definition  
↓  
ECS Service  
↓  
Fargate Tasks

ECS manages:

- Tasks
- Services
- Deployments
- Desired count

Fargate provides:

**Underlying compute capacity**

---

## Fargate vs ECS on EC2

This is the major SAA decision.

### ECS on EC2

You manage:

- EC2 instances
- Instance types
- Operating systems
- Patching
- Cluster capacity
- Auto Scaling Groups

### ECS on Fargate

AWS manages:

- Servers
- Host infrastructure
- Host operating system
- Underlying capacity

You manage:

- Container image
- CPU
- Memory
- Networking
- IAM
- Application configuration

---

## EC2 vs Fargate Quick Comparison

| Requirement | ECS on EC2 | ECS on Fargate |
|---|---:|---:|
| Manage EC2 Hosts | ✅ | ❌ |
| Serverless | ❌ | ✅ |
| Choose Host Instance Type | ✅ | ❌ |
| Host OS Management | Customer | AWS |
| Host Patching | Customer | AWS |
| Cluster Capacity Planning | Required | Greatly Reduced |
| Task-Level CPU / Memory | ✅ | ✅ |
| Host-Level Control | ✅ | ❌ |
| Minimum Operational Overhead | ❌ | ✅ |

### Killer Memory Trick

**EC2 = Manage Machines**

**Fargate = Manage Tasks**

---

## When to Choose Fargate

Think Fargate when the question says:

- No server management
- Minimum operational overhead
- Serverless containers
- No EC2 provisioning
- No host patching
- Automatically managed compute capacity

### Killer Exam Clue

> **Run containers without provisioning or managing servers**
>
> → **Fargate**

---

## When ECS on EC2 May Be Better

Think ECS on EC2 when you need:

- Specific EC2 instance types
- Host-level control
- Custom AMIs
- Specialized hardware
- Greater control over infrastructure
- Existing EC2 capacity

### Exam Shortcut

**Need host control**
→ EC2

**Need minimum management**
→ Fargate

---

## Fargate Task Resources

With Fargate, you specify resources for:

**Each task**

Important resources include:

- CPU
- Memory

Think:

Task Definition  
↓  
CPU + Memory Requirements  
↓  
Fargate Provides Compute

You do NOT select:

**An EC2 instance type**

---

## Fargate Pricing Model

Fargate pricing is primarily based on:

**Resources requested by your tasks**

Think:

- vCPU
- Memory
- Task runtime

The SAA concept:

> **Pay for task resources instead of managing EC2 server capacity**

---

## Fargate Scaling

Fargate works with:

**ECS Service Auto Scaling**

Architecture:

Traffic ↑  
↓  
Metric ↑  
↓  
ECS Service Auto Scaling  
↓  
More Fargate Tasks

AWS automatically provides:

**Underlying compute**

---

## Why Scaling Is Simpler

With ECS on EC2:

More Tasks Needed  
↓  
Enough EC2 Capacity?

If no:

Scale EC2 Instances  
↓  
Then Place Tasks

With Fargate:

More Tasks Needed  
↓  
Launch More Fargate Tasks

You do NOT separately manage:

**EC2 cluster scaling**

### Memory Trick

**Fargate removes the server-capacity layer**

---

## ECS Service Auto Scaling

Fargate services can scale based on metrics such as:

- CPU utilization
- Memory utilization
- ALB request count per target
- Custom CloudWatch metrics

Example:

CPU ↑  
↓  
Service Auto Scaling  
↓  
More Fargate Tasks

---

## Fargate + ALB

A very common SAA architecture:

Users  
↓  
[[Application Load Balancer]]  
↓  
ECS Service  
↓  
Fargate Tasks

Use this for:

**Serverless containerized web applications**

---

## Multi-AZ Fargate Architecture

For high availability:

ALB  
↓  
├── AZ-A → Fargate Tasks
└── AZ-B → Fargate Tasks

This provides:

- Load balancing
- Horizontal scaling
- Multi-AZ availability
- No EC2 host management

### Killer Exam Pattern

> **Highly available containerized HTTP application with minimum operational overhead**
>
> → **ALB + ECS + Fargate across multiple AZs**

---

## Fargate Networking

Fargate tasks use:

**awsvpc networking**

Each task receives its own:

**Elastic Network Interface**

This gives each task:

- Private IP address
- VPC subnet placement
- Security group association

Think:

Fargate Task  
↓  
ENI  
↓  
VPC

---

## Fargate Security Groups

Because Fargate tasks have:

**Their own network interfaces**

you can apply:

**Security Groups**

to the tasks.

Example:

ALB Security Group  
↓  
Fargate Task Security Group

Allow:

ALB SG  
→ Application Port

### SAA Principle

> **Reference security groups rather than opening application ports broadly**

---

## Public vs Private Subnets

Fargate tasks can run in:

- Public subnets
- Private subnets

For many production applications:

**Private subnets**

are preferred.

Architecture:

Internet  
↓  
ALB in Public Subnets  
↓  
Fargate Tasks in Private Subnets

This prevents application tasks from needing:

**Direct inbound Internet exposure**

---

## Fargate Internet Access

Tasks in private subnets may still need outbound access for:

- External APIs
- Software downloads
- Other Internet resources

A common architecture uses:

[[NAT Gateway]]

Private Fargate Task  
↓  
NAT Gateway  
↓  
Internet

---

## AWS Service Access

Fargate tasks may need access to AWS services such as:

- ECR
- S3
- CloudWatch
- Secrets Manager

Depending on the architecture, access can use:

- NAT Gateway
- VPC Endpoints

VPC Endpoints can help keep traffic:

**Inside the AWS network**

and potentially reduce dependence on:

**NAT Gateway**

---

## Fargate + ECR

A typical deployment:

Developer  
↓  
Build Image  
↓  
[[ECR]]  
↓  
Fargate Task

ECR:

**Stores image**

Fargate:

**Provides compute**

ECS:

**Orchestrates task**

### Memory Trick

**ECR = STORE**

**ECS = MANAGE**

**FARGATE = RUN**

---

## Task Execution Role

When ECS launches a Fargate task and needs to:

- Pull image from ECR
- Send container logs
- Retrieve startup secrets

think:

**Task Execution Role**

Architecture:

ECS / Fargate Runtime  
↓  
Execution Role  
↓  
AWS Service

### Memory Trick

**EXECUTION ROLE = START**

---

## Task Role

When the application inside the Fargate task needs:

- S3
- DynamoDB
- SQS
- SNS
- Secrets Manager
- Other AWS APIs

use:

**Task Role**

Architecture:

Application  
↓  
Task Role  
↓  
AWS Service

### Memory Trick

**TASK ROLE = APP**

---

## IAM Quick Comparison

| Requirement | Role |
|---|---|
| App Reads S3 | Task Role |
| App Writes DynamoDB | Task Role |
| App Polls SQS | Task Role |
| ECS Pulls ECR Image | Execution Role |
| ECS Sends Logs | Execution Role |
| ECS Injects Startup Secret | Execution Role |

> [!tip] Killer IAM Rule
> **APP → TASK ROLE**
>
> **START → EXECUTION ROLE**

---

## Fargate + CloudWatch

Fargate workloads integrate with:

[[07-Monitoring/CloudWatch]]

for:

- Metrics
- Logs
- Alarms
- Auto Scaling

Architecture:

Fargate Task  
↓  
CloudWatch Logs

Metrics  
↓  
CloudWatch  
↓  
Scaling Policy

---

## Fargate + SQS Workers

Fargate is useful for:

**Asynchronous worker containers**

Architecture:

Producer  
↓  
[[SQS]]  
↓  
ECS Service  
↓  
Fargate Workers

Benefits:

- Queue buffering
- Serverless workers
- Horizontal scaling
- No EC2 management

---

## Queue-Based Scaling

Architecture:

SQS Queue Depth ↑  
↓  
CloudWatch Metric  
↓  
ECS Service Auto Scaling  
↓  
More Fargate Tasks

Backlog ↓  
↓  
Scale In

### Killer Exam Pattern

> **Serverless container workers should scale with an SQS backlog**
>
> → **SQS + ECS Service Auto Scaling + Fargate**

---

## Fargate + EventBridge

[[20-SAA/10-Messaging/EventBridge]] can trigger:

**ECS tasks running on Fargate**

Architecture:

Event  
↓  
EventBridge  
↓  
ECS Task  
↓  
Fargate

This is useful for:

**Event-driven container jobs**

---

## Scheduled Fargate Tasks

Example:

Every Night  
↓  
EventBridge  
↓  
ECS Task  
↓  
Fargate  
↓  
Job Runs  
↓  
Task Stops

Use for:

- Reports
- Cleanup jobs
- Batch processing
- Maintenance

### Killer Exam Clue

> **Run a containerized job periodically without maintaining servers**
>
> → **Scheduled ECS Task + Fargate**

---

## Fargate Service vs One-Off Task

### ECS Service on Fargate

Use for:

**Long-running applications**

Examples:

- Web application
- API
- Continuous worker pool

---

### Standalone Fargate Task

Use for:

**Finite jobs**

Examples:

- Report generation
- Scheduled processing
- Event-driven processing

### Memory Trick

**SERVICE = STAY RUNNING**

**TASK = RUN AND FINISH**

---

## Fargate + EFS

Fargate tasks can use:

[[EFS]]

for:

**Persistent shared file storage**

Architecture:

Fargate Task A  
↓  

Fargate Task B  
↓  

Fargate Task C  
↓  

EFS

### Killer Exam Clue

> **Multiple Fargate tasks need shared persistent files**
>
> → **Fargate + EFS**

---

## Why External Storage Matters

Fargate tasks should generally be treated as:

**Ephemeral and replaceable**

Do NOT design scalable applications around:

**Important data existing only inside one task**

Externalize persistent state to services such as:

- EFS
- S3
- RDS
- DynamoDB
- ElastiCache

### SAA Principle

> **Stateless containers scale more easily**

---

## Fargate Spot

Fargate supports:

**Fargate Spot**

This uses:

**Spare AWS capacity**

at a lower price.

Tradeoff:

Tasks can be:

**Interrupted**

---

## When to Use Fargate Spot

Good workloads include:

- Batch processing
- Fault-tolerant workers
- Queue consumers
- Development workloads
- Interruptible background jobs

Avoid for:

- Critical workloads
- Tasks that cannot tolerate interruption
- Stateful workloads without recovery mechanisms

### Memory Trick

**Fargate Spot = Cheap but Interruptible**

---

## Fargate Spot + SQS

A strong cost-optimized architecture:

SQS  
↓  
Fargate Spot Workers

Why?

If a worker is interrupted:

Message eventually becomes available again  
↓  
Another worker can process it

This works well because:

**SQS provides durability**

while:

**Fargate Spot reduces compute cost**

---

## Capacity Providers

ECS:

**Capacity Providers**

can define how tasks use:

- Fargate
- Fargate Spot

Example:

ECS Service  
↓  
Capacity Provider Strategy  
↓  
├── Fargate
└── Fargate Spot

This supports:

**Blended reliability and cost optimization**

---

## Base and Weight

Capacity provider strategies can use:

### Base

Minimum number of tasks placed on:

**A specific provider**

### Weight

Relative distribution of:

**Additional tasks**

Example:

Base:

2 Fargate Tasks

Then:

1 part Fargate  
3 parts Fargate Spot

### Memory Trick

**BASE = MINIMUM**

**WEIGHT = RATIO**

---

## Example Cost Architecture

Requirement:

- At least two reliable tasks
- Extra capacity can be interruptible

Strategy:

Base = 2  
→ Fargate

Additional Tasks  
→ Mostly Fargate Spot

This provides:

**Stable baseline + cheaper burst capacity**

---

## Fargate vs Lambda

Both are:

**Serverless compute**

but solve different problems.

### [[02-Compute/Lambda]]

Think:

- Functions
- Event-driven
- Short-lived execution
- Function-level abstraction

### Fargate

Think:

- Containers
- Longer-running workloads
- Custom container runtime
- More runtime control

### Exam Shortcut

**Function**
→ Lambda

**Container**
→ Fargate

---

## Fargate vs EC2

### [[EC2]]

Think:

- Virtual machines
- Host control
- OS access
- Instance types
- Server management

### Fargate

Think:

- Containers
- No host management
- Task resources
- Serverless compute

---

## Fargate vs ECS

### [[ECS]]

Provides:

**Container orchestration**

### Fargate

Provides:

**Container compute**

They commonly work:

**Together**

Do NOT treat them as:

**Competing services**

---

## Fargate vs EKS

[[02-Compute/EKS]] provides:

**Kubernetes orchestration**

Fargate can provide:

**Serverless compute for certain EKS workloads**

Think:

EKS  
↓  
Fargate  
↓  
Kubernetes Pods

### Exam Shortcut

**Need Kubernetes + no worker-node management**
→ EKS + Fargate

---

## Fargate vs Elastic Beanstalk

Elastic Beanstalk focuses on:

**Application platform deployment**

Fargate focuses on:

**Serverless container compute**

If the question explicitly emphasizes:

- Containers
- Task definitions
- ECS services
- No EC2 host management

think:

**Fargate**

---

## Architecture Thinking

### Scenario 1 — Serverless Web Containers

Requirements:

- Docker application
- HTTP traffic
- Multi-AZ
- No EC2 management

Choose:

ALB  
↓  
ECS Service  
↓  
Fargate

---

### Scenario 2 — Background Workers

Requirements:

- SQS queue
- Bursty workload
- No server management
- Horizontal scaling

Choose:

SQS  
↓  
ECS Service  
↓  
Fargate Workers

---

### Scenario 3 — Scheduled Job

A container must run:

**Once every night**

Choose:

EventBridge  
↓  
ECS Task  
↓  
Fargate

---

### Scenario 4 — Shared Storage

Multiple serverless container tasks need:

**Shared persistent files**

Choose:

Fargate  
+  
EFS

---

### Scenario 5 — Application Reads S3

Application code inside Fargate needs:

`s3:GetObject`

Choose:

**Task Role**

---

### Scenario 6 — Pull Private Image

Fargate task cannot start because ECS cannot pull:

**Private ECR image**

Check:

**Task Execution Role**

---

### Scenario 7 — Host-Level Requirement

Application requires:

- Specific EC2 instance type
- Host configuration
- OS-level access

Do NOT choose Fargate.

Choose:

**ECS on EC2**

---

### Scenario 8 — Cost-Sensitive Workers

Background jobs:

- Can tolerate interruption
- Are retriable
- Use SQS

Choose:

**Fargate Spot**

---

### Scenario 9 — Kubernetes

Company requires:

**Kubernetes APIs**

but does not want to manage worker nodes.

Think:

**EKS + Fargate**

---

### Scenario 10 — Traffic Growth

CPU rises on an ECS Fargate service.

Need more capacity.

Choose:

**ECS Service Auto Scaling**

No EC2 ASG is required.

---

## Scenario Recognition

Immediately think:

[[Fargate]]

when you see:

- Serverless containers
- No EC2 management
- No server provisioning
- Minimum operational overhead
- Containerized application
- Task-level CPU and memory
- AWS-managed container infrastructure

---

## Think Fargate Spot When You See

- Interruptible container workload
- Fault-tolerant jobs
- Background processing
- Cost optimization
- SQS workers

---

## Think ECS on EC2 Instead When You See

- Host-level control
- Specific instance types
- Specialized hardware
- Custom host configuration
- EC2 management acceptable

---

## Exam Traps

### Trap 1 — Fargate Is a Container Orchestrator

False.

ECS / EKS:

**Orchestrate**

Fargate:

**Provides compute**

---

### Trap 2 — Fargate Requires EC2 Instances in Your Account

False.

You do not provision or manage:

**The underlying hosts**

---

### Trap 3 — Fargate Cannot Auto Scale

False.

ECS services running on Fargate can use:

**ECS Service Auto Scaling**

---

### Trap 4 — Fargate Needs an EC2 Auto Scaling Group

False.

AWS manages:

**Underlying compute capacity**

---

### Trap 5 — Fargate Eliminates the Need for ECS

False.

ECS can orchestrate:

**Fargate tasks**

---

### Trap 6 — Fargate Spot Is Guaranteed Capacity

False.

It uses:

**Spare capacity**

and tasks can be:

**Interrupted**

---

### Trap 7 — Fargate Spot Is Best for Critical Stateful Workloads

False.

Use it for:

**Fault-tolerant workloads**

---

### Trap 8 — Application AWS Permissions Belong to the Execution Role

False.

Application permissions:

**Task Role**

---

### Trap 9 — Fargate Tasks Cannot Use Shared Persistent Storage

False.

They can integrate with:

[[EFS]]

---

### Trap 10 — Fargate Means the Application Is Automatically Stateless

False.

Fargate manages:

**Infrastructure**

You still need to design:

**Application state correctly**

---

## Quick Cheat Sheet

| Exam Clue | Answer |
|---|---|
| Serverless Containers | Fargate |
| No EC2 Management | Fargate |
| ECS + Minimum Operations | ECS + Fargate |
| Control Host | ECS on EC2 |
| Long-Running Container App | ECS Service + Fargate |
| One-Off Container Job | ECS Task + Fargate |
| Scheduled Container | EventBridge + ECS + Fargate |
| Serverless Queue Workers | SQS + ECS + Fargate |
| Shared Persistent Files | Fargate + EFS |
| App AWS Permissions | Task Role |
| Pull ECR Image | Execution Role |
| Interruptible Cheap Containers | Fargate Spot |
| Kubernetes Without Worker Nodes | EKS + Fargate |

---

## EC2 vs Fargate Decision Tree

Need containers?  
↓

Need host-level control?

Yes  
→ **ECS on EC2**

No  
↓

Want minimum operational overhead?

Yes  
→ **Fargate**

Need Kubernetes?

Yes  
→ **EKS + Fargate**

Need AWS-native orchestration?

Yes  
→ **ECS + Fargate**

---

## Serverless Decision Shortcut

Need:

**Event-driven function**

→ [[02-Compute/Lambda]]

Need:

**Serverless container**

→ [[Fargate]]

Need:

**Serverless object storage**

→ [[S3]]

Need:

**Serverless NoSQL database**

→ DynamoDB

---

## Final Exam Rapid-Fire

> **SERVERLESS CONTAINERS**
> → FARGATE
>
> **NO EC2 HOST MANAGEMENT**
> → FARGATE
>
> **AWS-NATIVE ORCHESTRATION**
> → ECS
>
> **KUBERNETES**
> → EKS
>
> **STORE CONTAINER IMAGE**
> → ECR
>
> **APP AWS ACCESS**
> → TASK ROLE
>
> **PULL ECR IMAGE**
> → EXECUTION ROLE
>
> **SHARED FILE STORAGE**
> → EFS
>
> **SERVERLESS HTTP CONTAINERS**
> → ALB + ECS + FARGATE
>
> **SERVERLESS QUEUE WORKERS**
> → SQS + ECS + FARGATE
>
> **CHEAP INTERRUPTIBLE CONTAINERS**
> → FARGATE SPOT
>
> **NEED HOST CONTROL**
> → ECS ON EC2

---

## Master Memory Trick

> [!tip] Fargate Master Memory Trick
> Imagine renting a commercial kitchen.
>
> With:
>
> **ECS on EC2**
>
> you manage:
>
> - Kitchen equipment
> - Maintenance
> - Repairs
> - Capacity
>
> With:
>
> **Fargate**
>
> AWS says:
>
> **"Just tell me how many cooks you need and how much workspace they require."**
>
> AWS handles:
>
> **The kitchen infrastructure**

So remember:

> **ECS**
> → MANAGES CONTAINERS
>
> **ECR**
> → STORES IMAGES
>
> **FARGATE**
> → PROVIDES SERVERLESS COMPUTE
>
> **EC2**
> → YOU MANAGE SERVERS
>
> **FARGATE SPOT**
> → CHEAPER + INTERRUPTIBLE
>
> **TASK ROLE**
> → APP PERMISSIONS
>
> **EXECUTION ROLE**
> → STARTUP PERMISSIONS

And the killer SAA clue:

> **"Run containers with the least operational overhead and without managing EC2 instances."**
>
> → **FARGATE**

---

## Related Notes

- [[ECS]]
- [[ECS Auto Scaling]]
- [[ECS Solutions Architectures]]
- [[ECS IAM Roles]]
- [[ECR]]
- [[02-Compute/EKS]]
- [[Application Load Balancer]]
- [[SQS]]
- [[20-SAA/10-Messaging/EventBridge]]
- [[EFS]]
- [[02-Compute/Lambda]]
- [[07-Monitoring/CloudWatch]]
- [[NAT Gateway]]