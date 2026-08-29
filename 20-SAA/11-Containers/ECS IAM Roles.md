## Why This Matters

ECS IAM questions often test whether you know:

**Which role is used by the application**

versus:

**Which role is used by ECS itself**

The two main roles are:

- **ECS Task Role**
- **ECS Task Execution Role**

> [!tip] Master Memory Trick
> **TASK ROLE = APP PERMISSIONS**
>
> **EXECUTION ROLE = ECS STARTUP PERMISSIONS**

---

## ECS Task Role

The:

**ECS Task Role**

is assumed by:

**The application running inside the ECS task**

Use it when the containerized application needs permission to access AWS services.

Examples:

- [[S3]]
- DynamoDB
- [[SQS]]
- [[SNS]]
- Secrets Manager
- Systems Manager Parameter Store
- KMS
- Other AWS APIs

Architecture:

Application Container  
↓  
ECS Task Role  
↓  
AWS Service

### Killer Exam Clue

> **The application inside the container needs AWS API permissions**
>
> → **ECS Task Role**

---

## Example — Application Reads from S3

Containerized application needs:

`s3:GetObject`

Architecture:

ECS Task  
↓  
Task Role  
↓  
[[S3]]

Policy attached to:

**Task Role**

not:

**The EC2 instance role**

### SAA Principle

> Give permissions directly to the task that needs them.

This supports:

**Least privilege**

---

## Different Tasks Can Use Different Roles

Suppose three ECS services exist:

Orders Service  
↓  
Needs DynamoDB

Payments Service  
↓  
Needs KMS

Reporting Service  
↓  
Needs S3

Each can have:

**Its own Task Role**

Architecture:

Orders Task  
→ Orders Role  
→ DynamoDB

Payments Task  
→ Payments Role  
→ KMS

Reporting Task  
→ Reporting Role  
→ S3

This avoids giving every container:

**The same broad permissions**

---

## Why Not Use the EC2 Instance Role?

When ECS runs on:

**EC2**

the underlying EC2 instance also has an IAM role.

But that instance role should not automatically be used as:

**The application permission model**

Why?

Because multiple tasks may run on:

**The same EC2 host**

Example:

EC2 Instance  
↓  
├── Task A
├── Task B
└── Task C

If all permissions are placed on the EC2 instance role:

Every task may inherit access beyond:

**What it actually needs**

That violates:

**Least privilege**

---

## Task-Level Least Privilege

Better architecture:

Task A  
→ Role A

Task B  
→ Role B

Task C  
→ Role C

Each task receives:

**Only its required permissions**

### Memory Trick

**PER TASK = PERMISSION BOUNDARY**

---

## ECS Task Execution Role

The:

**ECS Task Execution Role**

is used by:

**ECS / the container runtime during task startup and operation**

It is not primarily for:

**The application code itself**

Common uses include:

- Pulling images from [[02-Compute/ECR]]
- Writing container logs to CloudWatch Logs
- Retrieving certain secrets or parameters needed during startup
- Other ECS-managed startup actions

### Killer Exam Clue

> **ECS needs permission to pull a private image or send logs**
>
> → **Task Execution Role**

---

## Example — Pull Image from ECR

Deployment flow:

ECS  
↓  
Task Execution Role  
↓  
[[02-Compute/ECR]]  
↓  
Pull Container Image  
↓  
Start Task

The application itself does NOT need:

**ECR pull permissions**

just because its image came from ECR.

Those permissions belong to:

**The execution role**

---

## Example — CloudWatch Logs

Container starts  
↓  
ECS Runtime  
↓  
Task Execution Role  
↓  
CloudWatch Logs

This allows ECS to:

**Send container logs**

to:

[[07-Monitoring/CloudWatch]]

### Exam Shortcut

**App accessing CloudWatch API itself**
→ Task Role

**ECS log driver sending task logs**
→ Execution Role

---

## Task Role vs Execution Role

| Role | Used By | Primary Purpose |
|---|---|---|
| Task Role | Application Code | Access AWS Services |
| Task Execution Role | ECS Runtime / Agent | Start and Operate Task |

### Memory Trick

**TASK ROLE**
→ What the container app can do

**EXECUTION ROLE**
→ What ECS needs to launch it

---

## Shared Example

Suppose a containerized app:

1. Pulls image from ECR
2. Writes logs to CloudWatch
3. Reads files from S3

Then:

ECR Pull  
→ **Execution Role**

CloudWatch Logging  
→ **Execution Role**

Application Reads S3  
→ **Task Role**

This is a very common exam-style distinction.

---

## Secrets Manager

Secrets can appear in two different patterns.

### Pattern 1 — Application Fetches Secret at Runtime

Application  
↓  
Task Role  
↓  
[[Secrets Manager]]

Use:

**Task Role**

because:

**The application is making the API call**

---

### Pattern 2 — ECS Injects Secret During Task Startup

ECS Task Startup  
↓  
Execution Role  
↓  
Secrets Manager / Parameter Store  
↓  
Secret Injected into Container

Think:

**Execution Role**

because:

**ECS is retrieving the secret during startup**

### Killer Rule

Ask:

> **WHO is calling AWS?**

Application?

→ Task Role

ECS runtime?

→ Execution Role

---

## Systems Manager Parameter Store

Same reasoning applies to:

**Parameter Store**

If application code calls Parameter Store:

→ Task Role

If ECS retrieves a parameter during startup:

→ Execution Role

---

## KMS Permissions

Encrypted resources may require:

**KMS permissions**

Again ask:

> **Who performs the decrypt operation?**

Application decrypting data:

→ Task Role

ECS retrieving an encrypted startup secret:

→ Execution Role may require KMS access

---

## ECS on EC2 Instance Role

When using:

**ECS on EC2**

the underlying EC2 instance can have its own:

**IAM instance profile**

This role supports:

**EC2/ECS infrastructure-level operations**

Do not confuse it with:

- Task Role
- Task Execution Role

---

## Three IAM Layers on ECS EC2

For ECS on EC2, conceptually:

### EC2 Instance Role

Used by:

**The host / ECS agent**

### Task Execution Role

Used for:

**Task startup operations**

### Task Role

Used by:

**Application code**

> [!tip] Memory Trick
> **HOST**
> → Instance Role
>
> **START**
> → Execution Role
>
> **APP**
> → Task Role

---

## Fargate IAM Roles

With [[02-Compute/Fargate]]:

You do NOT manage:

**EC2 instance roles**

because there are no customer-managed EC2 hosts.

You still commonly use:

- Task Role
- Task Execution Role

Architecture:

Fargate Task  
↓  
├── Task Role
└── Execution Role

---

## ECS IAM + Least Privilege

Best practice:

Give each application:

**Only the permissions it actually needs**

Avoid policies such as:

`Action: "*"`

and:

`Resource: "*"`

unless truly required.

### SAA Principle

> **Prefer task-specific roles over broad shared permissions**

---

## Cross-Account Access

If an ECS task needs to access a resource in:

**Another AWS account**

a common pattern is:

ECS Task Role  
↓  
AssumeRole  
↓  
Role in Target Account  
↓  
Resource

This requires:

- IAM permissions
- Trust relationship

### Exam Pattern

> **Container in Account A needs controlled access to resources in Account B**
>
> → **Task Role + Cross-Account Role Assumption**

---

## Resource Policies Still Matter

Some AWS services also use:

**Resource-based policies**

Examples:

- S3 bucket policies
- SQS queue policies
- KMS key policies

Even if the Task Role allows an action:

The resource policy may also need to:

**Permit access**

depending on the service and architecture.

---

## ECS IAM + SQS

Worker architecture:

SQS  
↓  
ECS Worker Task

Application needs to call:

- `ReceiveMessage`
- `DeleteMessage`

These permissions belong to:

**Task Role**

---

## ECS IAM + S3

Application:

ECS Task  
↓  
S3 Bucket

Permissions such as:

- `s3:GetObject`
- `s3:PutObject`

belong to:

**Task Role**

---

## ECS IAM + DynamoDB

Application:

ECS Task  
↓  
DynamoDB

Permissions such as:

- `dynamodb:GetItem`
- `dynamodb:PutItem`

belong to:

**Task Role**

---

## ECS IAM + ECR

Image startup:

ECS Runtime  
↓  
ECR

Permissions to:

**Pull private image**

belong to:

**Task Execution Role**

---

## ECS IAM + CloudWatch Logs

Container logging:

ECS Runtime  
↓  
CloudWatch Logs

Permissions to create/write log streams commonly belong to:

**Task Execution Role**

---

## ECS IAM + Secrets

Application retrieves database password itself:

→ Task Role

ECS injects database password during startup:

→ Execution Role

### Memory Trick

**RUNTIME APP CALL**
→ Task Role

**STARTUP ECS CALL**
→ Execution Role

---

## Architecture Thinking

### Scenario 1 — S3 Access

Application inside ECS must read objects from S3.

**Choose → Task Role**

---

### Scenario 2 — Pull Private ECR Image

ECS task cannot start because it lacks permission to pull its private image.

**Choose → Task Execution Role**

---

### Scenario 3 — Container Logs

ECS cannot send container logs to CloudWatch Logs.

**Check → Task Execution Role**

---

### Scenario 4 — DynamoDB

Application needs to write customer records into DynamoDB.

**Choose → Task Role**

---

### Scenario 5 — Secrets at Runtime

Application code calls Secrets Manager to retrieve credentials.

**Choose → Task Role**

---

### Scenario 6 — Secrets Injected at Startup

ECS task definition references a secret that ECS must retrieve before starting the container.

**Choose → Task Execution Role**

---

### Scenario 7 — Different Microservices

Orders, payments, and reporting containers need different AWS permissions.

**Choose → Separate Task Roles**

---

### Scenario 8 — ECS on EC2 Host Operations

The underlying ECS container instance needs infrastructure permissions.

Think:

**EC2 Instance Role**

not:

Task Role

---

### Scenario 9 — Fargate

A Fargate application needs access to S3.

Choose:

**Task Role**

There is no customer-managed:

**EC2 instance role**

---

### Scenario 10 — Cross-Account Resource

ECS application needs access to a resource in another account.

Think:

**Task Role + AssumeRole / Resource Policy**

depending on architecture.

---

## Scenario Recognition

Immediately think:

**Task Role**

when you see:

- Application needs S3
- App needs DynamoDB
- App needs SQS
- App needs SNS
- App calls Secrets Manager
- App calls KMS
- App calls AWS APIs

---

## Immediately Think Execution Role When You See

- Pull ECR image
- Start task
- ECS startup
- CloudWatch log delivery
- Secret injection at startup
- Parameter injection at startup

---

## Immediately Think EC2 Instance Role When You See

- ECS on EC2
- Host-level permissions
- ECS agent / container instance operations

---

## Exam Traps

### Trap 1 — Task Role Pulls Images From ECR

False.

That is typically:

**Task Execution Role**

---

### Trap 2 — Execution Role Gives Application Access to S3

Wrong role.

Application access:

**Task Role**

---

### Trap 3 — EC2 Instance Role Should Contain All Application Permissions

Bad architecture.

Use:

**Task Roles**

for per-application permissions.

---

### Trap 4 — Fargate Requires an EC2 Instance Profile

False.

You do not manage:

**EC2 hosts**

---

### Trap 5 — Task Role and Execution Role Are the Same Role

They can technically be configured broadly, but conceptually they serve:

**Different purposes**

For the exam:

Treat them separately.

---

### Trap 6 — Secret Access Always Means Task Role

Not always.

Ask:

**Who retrieves the secret?**

App  
→ Task Role

ECS during startup  
→ Execution Role

---

### Trap 7 — IAM Policy Alone Always Guarantees Cross-Account Access

False.

Cross-account scenarios may also require:

- Trust policies
- Resource policies
- KMS key policies

---

### Trap 8 — Every ECS Service Should Share One Task Role

Not ideal.

Separate roles help enforce:

**Least privilege**

---

## Quick Cheat Sheet

| Exam Clue | Role |
|---|---|
| App Reads S3 | Task Role |
| App Writes DynamoDB | Task Role |
| App Polls SQS | Task Role |
| App Publishes SNS | Task Role |
| App Calls Secrets Manager | Task Role |
| ECS Pulls ECR Image | Execution Role |
| ECS Sends Container Logs | Execution Role |
| ECS Injects Startup Secret | Execution Role |
| ECS EC2 Host Permissions | EC2 Instance Role |
| Fargate App AWS Access | Task Role |

---

## Role Decision Tree

Who needs permission?  
↓

Application code?

→ **Task Role**

ECS needs permission to start/manage task startup?

→ **Task Execution Role**

Underlying ECS EC2 host?

→ **EC2 Instance Role**

---

## Three-Role Comparison

| Role | Applies To | Think |
|---|---|---|
| Task Role | Application | APP |
| Task Execution Role | Task Startup / Runtime Infrastructure | START |
| EC2 Instance Role | ECS EC2 Host | HOST |

---

## Final Exam Rapid-Fire

> **APP → S3**
> → TASK ROLE
>
> **APP → DYNAMODB**
> → TASK ROLE
>
> **APP → SQS**
> → TASK ROLE
>
> **APP → SECRETS MANAGER**
> → TASK ROLE
>
> **ECS → ECR IMAGE**
> → EXECUTION ROLE
>
> **ECS → CLOUDWATCH LOGS**
> → EXECUTION ROLE
>
> **ECS → STARTUP SECRET**
> → EXECUTION ROLE
>
> **ECS EC2 HOST**
> → INSTANCE ROLE
>
> **FARGATE APP PERMISSIONS**
> → TASK ROLE

---

## Master Memory Trick

> [!tip] ECS IAM Master Memory Trick
> Imagine a restaurant.
>
> **Chef**
> → Application
>
> **Task Role**
> → What the chef is allowed to access
>
> Maybe:
>
> - Pantry
> - Safe
> - Inventory system
>
> **Restaurant Setup Crew**
> → ECS runtime
>
> **Execution Role**
> → What the setup crew needs to prepare the station
>
> Maybe:
>
> - Retrieve ingredients
> - Open the workstation
> - Connect logging
>
> **Building Manager**
> → EC2 host
>
> **Instance Role**
> → What the building infrastructure needs

So remember:

> **APP**
> → TASK ROLE
>
> **START**
> → EXECUTION ROLE
>
> **HOST**
> → INSTANCE ROLE

And the single best exam question:

> **"WHO is making the AWS API call?"**

If:

**Application**
→ Task Role

If:

**ECS startup/runtime infrastructure**
→ Task Execution Role

If:

**Underlying ECS EC2 host**
→ Instance Role

---

## Related Notes

- [[ECS]]
- [[ECS Auto Scaling]]
- [[ECS Solutions Architectures]]
- [[02-Compute/Fargate]]
- [[02-Compute/ECR]]
- [[IAM]]
- [[S3]]
- [[SQS]]
- [[SNS]]
- [[Secrets Manager]]
- [[06-Security/KMS]]
- [[07-Monitoring/CloudWatch]]