## What Problem Does It Solve?

Provides a private AWS repository for storing container images.

---

## Type

Container Registry

---

## Key Features

- Stores Docker container images
- Integrates with Amazon ECS
- Integrates with AWS Fargate
- AWS-managed container repository

---

## How It Fits Together

ECR = Store container image

ECS = Manage/run containers

Fargate = Run containers without managing EC2 servers

---

## Example

Developer builds a Docker image.

↓

Store image in Amazon ECR.

↓

ECS or Fargate uses the image to launch containers.

---

## Compare Against

ECS → Runs and manages containers

EKS → Runs Kubernetes

Fargate → Serverless container compute

ECR → Stores container images

---

## Exam Keywords

Docker images

Container registry

Repository

Containers

---

## Memory Trick

ECR = Container image storage