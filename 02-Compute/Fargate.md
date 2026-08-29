See also: [[02-Compute/ECS]]

See also: [[02-Compute/EKS]]

See also: [[02-Compute/ECR]]

## What Problem Does It Solve?

Runs containers without requiring you to provision or manage the underlying servers.

Fargate removes the need to manage EC2 instances for container workloads.

---

## Type

Serverless Containers

---

## What Is Fargate?

Fargate is a serverless compute option for containers.

Instead of provisioning EC2 instances yourself, AWS provides the infrastructure needed to run your containers.

### Memory Trick

Fargate = Serverless containers

---

## How Fargate Works

You define the resources your container needs, such as:

- CPU
- RAM

AWS provides the infrastructure and runs the container for you.

You do NOT need to provision EC2 instances.

---

## Fargate With ECS

ECS can run containers using:

### EC2

You provision and maintain the EC2 infrastructure.

### Fargate

AWS provides the underlying compute infrastructure.

### Memory Trick

ECS + EC2 = Manage servers

ECS + Fargate = No server management

---

## Fargate With EKS

EKS workloads can also run using Fargate.

This allows Kubernetes containers to run without requiring you to manage the underlying EC2 instances.

See:

[[02-Compute/EKS]]

---

## Fargate vs EC2

| EC2 | Fargate |
|---|---|
| Manage instances | No instance management |
| Choose servers | Serverless |
| Maintain infrastructure | AWS handles infrastructure |
| Full server control | Focus on containers |

---

## Fargate vs Lambda

Both are serverless, but they solve different problems.

### Fargate

Runs containers.

### Lambda

Runs functions/code in response to events.

| Service | Best For |
|---|---|
| Fargate | Containers |
| Lambda | Functions |

---

## Container Relationship

ECR

↓

Stores container images

ECS / EKS

↓

Orchestrates containers

Fargate

↓

Provides serverless compute for containers

---

## Key Features

- Serverless
- Runs containers
- No EC2 provisioning
- No underlying server management
- Works with ECS
- Works with EKS
- CPU and RAM based resources

---

## Compare Against

ECS → AWS-native container orchestration

EKS → Kubernetes

ECR → Container image storage

EC2 → Virtual machines you manage

Lambda → Serverless functions

---

## Exam Scenarios

A company wants to run containers without managing EC2 instances.

→ Fargate

---

A company wants ECS but does not want to provision container servers.

→ ECS + Fargate

---

A company wants Kubernetes without managing the underlying EC2 compute.

→ EKS + Fargate

---

A company wants serverless event-driven functions instead of containers.

→ Lambda

---

## Exam Keywords

Serverless

Containers

Docker

No EC2 management

CPU

RAM

ECS

EKS

---

## Memory Tricks

Fargate = Serverless Containers

ECS = AWS Containers

EKS = Kubernetes

ECR = Store Container Images

Lambda = Serverless Functions