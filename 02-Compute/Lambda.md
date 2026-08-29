See also: [[02-Compute/EC2]]

See also: [[02-Compute/Fargate]]

See also: [[API Gateway]]

## What Problem Does It Solve?

Runs code without requiring you to provision or manage servers.

Lambda is useful for short-running, event-driven workloads where you want AWS to manage the underlying infrastructure.

---

## Type

Serverless Compute

Function as a Service (FaaS)

---

## What Is Lambda?

Lambda allows you to upload code and have AWS run it when needed.

You do NOT:

- Provision servers
- Manage EC2 instances
- Maintain operating systems

AWS manages the underlying infrastructure.

---

## Event-Driven

Lambda is reactive.

A Lambda function can run when an event occurs.

Example:

User uploads an image to S3

↓

S3 event triggers Lambda

↓

Lambda creates a thumbnail

### Memory Trick

Event happens → Lambda runs

---

## Automatic Scaling

Lambda scales automatically.

If more events occur, AWS can run additional function executions as needed.

You do not manually provision additional servers.

---

## Maximum Execution Time

A Lambda invocation can run for up to:

15 minutes

### Exam Tip

Lambda is designed for short-running functions.

It is not intended for workloads that need to continuously run for long periods.

---

## Lambda Billing

Lambda billing is based primarily on:

- Number of invocations
- Execution duration
- Memory allocated

You don't pay for an idle EC2 server waiting for work.

### Memory Trick

Lambda = Pay when code runs

---

## Language Support

Lambda supports multiple programming languages.

Your course notes distinguish Lambda from running arbitrary Docker containers.

For general container workloads, consider:

[[02-Compute/ECS]]

[[02-Compute/Fargate]]

---

## Lambda + S3

A common serverless architecture is:

S3

↓

Event

↓

Lambda

↓

Process data

### Example

Image uploaded to S3

↓

Lambda automatically creates a thumbnail

---

## Lambda + API Gateway

API Gateway can expose Lambda functions through an HTTP API.

Basic Flow:

User

↓

API Gateway

↓

Lambda

### Example

Client sends web request

↓

API Gateway receives request

↓

Lambda executes application logic

See:

[[API Gateway]]

---

## Serverless Cron Jobs

Lambda can also be used for scheduled serverless jobs.

This allows code to execute on a schedule without maintaining a continuously running server.

---

## Lambda vs EC2

| EC2 | Lambda |
|---|---|
| Virtual machine | Function |
| Manage server | No server management |
| Can run continuously | Maximum 15-minute invocation |
| Pay for provisioned compute | Pay based on execution |
| Full OS control | Focus on code |

### Memory Trick

EC2 = Rent server

Lambda = Run function

---

## Lambda vs Fargate

Both reduce server management, but they solve different problems.

### Lambda

Runs functions.

### Fargate

Runs containers.

| Service | Best For |
|---|---|
| Lambda | Serverless functions |
| Fargate | Serverless containers |

---

## Common Use Cases

- Image processing
- S3 event processing
- Serverless APIs
- Scheduled jobs
- Event-driven applications

---

## Compare Against

EC2 → Virtual machines

Fargate → Serverless containers

ECS → Container orchestration

API Gateway → Exposes APIs that can invoke Lambda

---

## Exam Scenarios

An image uploaded to S3 needs to automatically generate a thumbnail.

→ Lambda

---

A company wants to run code without provisioning servers.

→ Lambda

---

A company needs a serverless backend for an HTTP API.

→ API Gateway + Lambda

---

A company needs to run containers without managing EC2 instances.

→ Fargate

---

A workload needs to run continuously for longer than 15 minutes.

→ Lambda is not the appropriate choice

---

## Exam Keywords

Serverless

Function as a Service

Event-driven

Automatic scaling

Invocation

15 minutes

S3

API Gateway

---

## Memory Tricks

Lambda = Serverless Functions

Event → Lambda Runs

S3 + Lambda = Event Processing

API Gateway + Lambda = Serverless API

Fargate = Serverless Containers

EC2 = Virtual Machines