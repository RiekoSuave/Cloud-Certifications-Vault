## What Problem Does It Solve?

[[Step Functions]] is AWS's:

**Serverless workflow orchestration service**

It coordinates multiple application steps into:

**A managed workflow**

Architecture:

Start  
↓  
Task A  
↓  
Decision  
↓  
Task B / Task C  
↓  
Wait / Retry  
↓  
Finish

> [!tip] Memory Trick
> **Step Functions = Workflow Manager**
>
> **Lambda does the work**
>
> **Step Functions decides what happens next**

---

## Core Concept

Without Step Functions:

Lambda A  
↓  
Calls Lambda B  
↓  
Calls Lambda C  
↓  
Custom Retry Logic  
↓  
Custom Error Handling

This can become:

**Tightly coupled and difficult to manage**

With Step Functions:

Step Functions  
↓  
Lambda A  
↓  
Decision  
↓  
Lambda B  
↓  
Retry / Catch  
↓  
Lambda C

The workflow logic is moved into:

**A managed state machine**

---

## State Machine

A Step Functions workflow is called a:

**State Machine**

It defines:

- Tasks
- Decisions
- Parallel branches
- Wait periods
- Retries
- Error handling
- Workflow transitions

### Memory Trick

**State Machine = Workflow Blueprint**

---

## States

A state machine contains:

**States**

Each state represents:

**One step in the workflow**

Examples:

- Task
- Choice
- Wait
- Parallel
- Map
- Pass
- Succeed
- Fail

---

# Task State

A:

**Task State**

performs:

**Work**

It can invoke AWS services such as:

- [[Lambda]]
- ECS
- Fargate
- Batch
- SNS
- SQS
- DynamoDB
- Other supported AWS integrations

Architecture:

Task State  
↓  
AWS Service  
↓  
Result  
↓  
Next State

### Killer Exam Clue

> **Workflow needs to invoke an AWS service as one step**
>
> → **Task State**

---

# Choice State

A:

**Choice State**

adds:

**Conditional branching**

Example:

Order Amount  
↓  
Choice

If:

Amount > $10,000  
→ Manual Review

Else  
→ Auto Approve

### Memory Trick

**Choice = IF / ELSE**

---

# Wait State

A:

**Wait State**

pauses execution for:

- A number of seconds
- A specific timestamp

Architecture:

Task  
↓  
Wait 1 Hour  
↓  
Next Task

### Killer Exam Clue

> **Workflow must pause before continuing**
>
> → **Wait State**

---

# Parallel State

A:

**Parallel State**

runs multiple workflow branches:

**At the same time**

Example:

Order Received  
↓  
Parallel  
├── Charge Payment
├── Reserve Inventory
└── Send Confirmation

The workflow can wait until:

**All parallel branches complete**

### Memory Trick

**Parallel = Do Multiple Things Together**

---

# Map State

A:

**Map State**

runs the same processing logic for:

**Multiple items**

Example:

List of 1,000 Files  
↓  
Map  
↓  
Process Each File

This is useful for:

- Batch processing
- Repeating workflow logic
- Processing arrays
- Large datasets

### Memory Trick

**Map = FOR EACH**

---

# Pass State

A:

**Pass State**

passes input to output without doing:

**Actual work**

It can help:

- Transform workflow data
- Insert fixed values
- Test workflows

---

# Succeed State

A:

**Succeed State**

ends the workflow successfully.

Think:

**Workflow Complete ✅**

---

# Fail State

A:

**Fail State**

ends the workflow as:

**Failed**

Think:

**Workflow Complete ❌**

---

# Step Functions + Lambda

This is the classic architecture:

Step Functions  
↓  
Lambda A  
↓  
Lambda B  
↓  
Lambda C

Each Lambda function handles:

**A focused piece of work**

Step Functions handles:

- Order
- State
- Retry
- Error paths
- Branching

### Killer Exam Pattern

> **Coordinate multiple Lambda functions with branching and retries**
>
> → **Step Functions**

---

# Why Not Chain Lambdas Directly?

Direct chaining:

Lambda A  
↓  
Lambda B  
↓  
Lambda C

can create:

- Tight coupling
- Harder troubleshooting
- Custom retry logic
- Complex error handling
- Longer function duration
- Difficult workflow visualization

Step Functions provides:

**Managed orchestration**

---

# Retry

Step Functions supports:

**Automatic retry policies**

Example:

Task  
↓  
Failure  
↓  
Wait  
↓  
Retry

You can configure concepts such as:

- Error types
- Retry attempts
- Backoff behavior

### Killer Exam Clue

> **Workflow task should automatically retry when it temporarily fails**
>
> → **Step Functions Retry**

---

# Exponential Backoff

Retry policies can use:

**Backoff**

to increase delay between retries.

Concept:

Attempt 1  
↓  
Wait

Attempt 2  
↓  
Wait Longer

Attempt 3

This helps avoid:

**Hammering a failing dependency**

---

# Catch

A:

**Catch**

handles errors after:

**A task fails**

Architecture:

Task  
↓  
Failure  
↓  
Catch  
↓  
Recovery State

Example:

Charge Card  
↓  
Fails  
↓  
Catch  
↓  
Notify Customer

### Memory Trick

**Retry = Try Again**

**Catch = Do Something Else**

---

# Retry vs Catch

| Feature | Purpose |
|---|---|
| Retry | Attempt task again |
| Catch | Handle failure path |

### Killer Exam Shortcut

Temporary failure?

→ Retry

Permanent / handled failure?

→ Catch

---

# Built-In Error Handling

One of Step Functions' biggest advantages is:

**Workflow-level error handling**

Instead of writing retry logic in every Lambda:

Step Functions can centrally define:

- Retry
- Catch
- Timeout
- Failure paths

This makes workflows:

**Easier to reason about**

---

# Workflow State

Step Functions keeps track of:

**Workflow execution state**

This means individual Lambda functions do not need to store:

**Which step comes next**

### Memory Trick

**Lambda = Stateless Worker**

**Step Functions = Remembers Workflow State**

---

# Standard Workflows

Step Functions supports:

**Standard Workflows**

Best for:

- Long-running workflows
- Durable execution
- Auditable workflows
- Exactly-once workflow execution semantics
- Complex business processes

Standard Workflows can run for:

**Up to one year**

### Killer Exam Clue

> **Long-running durable workflow lasting hours, days, or months**
>
> → **Standard Workflow**

---

# Express Workflows

Step Functions also supports:

**Express Workflows**

Best for:

- High-volume
- Short-duration
- Event-processing workloads
- High-throughput workflows

They are designed for:

**Much shorter execution durations**

than Standard Workflows.

### Memory Trick

**STANDARD = Long + Durable**

**EXPRESS = Fast + High Volume**

---

# Standard vs Express

| Requirement | Standard | Express |
|---|---:|---:|
| Long-Running | ✅ | ❌ |
| Up to One Year | ✅ | ❌ |
| High-Volume Events | Possible | ✅ |
| Detailed Execution History | ✅ | More Limited |
| Business Workflow | ✅ | Possible |
| Short High-Throughput Workflow | ❌ Best Fit | ✅ |

### Killer Exam Shortcut

**Long-running business process**
→ Standard

**High-volume short workflow**
→ Express

---

# Standard Workflow Execution Semantics

Standard Workflows are associated with:

**Exactly-once workflow execution semantics**

This is useful when duplicate workflow execution would be:

**Problematic**

---

# Express Workflow Execution Semantics

Express Workflows are designed for:

**High-volume event workloads**

Their delivery/execution semantics differ depending on:

**Synchronous vs asynchronous Express execution**

For SAA, the key distinction is:

> **Express emphasizes throughput and short duration**
>
> **Standard emphasizes durability and long-running workflows**

---

# Synchronous Express Workflows

Express workflows can support:

**Synchronous execution**

where the caller waits for:

**The workflow result**

This is useful for:

**High-volume synchronous workflows**

---

# Asynchronous Express Workflows

Express workflows can also run:

**Asynchronously**

for high-volume background workflows.

---

# Step Functions Service Integrations

Step Functions can directly integrate with many AWS services.

Examples:

- Lambda
- ECS
- Fargate
- Batch
- DynamoDB
- SNS
- SQS
- Glue
- SageMaker
- EventBridge

### SAA Principle

> **You do not always need Lambda just to call another AWS service**

---

# Direct Service Integration

Instead of:

Step Functions  
↓  
Lambda  
↓  
DynamoDB

you may sometimes use:

Step Functions  
↓  
DynamoDB

This can reduce:

- Code
- Lambda invocations
- Operational complexity

### Killer Exam Clue

> **Workflow only needs to call an AWS service API**
>
> → Consider **Step Functions direct service integration**

---

# Integration Patterns

Step Functions supports different ways of interacting with tasks.

Important concepts include:

- Request/Response
- Run a Job
- Wait for Callback

---

# Request/Response Pattern

Step Functions sends request:

↓  

AWS service responds:

↓  

Workflow continues.

Think:

**Normal synchronous API call**

---

# Run a Job Pattern

Step Functions starts a job and waits until:

**The job finishes**

Examples can include:

- Batch jobs
- ECS tasks
- Glue jobs

Architecture:

Start Job  
↓  
Wait for Completion  
↓  
Continue Workflow

### Killer Exam Clue

> **Workflow should wait until an ECS/Batch job finishes**
>
> → **Run a Job integration**

---

# Wait for Callback Pattern

Some workflows involve:

**External systems or humans**

Step Functions can start work and wait for:

**A callback token**

Architecture:

Step Functions  
↓  
Send Task + Token  
↓  
External System / Human  
↓  
Callback  
↓  
Workflow Continues

### Killer Exam Clue

> **Workflow must pause until an external process explicitly signals completion**
>
> → **Wait for Callback / Task Token**

---

# Human Approval Workflow

Example:

Expense Request  
↓  
Step Functions  
↓  
Send Approval Request  
↓  
Wait for Human  
↓  
Approved?

Yes  
→ Continue

No  
→ Reject

This is a classic use of:

**Callback-style workflows**

---

# Step Functions + EventBridge

[[20-SAA/10-Messaging/EventBridge]] can start:

**Step Functions workflows**

Architecture:

Business Event  
↓  
EventBridge  
↓  
Step Functions  
↓  
Workflow

### Killer Exam Clue

> **A business event should launch a multi-step serverless workflow**
>
> → **EventBridge + Step Functions**

---

# Step Functions + API Gateway

Architecture:

Client  
↓  
[[API Gateway]]  
↓  
Step Functions  
↓  
Workflow

This can be used when an API request needs to start:

**A managed workflow**

---

# Step Functions + SQS

A workflow can:

- Send an SQS message
- Wait on task-token patterns
- Coordinate queue-based work

Architecture:

Step Functions  
↓  
[[SQS]]  
↓  
Worker

Use SQS when you also need:

**Buffering and decoupling**

---

# Step Functions + SNS

A workflow can publish:

**Notifications**

to:

[[SNS]]

Example:

Workflow Failure  
↓  
SNS  
↓  
Operations

---

# Step Functions + ECS / Fargate

Step Functions can start:

**Container workloads**

Architecture:

Step Functions  
↓  
ECS / [[Fargate]]  
↓  
Container Job  
↓  
Continue

This is especially useful when a workflow step:

**Cannot fit within Lambda's 15-minute runtime**

---

# Step Functions + Batch

For compute-intensive or batch-processing workflows:

Step Functions  
↓  
AWS Batch  
↓  
Job  
↓  
Continue

This separates:

**Workflow orchestration**

from:

**Compute execution**

---

# Step Functions vs Lambda

### [[Lambda]]

Think:

**Perform one unit of compute**

### Step Functions

Think:

**Coordinate multiple units of work**

### Memory Trick

**Lambda = Worker**

**Step Functions = Manager**

---

# Step Functions vs SQS

### [[SQS]]

Think:

- Queue
- Buffer
- Backpressure
- Decoupling

### Step Functions

Think:

- Workflow
- Order
- State
- Branching
- Retry
- Coordination

### Exam Shortcut

**Work must wait**
→ SQS

**Steps must be coordinated**
→ Step Functions

---

# Step Functions vs EventBridge

### [[20-SAA/10-Messaging/EventBridge]]

Think:

**Route events**

### Step Functions

Think:

**Orchestrate workflows**

Together:

Event  
↓  
EventBridge  
↓  
Step Functions  
↓  
Workflow

### Memory Trick

**EventBridge = Which workflow?**

**Step Functions = What happens inside it?**

---

# Step Functions vs SWF

AWS Simple Workflow Service is an older workflow technology.

For modern serverless workflow orchestration:

Think:

**Step Functions**

unless the scenario explicitly requires:

**SWF-specific capabilities**

---

# Visual Workflow

Step Functions provides:

**Visual workflow execution**

This makes it easier to inspect:

- Current state
- Completed states
- Errors
- Branches
- Retry paths

This improves:

**Troubleshooting**

compared with manually chained Lambda functions.

---

# Execution History

Standard workflows maintain:

**Detailed execution history**

This helps with:

- Auditing
- Debugging
- Troubleshooting
- Business process visibility

---

# Step Functions and IAM

Step Functions needs permissions to:

**Invoke the services used by workflow tasks**

Example:

Step Functions  
↓  
IAM Role  
↓  
Lambda

The role may need:

`lambda:InvokeFunction`

### SAA Principle

> **Step Functions requires IAM permissions for the services it orchestrates**

---

# Step Functions Logging

Workflows can integrate with:

[[07-Monitoring/CloudWatch]]

for:

- Logging
- Metrics
- Monitoring
- Alarms

This helps detect:

- Failed executions
- Long runtimes
- Workflow errors

---

# Step Functions + X-Ray

Step Functions can integrate with:

AWS X-Ray

for:

**Distributed tracing**

This helps visualize requests across:

**Multiple workflow components**

---

# Architecture Thinking

## Scenario 1 — Three Lambda Functions

Application must:

1. Validate order
2. Charge payment
3. Send confirmation

Need:

- Retry
- Error handling
- State tracking

Choose:

**Step Functions**

---

## Scenario 2 — Conditional Workflow

If payment succeeds:

Ship order

If payment fails:

Notify customer

Choose:

**Choice State**

---

## Scenario 3 — Parallel Work

After order placement:

- Reserve inventory
- Calculate shipping
- Run fraud check

should happen simultaneously.

Choose:

**Parallel State**

---

## Scenario 4 — Process 10,000 Files

Need the same workflow logic applied to:

**Many files**

Choose:

**Map State**

---

## Scenario 5 — Wait 24 Hours

Workflow should:

**Pause for one day**

before checking payment status.

Choose:

**Wait State**

---

## Scenario 6 — Temporary API Failure

External service occasionally returns:

**Transient errors**

Choose:

**Retry**

with backoff.

---

## Scenario 7 — Permanent Failure

After retries fail:

Send notification.

Choose:

**Catch**

---

## Scenario 8 — Human Approval

Workflow must stop until:

**A manager approves**

Choose:

**Callback / Task Token Pattern**

---

## Scenario 9 — 3-Day Workflow

Business approval process can take:

**Several days**

Choose:

**Standard Workflow**

---

## Scenario 10 — Millions of Short Events

Need:

**Very high-throughput, short-duration workflow execution**

Choose:

**Express Workflow**

---

## Scenario 11 — 30-Minute Container Job

Workflow step takes:

30 minutes.

Do NOT use Lambda for that step.

Choose:

Step Functions  
↓  
ECS / Fargate

---

## Scenario 12 — AWS Service API Call

Workflow needs only to:

**Write an item to DynamoDB**

Do not automatically add Lambda.

Consider:

**Direct DynamoDB service integration**

---

# Scenario Recognition

Immediately think:

**Step Functions**

when you see:

- Workflow orchestration
- State machine
- Multiple Lambda functions
- Branching
- Retry
- Catch
- Wait
- Parallel processing
- Human approval
- Long-running workflow
- Visual workflow

---

## Think Standard Workflow When You See

- Hours/days/months
- Durable execution
- Auditing
- Business process
- Exactly-once workflow semantics

---

## Think Express Workflow When You See

- High volume
- Short duration
- Event processing
- Very high throughput

---

# Exam Traps

## Trap 1 — Lambda Should Coordinate Every Multi-Step Workflow Itself

❌

Think:

**Step Functions**

---

## Trap 2 — Step Functions Is a Queue

❌

Queue:

**SQS**

Workflow orchestration:

**Step Functions**

---

## Trap 3 — Step Functions Only Works with Lambda

❌

It supports:

**Many AWS service integrations**

---

## Trap 4 — Every Service Call Requires an Intermediate Lambda

❌

Use:

**Direct service integrations**

when appropriate.

---

## Trap 5 — Retry and Catch Mean the Same Thing

❌

Retry:

**Try again**

Catch:

**Follow failure path**

---

## Trap 6 — Standard and Express Have the Same Use Case

❌

Standard:

**Long + durable**

Express:

**Short + high volume**

---

## Trap 7 — Lambda's 15-Minute Limit Means Step Functions Workflows Must Finish in 15 Minutes

❌

The Lambda step has the limit.

The overall workflow can be:

**Much longer**

---

## Trap 8 — Wait State Consumes a Running Lambda While Waiting

❌

Step Functions manages:

**The workflow wait**

without keeping a Lambda function executing.

---

## Trap 9 — Human Approval Requires a Lambda to Poll Continuously

❌

Use:

**Callback / Task Token Pattern**

---

# Quick Cheat Sheet

| Exam Clue | Answer |
|---|---|
| Serverless Workflow Orchestration | Step Functions |
| Conditional Branching | Choice |
| Pause Workflow | Wait |
| Parallel Branches | Parallel |
| Process Each Item | Map |
| Retry Temporary Failure | Retry |
| Handle Failure Path | Catch |
| Human / External Callback | Task Token |
| Long Durable Workflow | Standard |
| Short High-Volume Workflow | Express |
| Invoke Lambda | Task |
| Long Container Job | ECS/Fargate Integration |
| Direct AWS API Call | Service Integration |
| Event Starts Workflow | EventBridge + Step Functions |

---

# State Cheat Sheet

| State | Think |
|---|---|
| Task | DO |
| Choice | IF / ELSE |
| Wait | PAUSE |
| Parallel | AT SAME TIME |
| Map | FOR EACH |
| Pass | MOVE DATA |
| Succeed | DONE ✅ |
| Fail | DONE ❌ |

---

# Standard vs Express Decision

Need:

**Long-running durable business workflow**

→ Standard

Need:

**Detailed execution history**

→ Standard

Need:

**Very high-volume short workflow**

→ Express

Need:

**Fast event-processing workflow**

→ Express

---

# Orchestration Decision

Need:

**Run one piece of code**

→ Lambda

Need:

**Hold work**

→ SQS

Need:

**Route event**

→ EventBridge

Need:

**Coordinate many steps**

→ Step Functions

---

# Final Exam Rapid-Fire

> **MULTI-STEP WORKFLOW**
> → STEP FUNCTIONS
>
> **IF / ELSE**
> → CHOICE
>
> **PAUSE**
> → WAIT
>
> **RUN BRANCHES TOGETHER**
> → PARALLEL
>
> **FOR EACH ITEM**
> → MAP
>
> **TRY AGAIN**
> → RETRY
>
> **HANDLE FAILURE**
> → CATCH
>
> **HUMAN APPROVAL**
> → CALLBACK / TASK TOKEN
>
> **LONG DURABLE WORKFLOW**
> → STANDARD
>
> **HIGH-VOLUME SHORT WORKFLOW**
> → EXPRESS
>
> **ONE COMPUTE TASK**
> → LAMBDA
>
> **QUEUE**
> → SQS
>
> **EVENT ROUTING**
> → EVENTBRIDGE
>
> **30-MINUTE CONTAINER STEP**
> → ECS / FARGATE
>
> **DIRECT AWS SERVICE CALL**
> → SERVICE INTEGRATION

---

## Master Memory Trick

> [!tip] Step Functions Master Memory Trick
> Imagine a project manager coordinating a team.
>
> The workers are:
>
> **Lambda / ECS / AWS Services**
>
> The project manager is:
>
> **STEP FUNCTIONS**
>
> The manager says:
>
> **DO THIS**
> → Task
>
> **IF THIS, DO THAT**
> → Choice
>
> **WAIT UNTIL TOMORROW**
> → Wait
>
> **DO THESE TOGETHER**
> → Parallel
>
> **DO THIS FOR EVERY ITEM**
> → Map
>
> **TRY AGAIN**
> → Retry
>
> **IF IT STILL FAILS, DO THIS**
> → Catch

So remember:

> **LAMBDA**
> → WORKER
>
> **STEP FUNCTIONS**
> → MANAGER
>
> **SQS**
> → WAITING LINE
>
> **EVENTBRIDGE**
> → DISPATCHER
>
> **STANDARD**
> → LONG + DURABLE
>
> **EXPRESS**
> → FAST + HIGH VOLUME

And the killer SAA question:

> **"Does the application need to coordinate multiple steps with state, branching, retries, or waiting?"**
>
> YES
>
> → **Step Functions**

---

## Related Notes

- [[Lambda]]
- [[API Gateway]]
- [[20-SAA/10-Messaging/EventBridge]]
- [[SQS]]
- [[SNS]]
- [[ECS]]
- [[Fargate]]
- [[DynamoDB]]
- [[07-Monitoring/CloudWatch]]