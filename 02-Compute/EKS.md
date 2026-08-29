See also: [[02-Compute/EKS]]

See also: [[02-Compute/Fargate]]

See also: [[02-Compute/ECR]]

## What Problem Does It Solve?

Provides managed Kubernetes on AWS.

EKS reduces the operational complexity of deploying and managing Kubernetes clusters yourself.

---

## Type

Managed Kubernetes

---

## What Is EKS?

EKS stands for:

Elastic Kubernetes Service

EKS allows you to launch and manage Kubernetes clusters on AWS.

AWS manages the Kubernetes control plane.

---

## What Is Kubernetes?

Kubernetes is an open-source system used to:

- Deploy containerized applications
- Manage containers
- Scale containerized applications

Kubernetes commonly manages applications packaged as containers.

---

## Kubernetes Is Cloud-Agnostic

Kubernetes is not exclusive to AWS.

It can be used across different environments and cloud providers.

Examples:

- AWS
- Microsoft Azure
- Google Cloud

### Memory Trick

Kubernetes = Portable container orchestration

EKS = AWS-managed Kubernetes

---

## Running EKS Workloads

Containers managed through EKS can run using:

### EC2

You provision and manage the EC2 instances providing the compute infrastructure.

### Fargate

AWS provides serverless compute for the containers.

No EC2 instances need to be managed.

See:

[[AWS Fargate]]

---

## EKS vs ECS

Both services manage containerized applications, but the major difference is Kubernetes.

### Amazon ECS

AWS-native container orchestration.

### Amazon EKS

Managed Kubernetes.

| Service | Best For |
|---|---|
| ECS | AWS-native container orchestration |
| EKS | Kubernetes |
| Fargate | Serverless container compute |
| ECR | Container image storage |

---

## Key Features

- Managed Kubernetes
- Managed control plane
- Container orchestration
- Scalable
- Supports EC2
- Supports Fargate
- Uses open-source Kubernetes

---

## Compare Against

ECS → AWS-native container orchestration

Fargate → Serverless compute for containers

ECR → Stores container images

EC2 → Virtual machines that can provide container compute

---

## Exam Scenarios

A company specifically wants to run Kubernetes on AWS.

→ Amazon EKS

---

A company wants Kubernetes without managing the Kubernetes control plane itself.

→ Amazon EKS

---

A company wants Kubernetes containers without managing EC2 instances.

→ EKS + Fargate

---

A company wants AWS-native container orchestration and does not require Kubernetes.

→ Amazon ECS

---

## Exam Keywords

Kubernetes

Containers

Managed Kubernetes

Control plane

EC2

Fargate

Cloud-agnostic

---

## Memory Tricks

EKS = Kubernetes

ECS = AWS Containers

Fargate = Serverless Containers

ECR = Container Image Storage