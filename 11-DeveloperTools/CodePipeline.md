## What Problem Does It Solve?

Automates and orchestrates the software release process.

**CodePipeline** solves the problem of coordinating the different steps required to move application code from development to production.

Think:

Code

↓

Build

↓

Test

↓

Provision

↓

Deploy

### Memory Trick

CodePipeline = Connect the Process

---

## Type

CI/CD Pipeline

---

## What Is AWS CodePipeline?

AWS CodePipeline is used to:

ORCHESTRATE

the different steps required to automatically push code to production.

Instead of performing only one task, CodePipeline connects the different stages of the software delivery process.

### Memory Trick

CodePipeline = Orchestrate the Pipeline

---

## CI/CD

CodePipeline is a basis for:

CI/CD

### CI

Continuous Integration

### CD

Continuous Delivery

For your course, associate:

CI/CD

↓

CodePipeline

### Memory Trick

CodePipeline = CI/CD Workflow

---

## Pipeline Workflow

Your course gives this sequence:

CODE

↓

BUILD

↓

TEST

↓

PROVISION

↓

DEPLOY

CodePipeline orchestrates these different steps.

### Memory Trick

Pipeline = From Code to Production

---

## Fully Managed

CodePipeline is:

Fully Managed

AWS handles the underlying pipeline service so developers can focus on defining and automating the software delivery workflow.

### Memory Trick

CodePipeline = Managed CI/CD

---

## Service Integration

Your course emphasizes that CodePipeline can work with multiple AWS and external services.

Examples include:

- [[CodeCommit]]
- [[CodeBuild]]
- [[CodeDeploy]]
- [[Elastic Beanstalk]]
- [[CloudFormation]]
- GitHub
- Third-party services
- Custom plugins

This allows CodePipeline to connect different stages of the release process.

### Memory Trick

CodePipeline = CONNECT SERVICES

---

## Fast Delivery

Your course identifies benefits such as:

Fast Delivery

and

Rapid Updates

Automating the pipeline helps move application changes through the release process.

---

## Common Use Cases

- CI/CD workflows
- DevOps workflows
- Automated software releases
- Connecting development services
- Automatically pushing code toward production

---

## CodePipeline vs CodeCommit

### [[CodeCommit]]

Think:

STORE CODE

### [[CodePipeline]]

Think:

ORCHESTRATE PROCESS

### Memory Trick

CodeCommit = STORE

CodePipeline = ORCHESTRATE

---

## CodePipeline vs CodeBuild

### [[CodeBuild]]

Think:

BUILD + TEST

It performs a specific part of the process.

### [[CodePipeline]]

Think:

WHOLE WORKFLOW

It orchestrates the different stages.

### Memory Trick

CodeBuild = BUILD STEP

CodePipeline = WHOLE PROCESS

---

## CodePipeline vs CodeDeploy

### [[CodeDeploy]]

Think:

DEPLOY

### [[CodePipeline]]

Think:

ORCHESTRATE

CodeDeploy performs the deployment.

CodePipeline coordinates the overall workflow.

### Memory Trick

CodeDeploy = DEPLOY

CodePipeline = CONNECT

---

## Developer Tools Workflow

[[CodeCommit]]

↓

STORE CODE

↓

[[CodeBuild]]

↓

BUILD + TEST

↓

[[CodeDeploy]]

↓

DEPLOY CODE

[[CodePipeline]]

↓

ORCHESTRATES THE ENTIRE PROCESS

### Memory Trick

Commit = STORE

Build = BUILD

Deploy = DEPLOY

Pipeline = ORCHESTRATE

---

## Scenario Questions

A company needs to orchestrate the different stages of its software release process.

→ CodePipeline

---

A company needs to automate a CI/CD workflow.

→ CodePipeline

---

A company needs to connect its code, build, test, and deployment stages.

→ CodePipeline

---

A company wants code changes automatically moved through a workflow toward production.

→ CodePipeline

---

A company needs a fully managed service for orchestrating its software delivery pipeline.

→ CodePipeline

---

A company needs a private Git repository.

→ [[CodeCommit]]

NOT CodePipeline

---

A company only needs to compile source code and run tests.

→ [[CodeBuild]]

NOT CodePipeline

---

A company needs to deploy applications onto servers.

→ [[CodeDeploy]]

NOT CodePipeline

---

## Don't Confuse These

[[CodeCommit]] = Store Code

[[CodeBuild]] = Build + Test Code

[[CodeDeploy]] = Deploy Code

[[CodePipeline]] = Orchestrate Pipeline

---

## Exam Keywords

AWS CodePipeline

CI/CD

Continuous Integration

Continuous Delivery

Pipeline

Orchestration

Workflow

Software Release

Production

Automation

Fully Managed

Integration

---

## Memory Tricks

CodePipeline = ORCHESTRATE

CodePipeline = CONNECT THE PROCESS

CodePipeline = WHOLE WORKFLOW

CodePipeline = CI/CD

CodePipeline = CODE → BUILD → TEST → PROVISION → DEPLOY

CodeCommit = STORE

CodeBuild = BUILD

CodeDeploy = DEPLOY

CodePipeline = ORCHESTRATE

---

## Quick Cheat Sheet

CodePipeline = ORCHESTRATE

CodePipeline = CI/CD

CodePipeline = Connect Services

CodePipeline = Automate Release Process

CodePipeline = Fully Managed

CodePipeline = Fast Delivery + Rapid Updates

Code → Build → Test → Provision → Deploy

CodeCommit = STORE

CodeBuild = BUILD + TEST

CodeDeploy = DEPLOY

CodePipeline = ORCHESTRATE

---

## Related Notes

- [[CodeCommit]]
- [[CodeBuild]]
- [[CodeDeploy]]
- [[Elastic Beanstalk]]
- [[CloudFormation]]
- [[Developer Tools Comparison]]
- [[Developer Tools Cheat Sheet]]