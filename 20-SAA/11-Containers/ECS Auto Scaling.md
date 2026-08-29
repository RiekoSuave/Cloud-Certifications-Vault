## What Problem Does It Solve?

[[ECS Auto Scaling]] helps an ECS application:

**Automatically adjust capacity as demand changes**

There are two different scaling concepts you must keep separate:

1. **ECS Service Auto Scaling**
2. **ECS Cluster / EC2 Capacity Scaling**

This distinction is extremely important for SAA.

> [!tip] Master Memory Trick
> **Service Auto Scaling = Scale TASKS**
>
> **EC2 Auto Scaling = Scale SERVERS**

---

## The Two Scaling Layers

When running ECS on EC2:

Traffic  
↓  
ECS Service  
↓  
Tasks  
↓  
EC2 Instances

There are potentially:

**Two separate scaling layers**

### Layer 1 — ECS Service Auto Scaling

Changes:

**Number of ECS Tasks**

### Layer 2 — EC2 Auto Scaling

Changes:

**Number of EC2 Instances**

> [!warning] Exam Trap
> More tasks do NOT help if the ECS cluster does not have enough underlying EC2 capacity.

---

## ECS Service Auto Scaling

ECS Service Auto Scaling automatically changes:

**The desired number of ECS tasks**

Example:

Normal Traffic  
↓  
4 Tasks

Traffic Increases  
↓  
Scale Out

8 Tasks

Traffic Decreases  
↓  
Scale In

4 Tasks

The goal is:

**Match application capacity to demand**

---

## Desired Task Count

An ECS Service maintains a:

**Desired Count**

Example:

Desired Count = 4

ECS attempts to keep:

**4 healthy tasks running**

If a task fails:

4 Tasks  
↓  
1 Fails  
↓  
ECS Replaces It  
↓  
4 Healthy Tasks

This is:

**Service maintenance**

Scaling goes further by changing the desired count itself.

---

## Desired Count vs Auto Scaling

These concepts are related but different.

### Desired Count

Defines:

**How many tasks should currently be running**

### Auto Scaling

Automatically changes:

**The desired count**

Example:

Desired Count = 4  
↓  
CPU Increases  
↓  
Auto Scaling  
↓  
Desired Count = 8

---

## Scaling Metrics

ECS Service Auto Scaling commonly uses:

**CloudWatch metrics**

Important metrics include:

- ECS Service Average CPU Utilization
- ECS Service Average Memory Utilization
- ALB Request Count Per Target
- Custom CloudWatch metrics

Architecture:

Metric  
↓  
CloudWatch  
↓  
Auto Scaling  
↓  
Change Desired Task Count

---

## CPU-Based Scaling

Example:

Average CPU  
↓  
Target = 50%

If CPU rises above the target:

**Scale Out**

If CPU falls sufficiently:

**Scale In**

Architecture:

CPU ↑  
↓  
More Tasks

CPU ↓  
↓  
Fewer Tasks

### Exam Pattern

> **Automatically add ECS tasks when average CPU utilization increases**
>
> → **ECS Service Auto Scaling**

---

## Memory-Based Scaling

ECS can also scale based on:

**Average memory utilization**

Example:

Memory Usage ↑  
↓  
ECS Service Auto Scaling  
↓  
More Tasks

This is useful for applications where:

**Memory is the primary capacity constraint**

---

## ALB Request Count Per Target

For applications behind an:

[[Application Load Balancer]]

ECS can scale using:

**ALB Request Count Per Target**

Architecture:

Users  
↓  
ALB  
↓  
ECS Tasks

Requests per target ↑  
↓  
More Tasks

This can be useful when:

**Application demand correlates more closely with requests than CPU or memory**

---

## Target Tracking Scaling

Target Tracking attempts to maintain:

**A target value for a metric**

Example:

Target:

CPU = 50%

Auto Scaling continuously adjusts capacity to keep the metric:

**Near the target**

### Memory Trick

**Target Tracking = Thermostat**

You set:

**Desired temperature**

The system automatically adjusts:

**Heating / cooling**

Likewise:

You set:

**Desired metric**

ECS adjusts:

**Task count**

---

## Target Tracking Example

Target:

50% CPU

Current:

80% CPU

Result:

**Scale Out**

Later:

Current:

25% CPU

Result:

**Scale In**

The exact number of tasks is managed automatically according to:

**The scaling policy**

---

## Step Scaling

Step Scaling changes capacity based on:

**The size of a CloudWatch alarm breach**

Example:

CPU 60%  
→ Add 1 Task

CPU 75%  
→ Add 2 Tasks

CPU 90%  
→ Add 4 Tasks

Think:

**Different alarm severity = Different scaling amount**

### Memory Trick

**STEP = Bigger problem → Bigger response**

---

## Scheduled Scaling

Scheduled Scaling changes capacity based on:

**Known time patterns**

Example:

Business knows traffic spikes:

Every weekday at 8:00 AM

Schedule:

7:45 AM  
↓  
Increase Desired Tasks

After peak:

6:00 PM  
↓  
Reduce Desired Tasks

### Exam Pattern

> **Traffic predictably increases every weekday morning**
>
> → **Scheduled Scaling**

---

## Scaling Policy Comparison

| Scaling Method | Best Use |
|---|---|
| Target Tracking | Maintain Metric Target |
| Step Scaling | Different Response Based on Alarm Size |
| Scheduled Scaling | Predictable Demand |

### Exam Shortcut

**Maintain 50% CPU**
→ Target Tracking

**Scale differently at 70%, 80%, 90%**
→ Step Scaling

**Scale every weekday at 8 AM**
→ Scheduled Scaling

---

## ECS on Fargate Scaling

With [[02-Compute/Fargate]]:

ECS Service Auto Scaling changes:

**The number of Fargate tasks**

Architecture:

Demand ↑  
↓  
ECS Service Auto Scaling  
↓  
More Fargate Tasks

You do NOT need to scale:

**EC2 instances**

because AWS manages:

**The underlying infrastructure**

> [!tip] Memory Trick
> **Fargate scaling = Think TASKS only**

---

## Why Fargate Simplifies Scaling

With ECS on EC2:

More Tasks  
↓  
Need EC2 Capacity

With Fargate:

More Tasks  
↓  
AWS Provides Compute

This eliminates much of the:

**Cluster capacity management**

---

## ECS on EC2 Scaling

With ECS on EC2:

Tasks need:

**Available EC2 capacity**

Architecture:

ECS Service  
↓  
Tasks  
↓  
EC2 Instances

If tasks increase:

More Tasks  
↓  
May Need More EC2 Instances

This creates:

**Two scaling problems**

---

## Scaling Problem Example

Suppose:

ECS Cluster  
↓  
2 EC2 Instances

Each EC2 instance can run:

4 Tasks

Maximum current capacity:

**8 Tasks**

Now ECS Service Auto Scaling requests:

**12 Tasks**

Result:

8 Tasks Running  
+  
4 Tasks Pending

Why?

There is:

**Insufficient EC2 capacity**

---

## Pending Tasks

A major clue that the ECS cluster may lack capacity is:

**Tasks remain in PENDING state**

Example:

Desired Tasks = 12

Running = 8

Pending = 4

Potential problem:

**Not enough cluster capacity**

The solution may involve:

**Scaling the underlying EC2 infrastructure**

---

## EC2 Auto Scaling Group

ECS EC2 instances can be managed by an:

[[Auto Scaling Groups|Auto Scaling Group]]

Architecture:

ECS Cluster  
↓  
Auto Scaling Group  
↓  
EC2 Instances

The ASG can:

- Add instances
- Remove instances
- Replace unhealthy instances

This handles:

**Underlying compute capacity**

---

## ECS Cluster Capacity Scaling

Think:

ECS Tasks  
↓  
Need Compute  
↓  
EC2 Capacity

The cluster needs enough:

- CPU
- Memory
- Network capacity
- Instance resources

to place:

**Requested tasks**

---

## ECS Capacity Providers

ECS:

**Capacity Providers**

help manage the compute capacity available to:

**ECS tasks**

Capacity Providers can work with:

- EC2 Auto Scaling Groups
- Fargate
- Fargate Spot

Think:

> **Capacity Provider = Where ECS gets compute capacity**

---

## Capacity Provider + EC2 Auto Scaling

For ECS on EC2:

Capacity Provider  
↓  
EC2 Auto Scaling Group  
↓  
EC2 Instances  
↓  
ECS Tasks

The capacity provider helps connect:

**ECS task demand**

with:

**EC2 cluster capacity**

---

## Cluster Auto Scaling

ECS Cluster Auto Scaling can use:

**Capacity Providers**

to automatically adjust:

**EC2 Auto Scaling Group capacity**

based on ECS task demand.

Architecture:

More Tasks Needed  
↓  
Insufficient EC2 Capacity  
↓  
Capacity Provider  
↓  
ASG Scales Out  
↓  
More EC2 Instances  
↓  
Tasks Placed

### Killer Exam Clue

> **ECS tasks are pending because the EC2-backed cluster lacks capacity**
>
> → **ECS Capacity Provider / Cluster Auto Scaling**

---

## Managed Scaling

Capacity Providers can provide:

**Managed Scaling**

for associated EC2 Auto Scaling Groups.

The goal:

**Automatically maintain enough cluster capacity for ECS workloads**

This reduces:

**Manual EC2 capacity management**

---

## Managed Termination Protection

Capacity Providers can also help protect:

**EC2 instances running ECS tasks**

from being terminated prematurely during:

**Scale-in**

This helps prevent:

**Running tasks from being unnecessarily disrupted**

---

## ECS Service Scaling vs Cluster Scaling

This is the biggest concept in the note.

### Service Scaling

Question:

> **How many application tasks do I need?**

Changes:

**Task count**

---

### Cluster Scaling

Question:

> **Do I have enough servers to run those tasks?**

Changes:

**EC2 capacity**

### Memory Trick

**SERVICE = WORKLOAD**

**CLUSTER = INFRASTRUCTURE**

---

## Scaling Architecture

Traffic ↑  
↓  
ALB  
↓  
ECS Service Auto Scaling  
↓  
More Tasks Needed  
↓  
Capacity Provider  
↓  
EC2 Auto Scaling Group  
↓  
More EC2 Instances

Two decisions:

**How many tasks?**

and:

**Where will those tasks run?**

---

## Service Scaling Without Cluster Scaling

Example:

Service Auto Scaling  
↓  
Desired Tasks = 20

But cluster capacity:

Only supports 10 tasks

Result:

10 Running  
10 Pending

Therefore:

> **Scaling tasks without scaling infrastructure can create pending tasks.**

---

## Cluster Scaling Without Service Scaling

Suppose:

EC2 Auto Scaling Group  
↓  
Adds 10 EC2 instances

But ECS Service Desired Count remains:

**4**

Result:

You may have:

**Large amounts of unused EC2 capacity**

Therefore:

> **Scaling infrastructure alone does not automatically mean more application tasks are required.**

---

## Fargate Removes the Second Layer

With Fargate:

Traffic ↑  
↓  
Service Auto Scaling  
↓  
More Tasks  
↓  
Fargate Provides Capacity

You don't manage:

**EC2 Auto Scaling Groups**

This is why Fargate is commonly associated with:

**Minimum operational overhead**

---

## Fargate Spot

[[02-Compute/Fargate]] also supports:

**Fargate Spot**

This uses:

**Spare AWS capacity**

at a lower cost.

Best for:

- Fault-tolerant tasks
- Batch workloads
- Interruptible workloads

Avoid for:

**Critical workloads that cannot tolerate interruption**

---

## Capacity Provider Strategy

A:

**Capacity Provider Strategy**

determines how ECS tasks use available:

**Capacity Providers**

Example:

ECS Service  
↓  
├── Fargate
└── Fargate Spot

This can balance:

- Availability
- Cost
- Workload requirements

---

## Base

A capacity provider strategy can define a:

**Base**

This represents:

**The minimum number of tasks placed on a specific capacity provider**

Example:

Base = 2 on Fargate

First 2 tasks:

→ Fargate

Additional tasks can then follow:

**Configured weights**

---

## Weight

Capacity Provider:

**Weight**

controls the relative proportion of tasks placed across providers.

Example:

Fargate Weight = 1

Fargate Spot Weight = 3

After satisfying the base:

More tasks are proportionally favored toward:

**Fargate Spot**

### Memory Trick

**BASE = Minimum**

**WEIGHT = Distribution**

---

## Auto Scaling + ALB

A common production architecture:

Users  
↓  
[[Application Load Balancer]]  
↓  
ECS Service  
↓  
Multiple Tasks

ALB Request Count  
↓  
CloudWatch Metric  
↓  
ECS Service Auto Scaling  
↓  
Task Count Changes

This creates:

**Demand-driven application scaling**

---

## Auto Scaling + CloudWatch

[[07-Monitoring/CloudWatch]] provides:

**Metrics and alarms**

that can drive scaling.

Architecture:

ECS Metric  
↓  
CloudWatch  
↓  
Scaling Policy  
↓  
ECS Service Auto Scaling

Examples:

CPU ↑  
→ Scale Out

Memory ↑  
→ Scale Out

Requests ↑  
→ Scale Out

---

## Scaling Out

Scale Out means:

**Increase capacity**

For ECS Service Auto Scaling:

More Tasks

For EC2 Auto Scaling:

More Instances

### Memory Trick

**OUT = ADD**

---

## Scaling In

Scale In means:

**Reduce capacity**

For ECS Service Auto Scaling:

Fewer Tasks

For EC2 Auto Scaling:

Fewer Instances

### Memory Trick

**IN = REMOVE**

---

## Minimum Capacity

Auto Scaling can define:

**Minimum task count**

Example:

Minimum = 2

Even during low traffic:

At least:

**2 tasks remain**

This can help maintain:

- Availability
- Baseline performance

---

## Maximum Capacity

Auto Scaling can define:

**Maximum task count**

Example:

Maximum = 20

Even during heavy traffic:

Auto Scaling will not exceed:

**20 tasks**

This can help control:

- Cost
- Resource consumption
- Scaling boundaries

---

## Desired Capacity

Desired capacity represents:

**The current target number of tasks**

It must generally remain within:

Minimum  
≤  
Desired  
≤  
Maximum

Example:

Min = 2

Desired = 6

Max = 20

---

## Cooldown Periods

Scaling systems need time to:

**Observe the effect of a scaling action**

Cooldown behavior helps prevent:

**Rapid repeated scaling actions**

Example:

Scale Out  
↓  
Wait for Tasks to Start  
↓  
Observe Metrics  
↓  
Decide Whether More Scaling Is Needed

The exam concept:

> **Avoid reacting too aggressively before previous scaling actions take effect.**

---

## Scaling During Deployments

During an ECS deployment:

Old Tasks  
+  
New Tasks

may temporarily run together.

The ECS service manages deployment configuration to maintain:

**Application availability**

Auto Scaling still needs to work alongside:

**Deployment behavior**

---

## High Availability + Scaling

A scalable ECS application should also be:

**Highly available**

Architecture:

ALB  
↓  
├── AZ-A → ECS Tasks
└── AZ-B → ECS Tasks

Scaling should add tasks across:

**Available infrastructure**

rather than concentrating everything into:

**One failure domain**

---

## Scaling + Spread Placement

For ECS on EC2:

**Spread**

can distribute tasks across:

- Availability Zones
- EC2 instances

Goal:

**Availability**

### Memory Trick

**SPREAD = HA**

---

## Scaling + Binpack

**Binpack**

attempts to place tasks using:

**As few EC2 instances as possible**

Goal:

**Resource utilization / cost efficiency**

### Memory Trick

**BINPACK = COST**

---

## Scaling and Persistent Storage

Scaling creates:

**Multiple interchangeable tasks**

Therefore application state should generally NOT depend on:

**A single task's local filesystem**

For shared persistent files:

→ [[EFS]]

For object storage:

→ [[S3]]

For application data:

→ Appropriate database service

### Exam Principle

> **Design scalable containers to be as stateless as practical.**

---

## Scaling + Sessions

If a web application stores user session state:

**Inside an individual container**

scaling can create problems.

Better architecture:

ECS Tasks  
↓  
External Shared Session Store

Potential service:

**ElastiCache**

This allows tasks to remain:

**Stateless and replaceable**

---

## Architecture Thinking

### Scenario 1 — CPU Spike

An ECS application runs on Fargate.

CPU increases significantly.

Need:

**Automatically add tasks**

Choose:

**ECS Service Auto Scaling**

---

### Scenario 2 — Predictable Morning Traffic

Traffic increases every weekday:

**At 8 AM**

Choose:

**Scheduled Scaling**

---

### Scenario 3 — Maintain 50% CPU

The application should automatically keep average CPU near:

**50%**

Choose:

**Target Tracking**

---

### Scenario 4 — Different Responses to Different CPU Levels

Requirement:

70% CPU  
→ Add 1

80% CPU  
→ Add 3

90% CPU  
→ Add 6

Choose:

**Step Scaling**

---

### Scenario 5 — Tasks Stuck Pending

ECS on EC2:

Desired = 20

Running = 10

Pending = 10

EC2 instances are fully utilized.

Choose:

**Scale EC2 cluster capacity**

using:

**Capacity Provider / Cluster Auto Scaling**

---

### Scenario 6 — Minimum Operations

Company needs:

- Automatic task scaling
- No EC2 capacity management

Choose:

**ECS + Fargate + Service Auto Scaling**

---

### Scenario 7 — HTTP Traffic Scaling

An ECS web application needs to scale based on:

**Requests reaching each target**

Choose:

**ALB Request Count Per Target**

---

### Scenario 8 — Cost-Optimized Fault-Tolerant Tasks

Tasks can tolerate interruption.

Need:

**Lower compute cost**

Choose:

**Fargate Spot**

---

### Scenario 9 — Scale Tasks but Not Servers

ECS Service Auto Scaling adds tasks.

New tasks remain:

**PENDING**

Why?

The EC2-backed cluster:

**Doesn't have enough capacity**

Need:

**Cluster scaling**

---

### Scenario 10 — Scale Servers but Not Tasks

ASG adds many EC2 instances.

Application traffic remains low.

ECS still runs:

**Only the desired task count**

Why?

EC2 scaling changes:

**Infrastructure capacity**

not:

**Application demand**

---

## Scenario Recognition

Immediately think:

**ECS Service Auto Scaling**

when you see:

- Scale tasks
- Desired task count
- CPU utilization
- Memory utilization
- ALB request count
- Target tracking
- Step scaling
- Scheduled scaling

---

## Think Capacity Provider / Cluster Scaling When You See

- ECS on EC2
- Pending tasks
- Insufficient cluster capacity
- EC2 Auto Scaling Group
- Automatically scale ECS hosts
- Managed scaling

---

## Think Fargate When You See

- No EC2 scaling
- Serverless containers
- Minimum operational overhead
- AWS manages infrastructure

---

## Exam Traps

### Trap 1 — ECS Service Auto Scaling Scales EC2 Instances

False.

It changes:

**Number of ECS tasks**

---

### Trap 2 — EC2 Auto Scaling Automatically Changes ECS Desired Task Count

False.

It changes:

**EC2 infrastructure**

---

### Trap 3 — More Tasks Can Always Start on ECS EC2

False.

There must be:

**Enough underlying EC2 capacity**

---

### Trap 4 — Fargate Requires an EC2 Auto Scaling Group

False.

AWS manages:

**The infrastructure**

---

### Trap 5 — Target Tracking Means Scale at a Specific Time

False.

Target Tracking:

**Maintains a metric target**

Scheduled Scaling:

**Uses known time patterns**

---

### Trap 6 — Step Scaling and Target Tracking Are the Same

False.

Target Tracking:

**Maintain target**

Step Scaling:

**Different scaling actions based on alarm magnitude**

---

### Trap 7 — Fargate Spot Is Appropriate for Any Critical Application

False.

Fargate Spot tasks can:

**Be interrupted**

Use them for:

**Fault-tolerant workloads**

---

### Trap 8 — Pending Tasks Always Mean Application Failure

False.

They may indicate:

**Insufficient compute capacity**

---

### Trap 9 — Scaling Stateful Containers Is Ideal

Usually not.

Scalable container architectures should favor:

**Stateless tasks + external state**

---

### Trap 10 — Desired Count and Maximum Count Are the Same

False.

Desired:

**Current target**

Maximum:

**Upper scaling boundary**

---

## Quick Cheat Sheet

| Exam Clue | Answer |
|---|---|
| Scale Number of ECS Tasks | ECS Service Auto Scaling |
| Maintain 50% CPU | Target Tracking |
| Different Scaling by Alarm Severity | Step Scaling |
| Predictable Traffic Schedule | Scheduled Scaling |
| Scale EC2 Hosts | EC2 Auto Scaling |
| Pending ECS Tasks | Check Cluster Capacity |
| Automatically Scale ECS EC2 Capacity | Capacity Provider |
| Serverless Container Scaling | Fargate |
| HTTP Request-Based Scaling | ALB Request Count Per Target |
| Fault-Tolerant Discounted Tasks | Fargate Spot |
| Minimum Tasks on Provider | Base |
| Relative Provider Distribution | Weight |

---

## Scaling Comparison

| Scaling Type | Changes |
|---|---|
| ECS Service Auto Scaling | Number of Tasks |
| EC2 Auto Scaling | Number of EC2 Instances |
| Capacity Provider Managed Scaling | ECS Cluster EC2 Capacity |
| Fargate Scaling | Tasks; AWS Handles Infrastructure |

---

## Scaling Policy Comparison

| Policy | Think |
|---|---|
| Target Tracking | Thermostat |
| Step Scaling | Severity Levels |
| Scheduled Scaling | Calendar / Clock |

---

## ECS on EC2 Scaling Flow

Traffic ↑  
↓  
Service Metric ↑  
↓  
ECS Service Auto Scaling  
↓  
More Tasks Requested  
↓  
Need More Cluster Capacity?  
↓  
Capacity Provider  
↓  
EC2 Auto Scaling Group  
↓  
More EC2 Instances  
↓  
Tasks Start

---

## Fargate Scaling Flow

Traffic ↑  
↓  
Service Metric ↑  
↓  
ECS Service Auto Scaling  
↓  
More Tasks  
↓  
AWS Provides Infrastructure

---

## Final Exam Rapid-Fire

> **MORE APPLICATION CAPACITY**
> → SCALE TASKS
>
> **MORE ECS EC2 CAPACITY**
> → SCALE INSTANCES
>
> **MAINTAIN 50% CPU**
> → TARGET TRACKING
>
> **DIFFERENT ACTIONS AT DIFFERENT THRESHOLDS**
> → STEP SCALING
>
> **KNOWN TRAFFIC TIME**
> → SCHEDULED SCALING
>
> **TASKS STUCK PENDING**
> → CHECK CLUSTER CAPACITY
>
> **AUTOMATIC ECS EC2 CAPACITY**
> → CAPACITY PROVIDER
>
> **NO EC2 CAPACITY MANAGEMENT**
> → FARGATE
>
> **LOW-COST INTERRUPTIBLE FARGATE**
> → FARGATE SPOT

---

## Master Memory Trick

> [!tip] ECS Auto Scaling Master Memory Trick
> Think of a restaurant.
>
> **ECS Tasks**
> → Cooks
>
> **ECS Service Auto Scaling**
> → Decides how many cooks are needed
>
> **EC2 Instances**
> → Kitchens
>
> **EC2 Auto Scaling**
> → Adds or removes kitchens
>
> **Capacity Provider**
> → Makes sure enough kitchens exist for the cooks
>
> **Fargate**
> → AWS automatically provides the kitchens

If customers increase:

More Customers  
↓  
Need More Cooks  
↓  
**Service Auto Scaling**

But if all kitchens are full:

Need More Kitchens  
↓  
**Cluster / EC2 Scaling**

With Fargate:

More Customers  
↓  
More Cooks  
↓  
**AWS handles the kitchen capacity**

So memorize:

> **SERVICE AUTO SCALING**
> → TASKS
>
> **CLUSTER AUTO SCALING**
> → EC2 CAPACITY
>
> **TARGET TRACKING**
> → MAINTAIN
>
> **STEP SCALING**
> → REACT BY SEVERITY
>
> **SCHEDULED SCALING**
> → PREDICT
>
> **FARGATE**
> → FORGET THE SERVERS

The killer SAA distinction:

> **"Do I need more containers, or do I need more machines to run those containers?"**
>
> More containers:
> → **ECS Service Auto Scaling**
>
> More machines:
> → **ECS Cluster / EC2 Auto Scaling**

---

## Related Notes

- [[ECS]]
- [[02-Compute/Fargate]]
- [[02-Compute/ECR]]
- [[Auto Scaling Groups]]
- [[Application Load Balancer]]
- [[07-Monitoring/CloudWatch]]
- [[EFS]]
- [[S3]]
- [[ElastiCache]]