## What Problem Does It Solve?

[[ECS]] stands for:

**Amazon Elastic Container Service**

It is AWS's:

**Fully managed container orchestration service**

ECS helps you:

- Run containers
- Manage container deployments
- Scale containerized applications
- Replace failed containers
- Integrate containers with AWS services

Think:

Docker Container  
↓  
ECS  
↓  
AWS Infrastructure

> [!tip] Memory Trick
> **ECS = AWS-native container orchestration**
>
> You provide:
>
> **Containerized application**
>
> ECS handles:
>
> **Running and managing the containers**

---

## What Is a Container?

A container packages:

- Application code
- Runtime
- Libraries
- Dependencies

into:

**A portable unit**

Conceptually:

Application  
+  
Dependencies  
+  
Runtime  
↓  
Container

Containers are generally:

- Lightweight
- Portable
- Fast to start
- Consistent across environments

---

## Containers vs Virtual Machines

### Virtual Machine

Includes:

- Application
- Libraries
- Guest operating system

Runs on:

**Hypervisor**

---

### Container

Includes:

- Application
- Libraries
- Dependencies

Shares the host:

**Operating system kernel**

This generally makes containers:

**More lightweight than virtual machines**

---

## Docker

ECS commonly runs:

**Docker-compatible container images**

Typical workflow:

Application  
↓  
Docker Image  
↓  
Container Registry  
↓  
ECS

AWS's container registry is:

[[02-Compute/ECR]]

---

## ECS Core Architecture

Think:

ECS Cluster  
↓  
ECS Service  
↓  
ECS Tasks  
↓  
Containers

Important concepts:

- Cluster
- Task Definition
- Task
- Service
- Container Image
- Launch Type / Capacity

---

## ECS Cluster

An:

**ECS Cluster**

is a logical grouping where ECS workloads run.

Depending on the architecture, compute can be provided by:

- EC2 instances
- AWS Fargate

Think:

ECS Cluster  
↓  
Compute Capacity  
↓  
Tasks

---

## ECS Task Definition

A:

**Task Definition**

is the blueprint for running containers.

It defines things such as:

- Container image
- CPU
- Memory
- Ports
- Environment configuration
- IAM roles
- Logging configuration

Think:

> **Task Definition = Container Blueprint**

---

## Task Definition vs Task

### Task Definition

The:

**Blueprint**

### Task

A:

**Running instance of the blueprint**

Architecture:

Task Definition  
↓  
Launch  
↓  
ECS Task  
↓  
Container(s)

### Memory Trick

**Definition = Recipe**

**Task = Meal**

---

## ECS Task

An ECS Task is:

**One running copy of a Task Definition**

A task can contain:

**One or more containers**

Example:

Task  
├── Application Container  
└── Sidecar Container

---

## ECS Service

An:

**ECS Service**

maintains a desired number of running tasks.

Example:

Desired Count:

**3**

ECS attempts to keep:

**3 tasks running**

If one task fails:

3 Tasks  
↓  
1 Fails  
↓  
ECS Starts Replacement  
↓  
3 Tasks Again

> [!tip] Memory Trick
> **TASK = Running workload**
>
> **SERVICE = Keeps tasks running**

---

## ECS Service Architecture

Typical web application:

Users  
↓  
Application Load Balancer  
↓  
ECS Service  
↓  
├── Task
├── Task
└── Task

The service manages:

- Task deployment
- Desired count
- Replacement
- Scaling integration

---

## ECS Launch Options

The major SAA decision is:

### ECS on EC2

or:

### ECS on Fargate

This distinction is:

**Extremely important for the exam**

---

## ECS on EC2

With the EC2 launch model:

**You manage the EC2 instances**

Architecture:

ECS Cluster  
↓  
EC2 Instances  
↓  
ECS Tasks  
↓  
Containers

You are responsible for:

- EC2 instance provisioning
- Instance types
- Scaling EC2 capacity
- Operating system maintenance
- Patching
- Capacity planning

ECS manages:

**Container orchestration**

You manage:

**The underlying EC2 compute**

---

## ECS on EC2 Architecture

ECS Cluster  
↓  
Auto Scaling Group  
↓  
├── EC2 Instance
├── EC2 Instance
└── EC2 Instance  
↓  
ECS Tasks

Tasks are placed onto:

**Available EC2 capacity**

---

## ECS on EC2 Exam Pattern

Choose ECS on EC2 when:

- You need control over EC2 instances
- You need specific instance types
- You need specialized hardware
- You want to manage the underlying infrastructure
- You have workloads where EC2 capacity economics make sense

### Killer Exam Clue

> **Run ECS containers while retaining control over the underlying servers**
>
> → **ECS on EC2**

---

## ECS on Fargate

[[02-Compute/Fargate]] provides:

**Serverless compute for containers**

With Fargate:

You do NOT manage:

**EC2 instances**

Architecture:

ECS  
↓  
Fargate  
↓  
Tasks

AWS manages:

- Servers
- Infrastructure
- Capacity

You specify:

- CPU
- Memory
- Container configuration

> [!tip] Memory Trick
> **Fargate = Containers without managing servers**

---

## Fargate Exam Pattern

Choose Fargate when:

- Minimum operational overhead is required
- You do not want to manage EC2 instances
- Workloads should scale without managing server capacity
- Serverless containers are desired

### Killer Exam Clue

> **Run containers without provisioning or managing servers**
>
> → **ECS + Fargate**

---

## ECS EC2 vs Fargate

| Requirement | ECS on EC2 | ECS on Fargate |
|---|---:|---:|
| Manage EC2 Instances | ✅ | ❌ |
| Serverless | ❌ | ✅ |
| Control Instance Type | ✅ | ❌ |
| Manage OS / Patching | ✅ | ❌ |
| Capacity Planning | More Required | Reduced |
| Specify Task CPU / Memory | ✅ | ✅ |
| Minimum Operations | ❌ | ✅ |
| Container Orchestration | ECS | ECS |

### Memory Trick

**EC2 = Manage Servers**

**Fargate = Manage Tasks**

---

## ECS IAM Roles

ECS has two IAM role concepts that are easy to confuse:

1. ECS Task Role
2. ECS Task Execution Role

This distinction is:

**Very important for SAA**

---

## ECS Task Role

The:

**Task Role**

gives permissions to:

**The application running inside the container**

Example:

ECS Task  
↓  
Application  
↓  
Needs S3 Access

Task Role:

Allow:

`s3:GetObject`

### Killer Exam Clue

> **Containerized application needs permission to access DynamoDB/S3/SQS**
>
> → **ECS Task Role**

### Memory Trick

**TASK ROLE = What the APP can do**

---

## Different Tasks Can Have Different Roles

Example:

Task A  
↓  
S3 Access

Task B  
↓  
DynamoDB Access

Task C  
↓  
SQS Access

Each task can receive:

**Its own IAM permissions**

This follows:

**Least privilege**

---

## ECS Task Execution Role

The:

**Task Execution Role**

gives ECS permissions needed to:

**Start and operate the task**

Examples can include:

- Pull image from [[02-Compute/ECR]]
- Send logs to CloudWatch Logs
- Retrieve certain startup resources

### Memory Trick

**EXECUTION ROLE = What ECS needs to START the task**

---

## Task Role vs Execution Role

| Role | Used By | Purpose |
|---|---|---|
| Task Role | Application | Access AWS Services |
| Task Execution Role | ECS/Fargate Agent | Start / Operate Task |

### Killer Memory Trick

**TASK ROLE**
→ App permissions

**EXECUTION ROLE**
→ Launch permissions

---

## ECS + ECR

[[02-Compute/ECR]] stands for:

**Elastic Container Registry**

It stores:

**Container images**

Architecture:

Developer  
↓  
Build Container Image  
↓  
ECR  
↓  
ECS  
↓  
Task

Think:

**ECR = Container Image Storage**

**ECS = Container Execution / Orchestration**

---

## ECR Workflow

Typical deployment:

Code  
↓  
Build Image  
↓  
Push to ECR  
↓  
ECS Pulls Image  
↓  
Launch Task

### Exam Shortcut

**Store Docker/container image**
→ ECR

**Run container**
→ ECS

---

## ECS + Application Load Balancer

ECS integrates strongly with:

[[Application Load Balancer]]

Architecture:

Users  
↓  
ALB  
↓  
Target Group  
↓  
ECS Tasks

ALB can distribute traffic across:

**Multiple ECS tasks**

---

## Why ALB Works Well With ECS

ALB supports:

- HTTP
- HTTPS
- Path-based routing
- Host-based routing
- Dynamic ports

This makes it ideal for:

**Containerized web applications and microservices**

---

## ECS Dynamic Port Mapping

With ECS on EC2, multiple tasks may run on:

**The same EC2 instance**

Dynamic port mapping allows containers to use:

**Different dynamically assigned host ports**

Example:

ALB  
↓  
EC2 Instance

Task A  
→ Port 32768

Task B  
→ Port 32769

Task C  
→ Port 32770

The ALB knows:

**Which port belongs to each task**

### Killer Exam Clue

> **Multiple ECS tasks run on the same EC2 host and need load balancing**
>
> → **ALB + Dynamic Port Mapping**

---

## ECS + Network Load Balancer

[[Network Load Balancer]] can also work with ECS.

Think NLB when requirements involve:

- TCP
- UDP
- Very high performance
- Static IP-related requirements

For normal HTTP/HTTPS containerized applications:

**ALB is usually the stronger exam answer**

---

## ECS Service Auto Scaling

ECS services can:

**Automatically adjust the number of tasks**

Architecture:

Traffic Increases  
↓  
Metric Increases  
↓  
ECS Service Auto Scaling  
↓  
More Tasks

Traffic Decreases  
↓  
Scale In

---

## ECS Service Auto Scaling Metrics

Scaling can be based on metrics such as:

- CPU utilization
- Memory utilization
- ALB request count per target
- Custom CloudWatch metrics

The key concept:

> **ECS Service Auto Scaling changes the number of ECS tasks.**

---

## ECS Service Scaling vs EC2 Scaling

With ECS on EC2 there can be:

**Two scaling layers**

### Layer 1

ECS Service Auto Scaling

Changes:

**Number of tasks**

### Layer 2

EC2 Auto Scaling

Changes:

**Number of EC2 instances**

Architecture:

Demand  
↓  
More ECS Tasks Needed  
↓  
More EC2 Capacity May Be Needed

### Exam Trap

Adding more ECS tasks does NOT automatically mean:

**Enough EC2 capacity exists**

unless the underlying capacity also scales appropriately.

---

## Fargate Scaling

With Fargate:

You primarily think about:

**Scaling tasks**

You do NOT need to manually manage:

**EC2 capacity**

This is another reason Fargate provides:

**Lower operational overhead**

---

## ECS Capacity Providers

ECS Capacity Providers help manage:

**Compute capacity used by ECS tasks**

They can work with:

- EC2 Auto Scaling Groups
- Fargate
- Fargate Spot

Think:

> **Capacity Provider = Where ECS gets compute capacity**

---

## Capacity Provider Strategy

A capacity provider strategy can help determine:

**How tasks are distributed across available capacity types**

Example:

Some tasks  
→ Fargate

Some tasks  
→ Fargate Spot

This can support:

- Cost optimization
- Availability strategies

---

## Fargate Spot

Fargate Spot provides:

**Discounted spare compute capacity**

Best for:

- Fault-tolerant workloads
- Interruptible workloads
- Batch processing
- Non-critical tasks

Do NOT use it when:

**Tasks cannot tolerate interruption**

### Memory Trick

**Fargate Spot = Spot Instances concept for serverless containers**

---

## ECS Placement Strategies

For ECS on EC2, task placement can influence:

**Where tasks run**

Important placement strategies include:

- Binpack
- Random
- Spread

---

## Binpack

Binpack places tasks to:

**Use as few EC2 instances as possible**

Example:

Fill Instance A  
↓  
Then Instance B

Goal:

**Cost optimization**

### Memory Trick

**BINPACK = PACK TIGHT**

---

## Spread

Spread distributes tasks across:

**Different infrastructure attributes**

Examples:

- Availability Zones
- EC2 instances

Goal:

**High availability**

### Memory Trick

**SPREAD = SPREAD OUT**

---

## Random

Random places tasks:

**Randomly across available instances**

It is simpler but provides less explicit placement optimization.

---

## Placement Strategy Exam Shortcut

| Requirement | Strategy |
|---|---|
| Minimize EC2 Instances / Cost | Binpack |
| High Availability | Spread |
| No Specific Preference | Random |

---

## ECS Networking

With the:

**awsvpc network mode**

each ECS task can receive:

**Its own Elastic Network Interface**

This gives tasks networking behavior similar to:

**EC2 instances inside a VPC**

---

## awsvpc Mode

Each task can have:

- Private IP address
- Security groups
- VPC subnet placement

This is especially important with:

[[02-Compute/Fargate]]

where:

**awsvpc networking is used**

---

## Security Groups

With awsvpc networking:

Security groups can control traffic to:

**Individual tasks**

This enables:

**Fine-grained network security**

Example:

ALB Security Group  
↓  
ECS Task Security Group

Allow:

ALB SG  
→ Task Port

---

## ECS Logging

Containers can send logs to:

**CloudWatch Logs**

Architecture:

ECS Task  
↓  
Container Logs  
↓  
CloudWatch Logs

This provides:

- Centralized logging
- Troubleshooting
- Monitoring

---

## ECS + Secrets

Applications often need:

- Database passwords
- API keys
- Credentials

Do NOT hardcode these into:

**Container images**

Instead use services such as:

- Secrets Manager
- Systems Manager Parameter Store

The task can retrieve:

**Secrets securely**

---

## ECS Storage

Containers can require:

**Persistent shared storage**

ECS can integrate with:

[[EFS]]

Architecture:

ECS Tasks  
↓  
EFS  
↓  
Shared Files

This is especially useful when:

**Multiple tasks need shared persistent file storage**

---

## ECS + EFS

EFS provides:

- Shared file system
- Multi-AZ architecture
- Elastic capacity
- Persistent storage

Example:

Task A  
↓  

Task B  
↓  

Task C  
↓  

EFS

### Killer Exam Clue

> **Multiple ECS tasks need access to the same persistent files**
>
> → **ECS + EFS**

---

## ECS Task Lifecycle

Simplified lifecycle:

Task Definition  
↓  
ECS Schedules Task  
↓  
Compute Capacity Selected  
↓  
Container Image Pulled  
↓  
Container Starts  
↓  
Task Runs  
↓  
Task Stops / Replaced

---

## ECS Service High Availability

For highly available applications:

Run tasks across:

**Multiple Availability Zones**

Architecture:

ALB  
↓  
├── AZ-A → ECS Tasks
└── AZ-B → ECS Tasks

This protects against:

**Single-AZ failure**

---

## ECS Rolling Deployments

ECS services can replace:

**Old tasks with new tasks**

during application deployments.

Concept:

Version 1 Tasks  
↓  
Deploy Version 2  
↓  
Start New Tasks  
↓  
Health Check  
↓  
Stop Old Tasks

This allows:

**Controlled application updates**

---

## ECS Health Checks

Health can be monitored through:

- Container health checks
- Load balancer health checks

If a task becomes unhealthy:

ECS Service  
↓  
Stops / Replaces Task

This helps maintain:

**Desired healthy capacity**

---

## ECS vs Docker

Docker provides:

**Container technology**

ECS provides:

**Container orchestration**

### Memory Trick

**Docker = Build / Run Container**

**ECS = Manage Many Containers**

---

## ECS vs ECR

### [[ECS]]

Purpose:

**Run and orchestrate containers**

### [[02-Compute/ECR]]

Purpose:

**Store container images**

### Memory Trick

**ECR = Registry**

**ECS = Service**

---

## ECS vs Fargate

This comparison is slightly different because:

[[02-Compute/Fargate]] is NOT a replacement for ECS.

ECS:

**Container orchestrator**

Fargate:

**Serverless compute engine**

Architecture:

ECS  
↓  
Fargate  
↓  
Container Tasks

### Memory Trick

**ECS decides WHAT runs**

**Fargate provides WHERE it runs**

---

## ECS vs EKS

[[02-Compute/EKS]] stands for:

**Elastic Kubernetes Service**

Both services:

**Orchestrate containers**

Difference:

ECS:

**AWS-native orchestration**

EKS:

**Managed Kubernetes**

### Exam Shortcut

**AWS-native containers**
→ ECS

**Kubernetes required**
→ EKS

---

## ECS vs Lambda

### ECS

Best for:

- Containers
- Long-running services
- Custom runtimes
- More control over runtime environment

### [[02-Compute/Lambda]]

Best for:

- Event-driven functions
- Short-lived execution
- Serverless functions

### Exam Shortcut

**Containerized long-running application**
→ ECS

**Event-triggered function**
→ Lambda

---

## ECS vs Elastic Beanstalk

Elastic Beanstalk provides:

**Platform deployment abstraction**

ECS provides:

**Container orchestration**

If the question specifically focuses on:

- Containers
- Tasks
- Services
- Container images
- Container scaling

think:

**ECS**

---

## Architecture Thinking

### Scenario 1 — Serverless Containers

A company has Docker containers.

Requirements:

- No EC2 management
- Minimal operations
- Automatic infrastructure management

Choose:

**ECS + Fargate**

---

### Scenario 2 — Control Underlying Instances

A company needs:

- Specific EC2 instance types
- Control over host infrastructure
- ECS orchestration

Choose:

**ECS on EC2**

---

### Scenario 3 — Container Needs S3

An application inside an ECS task needs:

`s3:GetObject`

Choose:

**ECS Task Role**

Do NOT give the permission to:

**Every EC2 instance unnecessarily**

---

### Scenario 4 — ECS Needs to Pull Image

ECS needs permission to:

**Pull an image from ECR**

Think:

**Task Execution Role**

---

### Scenario 5 — Web Application

Containerized HTTP application needs:

- High availability
- Multiple tasks
- Load balancing

Choose:

ALB  
↓  
ECS Service  
↓  
Multiple Tasks

---

### Scenario 6 — Shared Container Storage

Multiple ECS tasks need:

**The same persistent files**

Choose:

**ECS + EFS**

---

### Scenario 7 — Scale Containers

CPU utilization increases.

Need:

**More running tasks**

Choose:

**ECS Service Auto Scaling**

---

### Scenario 8 — EC2 Capacity Problem

ECS Service Auto Scaling launches more tasks.

But:

**No EC2 capacity remains**

Need:

**Scale underlying EC2 capacity**

Think:

EC2 Auto Scaling / ECS Capacity Providers

---

### Scenario 9 — Kubernetes Requirement

The company requires:

**Kubernetes APIs and tooling**

Do NOT choose ECS.

Choose:

[[02-Compute/EKS]]

---

### Scenario 10 — Cost-Optimized Interruptible Containers

Fault-tolerant container workloads can tolerate:

**Interruption**

Choose:

**Fargate Spot**

---

### Scenario 11 — High Availability

Critical ECS application must survive:

**Availability Zone failure**

Run:

**Multiple tasks across multiple AZs**

behind:

**ALB**

---

## Scenario Recognition

Immediately think:

[[ECS]]

when you see:

- Docker containers
- Container orchestration
- Task Definition
- ECS Task
- ECS Service
- Desired task count
- ECS Cluster
- Task Role
- Task Execution Role
- Container deployment
- ECR integration
- Container Auto Scaling

---

## Think ECS on EC2 When You See

- Manage EC2 hosts
- Specific instance type
- Host-level control
- Existing EC2 capacity
- Task placement strategies
- Binpack
- Spread

---

## Think Fargate When You See

- Serverless containers
- No EC2 management
- Minimum operational overhead
- Pay for task resources
- No server provisioning

---

## Exam Traps

### Trap 1 — ECS Stores Container Images

False.

[[02-Compute/ECR]]:

**Stores images**

ECS:

**Runs containers**

---

### Trap 2 — Fargate Replaces ECS

False.

Fargate provides:

**Compute**

ECS provides:

**Orchestration**

---

### Trap 3 — ECS Task Role Pulls the Image From ECR

Wrong role.

Task Role:

**Application permissions**

Task Execution Role:

**ECS startup permissions**

---

### Trap 4 — ECS on EC2 Means AWS Manages the EC2 Hosts Completely

False.

You remain responsible for:

**Underlying EC2 infrastructure**

---

### Trap 5 — Fargate Requires You to Patch EC2 Instances

False.

There are no customer-managed EC2 instances.

---

### Trap 6 — ECS Service Auto Scaling Adds EC2 Instances

Not directly.

Service Auto Scaling changes:

**Task count**

Underlying EC2 capacity may require:

**Separate scaling**

---

### Trap 7 — SQS Is Needed Just to Run ECS Tasks

False.

SQS can be useful for:

**Queue-driven container workers**

but ECS itself does not require SQS.

---

### Trap 8 — Containers Should Store Important Persistent Data Locally

Dangerous assumption.

Containers should generally be treated as:

**Ephemeral**

For shared persistent files:

→ [[EFS]]

---

### Trap 9 — ECS Is Kubernetes

False.

ECS:

**AWS-native**

EKS:

**Kubernetes**

---

### Trap 10 — One Task Equals One Container

Not necessarily.

A task can contain:

**One or more containers**

---

## Quick Cheat Sheet

| Exam Clue | Answer |
|---|---|
| AWS Container Orchestration | ECS |
| Store Container Images | ECR |
| Serverless Containers | Fargate |
| Manage Container Hosts | ECS on EC2 |
| Container App Needs AWS Permissions | Task Role |
| ECS Needs to Pull ECR Image | Task Execution Role |
| Maintain Number of Tasks | ECS Service |
| Container Blueprint | Task Definition |
| Running Blueprint | Task |
| Scale Number of Containers | ECS Service Auto Scaling |
| HTTP Container Load Balancing | ALB |
| Shared Persistent Files | EFS |
| Kubernetes | EKS |
| Cost-Optimized Interruptible Fargate | Fargate Spot |
| Pack Tasks Tightly | Binpack |
| Distribute Tasks for HA | Spread |

---

## ECS Core Components

| Component | Purpose |
|---|---|
| Cluster | Logical ECS Environment |
| Task Definition | Container Blueprint |
| Task | Running Workload |
| Service | Maintains Desired Tasks |
| ECR | Stores Container Images |
| Task Role | App AWS Permissions |
| Execution Role | ECS Startup Permissions |
| ALB | Distributes Application Traffic |
| EFS | Shared Persistent Storage |

---

## EC2 vs Fargate Decision

Need control over servers?  
→ **ECS on EC2**

Need specific instance types?  
→ **ECS on EC2**

Need minimum management?  
→ **Fargate**

Need serverless containers?  
→ **Fargate**

Need fault-tolerant discounted serverless containers?  
→ **Fargate Spot**

---

## IAM Decision Shortcut

Application inside container needs:

S3 / DynamoDB / SQS / other AWS access?

→ **Task Role**

ECS needs to:

Pull image / start task / send logs?

→ **Task Execution Role**

> [!tip] Killer IAM Memory Trick
> **APP → TASK ROLE**
>
> **ECS → EXECUTION ROLE**

---

## Final Exam Rapid-Fire

> **RUN CONTAINERS**
> → ECS
>
> **STORE CONTAINER IMAGE**
> → ECR
>
> **NO SERVER MANAGEMENT**
> → FARGATE
>
> **CONTROL CONTAINER HOSTS**
> → ECS ON EC2
>
> **APP NEEDS AWS PERMISSION**
> → TASK ROLE
>
> **ECS NEEDS STARTUP PERMISSION**
> → EXECUTION ROLE
>
> **KEEP 5 TASKS RUNNING**
> → ECS SERVICE
>
> **DEFINE CONTAINER CONFIGURATION**
> → TASK DEFINITION
>
> **SCALE TASK COUNT**
> → ECS SERVICE AUTO SCALING
>
> **SHARED FILE STORAGE**
> → EFS
>
> **HTTP LOAD BALANCING**
> → ALB
>
> **KUBERNETES**
> → EKS

---

## Master Memory Trick

> [!tip] ECS Master Memory Trick
> Think of a restaurant.
>
> **ECR**
> → Pantry containing ingredients
>
> **Task Definition**
> → Recipe
>
> **Task**
> → Meal being cooked
>
> **ECS Service**
> → Manager making sure enough meals are always being prepared
>
> **ECS Cluster**
> → Kitchen
>
> **EC2**
> → You own and maintain the kitchen equipment
>
> **Fargate**
> → AWS provides the kitchen equipment
>
> **Task Role**
> → What the chef is allowed to access
>
> **Execution Role**
> → What the restaurant needs to prepare the workstation
>
> **ALB**
> → Host directing customers
>
> **EFS**
> → Shared storage room

So remember:

> **ECR = STORE**
>
> **ECS = ORCHESTRATE**
>
> **EC2 = MANAGE SERVERS**
>
> **FARGATE = SERVERLESS CONTAINERS**
>
> **TASK DEFINITION = BLUEPRINT**
>
> **TASK = RUNNING CONTAINER WORKLOAD**
>
> **SERVICE = KEEP TASKS RUNNING**
>
> **TASK ROLE = APP PERMISSIONS**
>
> **EXECUTION ROLE = STARTUP PERMISSIONS**

The biggest SAA question is usually:

> **"Who manages the underlying servers?"**

If the answer is:

**You**
→ ECS on EC2

If the answer is:

**AWS**
→ Fargate

---

## Related Notes

- [[02-Compute/Fargate]]
- [[02-Compute/ECR]]
- [[02-Compute/EKS]]
- [[EC2]]
- [[Application Load Balancer]]
- [[Network Load Balancer]]
- [[Auto Scaling Groups]]
- [[EFS]]
- [[IAM Roles]]
- [[07-Monitoring/CloudWatch]]
- [[SQS]]
- [[02-Compute/Lambda]]