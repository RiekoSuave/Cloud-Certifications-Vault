
See also: [[02-Compute/ECR|ECR]]

See also: [[02-Compute/Fargate]]

See also: [[02-Compute/EKS]]

## What Problem Does It Solve?

Runs and manages containerized applications on AWS.

ECS helps manage and scale containers without requiring you to use Kubernetes.

---

## Type

Container Orchestration

---

## What Is ECS?

ECS stands for:

Elastic Container Service

It is AWS's container management service.

ECS can launch and manage Docker containers on AWS.

---

## What Is a Container?

A container packages an application and its dependencies together so the application can run consistently.

Docker is a common container technology.

### Memory Trick

Docker = Container technology

ECS = AWS container management

---

## ECS With EC2

One way to run ECS containers is on EC2 instances.

In this model:

You provision and maintain the EC2 infrastructure.

AWS ECS manages starting and stopping the containers.

### Memory Trick

ECS + EC2 = You manage the servers

---

## ECS With Fargate

ECS can also use AWS Fargate.

With Fargate:

- No EC2 instances to provision
- No underlying servers to manage
- AWS runs the containers based on required CPU and RAM

See:

[[AWS Fargate]]

### Memory Trick

ECS + Fargate = Serverless containers

---

## ECS With ECR

Container images can be stored in:

Amazon ECR

ECR provides a private repository for Docker images.

Basic Flow:

Developer creates Docker image

↓

Store image in ECR

↓

ECS runs the container

See:

[[Amazon ECR]]

---

## Load Balancing

ECS integrates with:

Application Load Balancer (ALB)

This allows incoming application traffic to be distributed across containers.

---

## Key Features

- Runs Docker containers
- AWS-native container orchestration
- Starts and stops containers
- Integrates with EC2
- Integrates with Fargate
- Integrates with ECR
- Integrates with Application Load Balancer

---

## ECS vs EKS

### ECS

AWS-native container orchestration.

Does not require Kubernetes.

### EKS

AWS managed Kubernetes service.

Uses Kubernetes.

| Service | Purpose |
|---|---|
| ECS | AWS-native containers |
| EKS | Kubernetes containers |

### Memory Trick

ECS = AWS Containers

EKS = Kubernetes

---

## Compare Against

EKS → Managed Kubernetes

Fargate → Serverless compute for containers

ECR → Stores container images

EC2 → Virtual machines

---

## Exam Scenarios

A company wants to run Docker containers using an AWS-native container orchestration service.

→ Amazon ECS

---

A company wants ECS containers but does not want to manage EC2 instances.

→ ECS + Fargate

---

A company needs somewhere to privately store Docker images.

→ Amazon ECR

---

A company specifically requires Kubernetes.

→ Amazon EKS

---

## Exam Keywords

Containers

Docker

Container orchestration

EC2

Fargate

ECR

Application Load Balancer

---

## Memory Tricks

ECS = AWS Containers

ECR = Store Container Images

Fargate = Serverless Containers

EKS = Kubernetes