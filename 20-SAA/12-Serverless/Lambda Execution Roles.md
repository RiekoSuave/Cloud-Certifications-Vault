## What Problem Does It Solve?

A [[Lambda]] function often needs to interact with:

**Other AWS services**

Examples:

Lambda  
→ Read an S3 object

Lambda  
→ Write to DynamoDB

Lambda  
→ Send an SQS message

Lambda  
→ Retrieve a secret

Lambda needs:

**IAM permissions**

to perform those actions.

Those permissions are provided through the:

**Lambda Execution Role**

> [!tip] Memory Trick
> **Execution Role = What Lambda is allowed to DO**
>
> Think:
>
> **LAMBDA → AWS SERVICE**

---

## Core Concept

When Lambda runs:

Lambda Function  
↓  
Assumes Execution Role  
↓  
Receives Temporary Credentials  
↓  
Calls AWS Services

The execution role is an:

**IAM Role**

associated with the function.

---

## Example

Suppose Lambda needs to:

**Read objects from S3**

Architecture:

Lambda  
↓  
Execution Role  
↓  
`s3:GetObject`  
↓  
[[S3]]

Without the required permission:

**Access Denied**

---

# Least Privilege

The execution role should contain:

**Only the permissions the function actually needs**

Example:

Lambda only needs:

`GetObject`

from:

`my-images-bucket`

Prefer:

**Specific S3 read permissions**

instead of:

**AdministratorAccess**

### SAA Principle

> **Always prefer least privilege**

---

# Lambda Basic Execution Role

A Lambda function commonly needs permission to:

**Write logs to CloudWatch Logs**

AWS provides a managed policy commonly used for this purpose:

**AWSLambdaBasicExecutionRole**

It allows Lambda to perform logging actions such as:

- Create log group
- Create log stream
- Put log events

Architecture:

Lambda  
↓  
Execution Role  
↓  
[[07-Monitoring/CloudWatch]] Logs

### Memory Trick

**BASIC EXECUTION ROLE = LOGGING**

---

# Lambda + CloudWatch Logs

When Lambda runs:

Function Output  
↓  
CloudWatch Logs

This allows you to inspect:

- Application logs
- Errors
- Debug output
- Invocation behavior

The execution role must have:

**Appropriate CloudWatch Logs permissions**

---

# Lambda + S3

Suppose Lambda processes uploaded images.

Architecture:

[[S3]]  
↓  
Lambda  
↓  
Execution Role  
↓  
S3

The execution role may need:

- `s3:GetObject`
- `s3:PutObject`

depending on:

**What the function does**

---

# Lambda + DynamoDB

Architecture:

API Gateway  
↓  
Lambda  
↓  
Execution Role  
↓  
DynamoDB

The execution role may allow:

- `GetItem`
- `PutItem`
- `UpdateItem`
- `Query`

depending on application requirements.

### Killer Exam Clue

> **Lambda needs to write to DynamoDB**
>
> → **Grant DynamoDB permission to Lambda execution role**

---

# Lambda + SQS

Lambda may need to:

**Send messages to an SQS queue**

Architecture:

Lambda  
↓  
Execution Role  
↓  
[[SQS]]

Example permission:

`SendMessage`

### Important Distinction

If Lambda is:

**Sending a message to SQS**

think:

**Execution Role**

If Lambda is:

**Processing messages from SQS**

the integration uses:

**Event Source Mapping**

with the required permissions to poll the queue.

---

# Lambda + SNS

Lambda can publish messages to:

[[SNS]]

Architecture:

Lambda  
↓  
Execution Role  
↓  
SNS Topic

The role needs permission such as:

**Publish**

to the appropriate topic.

---

# Lambda + Secrets Manager

Lambda should not hardcode:

- Database passwords
- API credentials
- Tokens

Instead:

Lambda  
↓  
Execution Role  
↓  
[[Secrets Manager]]  
↓  
Secret

The role needs:

**Permission to retrieve the required secret**

### SAA Principle

> **Credentials belong in a secure secrets service, not application code**

---

# Lambda + KMS

If Lambda accesses encrypted resources:

[[06-Security/KMS]] permissions may also be required.

Architecture:

Lambda  
↓  
Execution Role  
↓  
KMS  
↓  
Decrypt

### Exam Clue

> **Lambda receives AccessDenied when trying to decrypt KMS-encrypted data**
>
> Check:
>
> - IAM permissions
> - KMS key policy

---

# Lambda + VPC

When Lambda connects to resources inside a VPC:

Lambda  
↓  
VPC Networking  
↓  
Private Resource

the execution role needs appropriate permissions related to:

**Managing the networking interfaces required for VPC connectivity**

AWS provides managed policies that can help provide:

**The required VPC access permissions**

---

# Execution Role vs Resource-Based Policy

This distinction is extremely important.

## Execution Role

Controls:

**What Lambda can access**

Direction:

Lambda  
→ AWS Service

---

## Resource-Based Policy

Controls:

**Who can invoke Lambda**

Direction:

AWS Service / Principal  
→ Lambda

### Master Memory Trick

> **EXECUTION ROLE**
> → Lambda goes OUT
>
> **RESOURCE POLICY**
> → Caller comes IN

---

# Example — S3 Invokes Lambda

Architecture:

S3  
↓  
Lambda  
↓  
DynamoDB

Two separate permission questions exist.

### Question 1

Can S3 invoke Lambda?

Think:

**Lambda Resource-Based Policy**

### Question 2

Can Lambda write to DynamoDB?

Think:

**Lambda Execution Role**

---

# Example — API Gateway Invokes Lambda

Architecture:

Client  
↓  
[[API Gateway]]  
↓  
Lambda  
↓  
DynamoDB

Permission flow:

API Gateway  
→ Lambda

requires:

**Invocation permission**

Lambda  
→ DynamoDB

requires:

**Execution Role permission**

### Killer Exam Distinction

> **WHO CAN CALL LAMBDA?**
>
> Resource-based policy
>
> **WHAT CAN LAMBDA CALL?**
>
> Execution role

---

# Lambda Resource-Based Policies

Lambda supports:

**Resource-based policies**

These can grant invocation permissions to:

- AWS services
- AWS accounts
- Other principals

Examples:

- S3
- SNS
- API Gateway
- EventBridge

---

# Cross-Account Invocation

Suppose:

Account A  
↓  
Lambda in Account B

The Lambda resource policy can allow:

**Account A**

to invoke the function.

Depending on the scenario:

**The caller also needs appropriate identity-based permissions**

### Exam Principle

Cross-account access commonly requires evaluating:

**Both sides of the authorization relationship**

---

# Lambda Execution Role Trust Policy

The execution role needs a:

**Trust Policy**

allowing:

**Lambda service**

to assume the role.

Conceptually:

Lambda Service  
↓  
AssumeRole  
↓  
Execution Role

The service principal is associated with:

**Lambda**

---

# Trust Policy vs Permissions Policy

An IAM role contains two important concepts.

## Trust Policy

Answers:

**Who can assume this role?**

For Lambda execution roles:

→ Lambda service

---

## Permissions Policy

Answers:

**What can the role do after it is assumed?**

Examples:

- Read S3
- Write DynamoDB
- Publish SNS

### Memory Trick

**TRUST = WHO GETS THE ROLE**

**PERMISSIONS = WHAT ROLE CAN DO**

---

# Temporary Credentials

Lambda does not need:

**Hardcoded access keys**

to use its execution role.

AWS provides:

**Temporary credentials**

to the execution environment.

### Exam Trap

Do NOT:

- Store IAM access keys in Lambda code
- Put permanent credentials in environment variables

Instead:

**Use an IAM execution role**

---

# Lambda Environment Variables and Credentials

Environment variables are useful for:

- Bucket names
- Table names
- Configuration
- Environment settings

They should NOT be your default mechanism for storing:

**Long-term AWS access keys**

Use:

**IAM Roles**

for AWS service access.

---

# Multiple Functions and IAM

Suppose:

Lambda A needs:

S3 read access

Lambda B needs:

DynamoDB write access

Best practice:

**Give each function the permissions it needs**

rather than giving both functions:

**One broad administrative role**

### SAA Principle

> **Separate roles can improve least privilege**

---

# Lambda + RDS

If Lambda connects to:

[[RDS]]

IAM considerations depend on:

**How database authentication is configured**

Lambda may also need access to:

[[Secrets Manager]]

to retrieve:

**Database credentials**

Architecture:

Lambda  
↓  
Execution Role  
↓  
Secrets Manager  
↓  
Credentials  
↓  
RDS

---

# Lambda + RDS Proxy

Architecture:

Lambda  
↓  
[[RDS Proxy]]  
↓  
RDS

Lambda still needs:

**Appropriate IAM and database permissions**

depending on:

**Authentication architecture**

RDS Proxy solves:

**Connection management**

not:

**Every IAM permission issue**

---

# Lambda + EFS

If Lambda uses:

[[EFS]]

the architecture may involve:

- VPC connectivity
- EFS access configuration
- Network permissions
- IAM authorization where configured

### Exam Principle

Access can depend on multiple layers:

**IAM + Network + Resource Configuration**

---

# CloudWatch Logs Permissions

A Lambda function runs successfully but:

**No logs appear**

One possible issue:

The execution role lacks:

**CloudWatch Logs permissions**

Think:

**AWSLambdaBasicExecutionRole**

---

# Permission Troubleshooting Framework

If Lambda gets:

**AccessDenied**

ask:

### 1. Who is making the request?

Lambda itself?

→ Execution Role

Another service invoking Lambda?

→ Resource-Based Policy / Invocation Permission

### 2. What resource is being accessed?

S3?

DynamoDB?

KMS?

Secrets Manager?

### 3. Is there another resource policy involved?

Examples:

- S3 Bucket Policy
- KMS Key Policy
- SQS Queue Policy

### 4. Is there an explicit Deny?

Remember:

**Explicit Deny wins**

---

# Execution Role and KMS Key Policy

KMS deserves special attention.

Even if the execution role has:

`kms:Decrypt`

access can still fail if:

**The KMS key policy does not allow the required access**

### Killer Exam Pattern

> IAM says Allow but encrypted resource still returns AccessDenied.
>
> → Check the **KMS key policy**

---

# Lambda Permissions and S3 Bucket Policies

Suppose:

Lambda execution role allows:

`s3:GetObject`

but the S3 bucket policy contains:

**Explicit Deny**

Result:

**Denied**

### IAM Rule

> **Explicit Deny overrides Allow**

---

# Lambda Permissions and SCPs

In AWS Organizations:

[[Service Control Policies]]

can restrict:

**Maximum available permissions**

Even if the Lambda execution role allows an action:

An SCP can still prevent it.

### Exam Thinking

Permissions can be restricted by:

- Identity policies
- Resource policies
- Permissions boundaries
- SCPs
- Explicit Deny

---

# Execution Role vs User Credentials

Do NOT create:

**IAM user access keys**

for Lambda.

Use:

**Execution Role**

Why?

Roles provide:

- Temporary credentials
- Automatic rotation
- No hardcoded secrets
- Better security

---

# Lambda Permissions with Event Source Mapping

For event source mappings:

Lambda needs permission to:

**Read from the source**

Example:

SQS  
↓  
Lambda

Permissions may include actions needed to:

- Receive messages
- Delete messages
- Read queue attributes

AWS managed policies can simplify:

**Common event source permissions**

---

# SQS Source vs SQS Destination

Do not confuse the direction.

### SQS → Lambda

Lambda consumes queue messages.

Think:

**Event Source Mapping + permissions to consume SQS**

### Lambda → SQS

Lambda sends messages.

Think:

**Execution Role + SendMessage**

### Memory Trick

**ARROW DIRECTION MATTERS**

---

# Architecture Thinking

## Scenario 1 — Lambda Reads S3

Lambda gets:

**AccessDenied**

when reading an object.

Check:

**Lambda Execution Role**

for required S3 permissions.

---

## Scenario 2 — S3 Cannot Invoke Lambda

S3 event notification is configured.

Lambda never runs.

Check:

**Lambda Resource-Based Policy**

for S3 invocation permission.

---

## Scenario 3 — API Gateway Cannot Invoke Lambda

API Gateway receives invocation permission error.

Check:

**Lambda invocation permission / resource policy**

not:

Lambda's S3 execution permissions.

---

## Scenario 4 — Lambda Cannot Write DynamoDB

Lambda executes but gets:

AccessDenied.

Fix:

**Add required DynamoDB permission to execution role**

---

## Scenario 5 — No CloudWatch Logs

Lambda executes but cannot write logs.

Check:

**Execution Role**

and:

**CloudWatch Logs permissions**

---

## Scenario 6 — Encrypted Secret Fails

Lambda role has Secrets Manager access but cannot decrypt the secret.

Check:

- KMS permissions
- KMS key policy

---

## Scenario 7 — Hardcoded Access Keys

Developer stores:

AWS Access Key  
AWS Secret Key

inside Lambda code.

Bad architecture.

Replace with:

**Lambda Execution Role**

---

## Scenario 8 — Two Functions Need Different Access

Function A:

S3 Read

Function B:

DynamoDB Write

Use:

**Least-privilege roles**

instead of:

**One broad role**

---

# Scenario Recognition

Immediately think:

**Lambda Execution Role**

when you see:

- Lambda accesses S3
- Lambda accesses DynamoDB
- Lambda publishes SNS
- Lambda sends SQS message
- Lambda retrieves secret
- Lambda decrypts KMS data
- Lambda writes CloudWatch Logs
- Lambda needs AWS API permissions

---

# Think Resource-Based Policy When You See

- S3 invokes Lambda
- SNS invokes Lambda
- API Gateway invokes Lambda
- EventBridge invokes Lambda
- Cross-account principal invokes Lambda
- "Who can invoke the function?"

---

# Exam Traps

## Trap 1 — Execution Role Controls Who Invokes Lambda

❌

Execution Role:

**Lambda → AWS**

Resource-Based Policy:

**Caller → Lambda**

---

## Trap 2 — Lambda Needs Hardcoded AWS Access Keys

❌

Use:

**IAM Execution Role**

---

## Trap 3 — Trust Policy Defines What Lambda Can Do

❌

Trust Policy:

**Who can assume the role**

Permissions Policy:

**What the role can do**

---

## Trap 4 — AdministratorAccess Is Best for Avoiding Permission Errors

❌

Use:

**Least privilege**

---

## Trap 5 — IAM Allow Always Overrides Resource Deny

❌

**Explicit Deny wins**

---

## Trap 6 — KMS Access Only Depends on Lambda's IAM Policy

❌

Check:

**KMS key policy**

too.

---

## Trap 7 — RDS Proxy Replaces IAM

❌

RDS Proxy:

**Manages database connections**

IAM:

**Controls authorization**

---

## Trap 8 — SQS Trigger and SQS Send Use the Same Architecture

❌

SQS → Lambda:

**Event Source Mapping**

Lambda → SQS:

**Execution Role permission**

---

# Quick Cheat Sheet

| Exam Clue | Answer |
|---|---|
| Lambda Reads S3 | Execution Role |
| Lambda Writes DynamoDB | Execution Role |
| Lambda Publishes SNS | Execution Role |
| Lambda Sends SQS Message | Execution Role |
| Lambda Reads Secret | Execution Role |
| Lambda Decrypts KMS Data | Execution Role + KMS Access |
| Lambda Writes Logs | Execution Role |
| S3 Invokes Lambda | Resource-Based Policy |
| API Gateway Invokes Lambda | Invocation Permission |
| Cross-Account Invokes Lambda | Resource-Based Policy |
| Who Assumes Role? | Trust Policy |
| What Can Role Do? | Permissions Policy |
| AWS Credentials in Code | ❌ Use Role |
| Explicit Deny | Wins |

---

# IAM Direction Cheat Sheet

| Direction | Permission |
|---|---|
| Lambda → S3 | Execution Role |
| Lambda → DynamoDB | Execution Role |
| Lambda → SQS | Execution Role |
| Lambda → SNS | Execution Role |
| Lambda → Secrets Manager | Execution Role |
| S3 → Lambda | Resource-Based Policy |
| SNS → Lambda | Resource-Based Policy |
| API Gateway → Lambda | Resource-Based Policy |
| EventBridge → Lambda | Resource-Based Policy |

---

# Final Exam Rapid-Fire

> **LAMBDA → AWS**
> → EXECUTION ROLE
>
> **AWS → LAMBDA**
> → RESOURCE-BASED POLICY
>
> **LAMBDA READS S3**
> → EXECUTION ROLE
>
> **LAMBDA WRITES DYNAMODB**
> → EXECUTION ROLE
>
> **LAMBDA GETS SECRET**
> → EXECUTION ROLE
>
> **LAMBDA DECRYPTS**
> → KMS PERMISSION + KEY POLICY
>
> **S3 INVOKES LAMBDA**
> → RESOURCE-BASED POLICY
>
> **API GATEWAY INVOKES LAMBDA**
> → INVOCATION PERMISSION
>
> **WHO ASSUMES ROLE?**
> → TRUST POLICY
>
> **WHAT CAN ROLE DO?**
> → PERMISSIONS POLICY
>
> **HARDCODED ACCESS KEYS**
> → WRONG
>
> **BEST PRACTICE**
> → IAM ROLE + LEAST PRIVILEGE
>
> **EXPLICIT DENY**
> → WINS

---

## Master Memory Trick

> [!tip] Lambda Execution Roles Master Memory Trick
> Picture Lambda standing inside a room.
>
> Lambda wants to walk **OUT** and use:
>
> - S3
> - DynamoDB
> - SQS
> - SNS
> - Secrets Manager
>
> Lambda asks:
>
> **"What am I allowed to do?"**
>
> Answer:
>
> **EXECUTION ROLE**
>
> Now imagine S3 standing outside and trying to come **IN**:
>
> S3 asks:
>
> **"Am I allowed to invoke Lambda?"**
>
> Answer:
>
> **RESOURCE-BASED POLICY**

So remember:

> **OUT**
> → Execution Role
>
> **IN**
> → Resource Policy
>
> **WHO GETS THE ROLE**
> → Trust Policy
>
> **WHAT THE ROLE CAN DO**
> → Permissions Policy
>
> **AWS ACCESS KEYS IN CODE**
> → NEVER
>
> **PERMISSIONS**
> → Least Privilege

And the killer SAA question:

> **"Which direction is the API call going?"**
>
> **Lambda → AWS service**
> → Execution Role
>
> **AWS service → Lambda**
> → Resource-Based Policy

---

## Related Notes

- [[Lambda]]
- [[Lambda Synchronous Invocations]]
- [[Lambda Asynchronous Invocations]]
- [[Lambda Event Source Mapping]]
- [[IAM]]
- [[S3]]
- [[04-Databases/DynamoDB]]
- [[SQS]]
- [[SNS]]
- [[API Gateway]]
- [[20-SAA/10-Messaging/EventBridge]]
- [[Secrets Manager]]
- [[06-Security/KMS]]
- [[07-Monitoring/CloudWatch]]
- [[RDS Proxy]]