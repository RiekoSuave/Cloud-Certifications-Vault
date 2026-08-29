## What Problem Does It Solve?

Provides managed source code repositories.

**CodeCommit** solves the need for a private, secure, scalable place to store and manage application source code using Git.

Think:

Developer Code

↓

CodeCommit

↓

Private Git Repository

### Memory Trick

CodeCommit = Store Code

---

## Type

Version Control / Source Control

---

## What Is AWS CodeCommit?

AWS CodeCommit is a:

Source-Control Service

that hosts:

Git-Based Repositories

Developers can use CodeCommit to store application code before it is built and deployed.

Think:

WRITE CODE

↓

[[CodeCommit]]

↓

STORE CODE

### Memory Trick

CodeCommit = AWS Git Repository

---

## Git-Based Repositories

Your course emphasizes that developers commonly store source code in:

Repositories

using:

Git

CodeCommit provides Git-based repositories within AWS.

### Memory Trick

Git Repository on AWS = CodeCommit

---

## Version Control

CodeCommit automatically versions:

Code Changes

This allows developers to track changes made to the source code.

Think:

Code Change

↓

CodeCommit

↓

Versioned

### Memory Trick

CodeCommit = Store + Version Code

---

## Collaboration

CodeCommit makes it easier for developers to:

Collaborate on Code

Multiple developers can work with code stored in the repository.

### Memory Trick

CodeCommit = Team Code Repository

---

## Fully Managed

CodeCommit is:

Fully Managed

AWS manages the underlying infrastructure for the source-control service.

### Memory Trick

CodeCommit = Git Without Managing Repository Infrastructure

---

## Scalable & Highly Available

Your course identifies CodeCommit as:

Scalable

and

Highly Available

For CCP, keep this association high-level.

---

## Private & Secure

Your course describes CodeCommit as:

Private

Secure

Integrated with AWS

### Memory Trick

CodeCommit = Private AWS Git Repository

---

## Common Use Cases

- Source code management
- Version control
- Git repositories
- Developer collaboration
- Storing application code before build and deployment

---

## CodeCommit vs CodeBuild

### [[CodeCommit]]

Think:

STORE CODE

### [[CodeBuild]]

Think:

BUILD + TEST CODE

Think:

[[CodeCommit]]

↓

Source Code

↓

[[CodeBuild]]

↓

Compile + Test

### Memory Trick

CodeCommit = STORE

CodeBuild = BUILD

---

## CodeCommit vs CodeDeploy

### [[CodeCommit]]

Stores the code.

### [[CodeDeploy]]

Deploys the code.

### Memory Trick

CodeCommit = STORE

CodeDeploy = DEPLOY

---

## CodeCommit vs CodePipeline

### [[CodeCommit]]

Think:

SOURCE CODE REPOSITORY

### [[CodePipeline]]

Think:

ORCHESTRATE CI/CD PROCESS

### Memory Trick

CodeCommit = STORE

CodePipeline = ORCHESTRATE

---

## CodeCommit vs GitHub

Your course uses GitHub as a familiar comparison.

### CodeCommit

AWS source-control service that hosts Git-based repositories.

### GitHub

A well-known public offering for Git repositories.

### Memory Trick

CodeCommit = AWS Git Repository

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

ORCHESTRATES THE PROCESS

### Memory Trick

Commit = STORE

Build = BUILD

Deploy = DEPLOY

Pipeline = AUTOMATE / ORCHESTRATE

---

## Scenario Questions

A company needs a source-control service that hosts Git-based repositories in AWS.

→ CodeCommit

---

A development team needs somewhere to store source code.

→ CodeCommit

---

A development team needs a private Git repository in AWS.

→ CodeCommit

---

A company wants code changes to be automatically versioned.

→ CodeCommit

---

A company needs developers to collaborate using an AWS-hosted source code repository.

→ CodeCommit

---

A company needs to compile source code and run tests.

→ [[CodeBuild]]

NOT CodeCommit

---

A company needs to automatically deploy code.

→ [[CodeDeploy]]

NOT CodeCommit

---

A company needs to orchestrate its CI/CD workflow.

→ [[CodePipeline]]

NOT CodeCommit

---

## Don't Confuse These

[[CodeCommit]] = Store Code

[[CodeBuild]] = Build + Test Code

[[CodeDeploy]] = Deploy Code

[[CodePipeline]] = Orchestrate Pipeline

---

## Exam Keywords

AWS CodeCommit

Source Control

Version Control

Git

Git Repository

Source Code

Private Repository

Code Collaboration

Code Versioning

Fully Managed

Scalable

Highly Available

Secure

---

## Memory Tricks

CodeCommit = STORE CODE

CodeCommit = AWS GIT REPOSITORY

CodeCommit = STORE + VERSION

CodeCommit = PRIVATE GIT

CodeBuild = BUILD

CodeDeploy = DEPLOY

CodePipeline = ORCHESTRATE

---

## Quick Cheat Sheet

CodeCommit = STORE CODE

CodeCommit = Git Repositories

CodeCommit = Source Control

CodeCommit = Version Control

CodeCommit = Automatically Version Changes

CodeCommit = Collaboration

CodeCommit = Fully Managed

CodeCommit = Private + Secure

CodeCommit = AWS Git Repository

CodeCommit = STORE

CodeBuild = BUILD

CodeDeploy = DEPLOY

CodePipeline = ORCHESTRATE

---

## Related Notes

- [[CodeBuild]]
- [[CodeDeploy]]
- [[CodePipeline]]
- [[Developer Tools Comparison]]
- [[Developer Tools Cheat Sheet]]