## Developer Tools Comparison

| Service | Best For | Shortcut |
| --- | --- | --- |
| [[CodeCommit]] | Store source code | Git repos |
| [[CodeBuild]] | Build & test code | Compile / test |
| [[CodeDeploy]] | Deploy code | Deploy |
| [[CodePipeline]] | Orchestrate pipeline | CI/CD |
| [[CodeArtifact]] | Store packages / dependencies | Packages |
| [[CDK]] | Define cloud infrastructure | Programming language |

---

## Core Recognition

[[CodeCommit]] = STORE CODE

[[CodeBuild]] = BUILD + TEST

[[CodeDeploy]] = DEPLOY

[[CodePipeline]] = ORCHESTRATE

[[CodeArtifact]] = STORE PACKAGES / DEPENDENCIES

[[CDK]] = INFRASTRUCTURE WITH PROGRAMMING LANGUAGE

---

## The Four Code Services

### [[CodeCommit]]

Think:

STORE CODE

Private Git repository.

### [[CodeBuild]]

Think:

BUILD + TEST

Compile source code and run tests.

### [[CodeDeploy]]

Think:

DEPLOY

Deploy applications onto servers.

### [[CodePipeline]]

Think:

ORCHESTRATE

Connect and automate the CI/CD process.

### Memory Trick

Commit = STORE

Build = BUILD

Deploy = DEPLOY

Pipeline = ORCHESTRATE

---

## Source Code vs Packages

This is the key distinction introduced by [[CodeArtifact]].

### [[CodeCommit]]

Stores:

SOURCE CODE

Think:

Git Repository

### [[CodeArtifact]]

Stores:

SOFTWARE PACKAGES / DEPENDENCIES

### Memory Trick

CodeCommit = CODE

CodeArtifact = PACKAGES

---

## CDK vs CloudFormation

### [[CDK]]

Define cloud infrastructure using a:

PROGRAMMING LANGUAGE

### [[CloudFormation]]

Think:

INFRASTRUCTURE AS CODE / TEMPLATES

### Memory Trick

CDK = PROGRAMMING LANGUAGE

CloudFormation = TEMPLATE

---

## CI/CD Workflow

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

DEPLOY

[[CodePipeline]]

↓

ORCHESTRATES THE PROCESS

### Memory Trick

STORE → BUILD → DEPLOY

Pipeline connects everything.

---

## CodePipeline Workflow

Your course gives the larger pipeline sequence as:

CODE

↓

BUILD

↓

TEST

↓

PROVISION

↓

DEPLOY

[[CodePipeline]] orchestrates these steps.

---

## Most Important Comparisons

| If You See... | Think... |
| --- | --- |
| Private Git repository | [[CodeCommit]] |
| Store source code | [[CodeCommit]] |
| Compile source code | [[CodeBuild]] |
| Run automated tests | [[CodeBuild]] |
| Deploy application onto servers | [[CodeDeploy]] |
| EC2 + on-premises deployment | [[CodeDeploy]] |
| CI/CD orchestration | [[CodePipeline]] |
| Automate software release workflow | [[CodePipeline]] |
| Store software packages | [[CodeArtifact]] |
| Store dependencies | [[CodeArtifact]] |
| Define infrastructure with programming language | [[CDK]] |

---

## Don't Confuse These

### [[CodeCommit]] vs [[CodeArtifact]]

CodeCommit = SOURCE CODE

CodeArtifact = PACKAGES / DEPENDENCIES

---

### [[CodeBuild]] vs [[CodeDeploy]]

CodeBuild = BUILD + TEST

CodeDeploy = DEPLOY

---

### [[CodeDeploy]] vs [[CodePipeline]]

CodeDeploy = DEPLOYMENT STEP

CodePipeline = WHOLE WORKFLOW

---

### [[CodeBuild]] vs [[CodePipeline]]

CodeBuild = BUILD / TEST STEP

CodePipeline = ORCHESTRATE PROCESS

---

### [[CDK]] vs [[CloudFormation]]

CDK = PROGRAMMING LANGUAGE

CloudFormation = TEMPLATE / INFRASTRUCTURE AS CODE

---

## Scenario Recognition

Need a private Git repository?

→ [[CodeCommit]]

---

Need to store source code?

→ [[CodeCommit]]

---

Need to compile and test code?

→ [[CodeBuild]]

---

Need to automatically deploy an application?

→ [[CodeDeploy]]

---

Need to deploy applications to EC2 or on-premises servers?

→ [[CodeDeploy]]

---

Need to orchestrate a CI/CD workflow?

→ [[CodePipeline]]

---

Need to store software packages or dependencies?

→ [[CodeArtifact]]

---

Need to define cloud infrastructure using a programming language?

→ [[CDK]]

---

## 6-Service Memory Map

STORE CODE

→ [[CodeCommit]]

BUILD + TEST

→ [[CodeBuild]]

DEPLOY

→ [[CodeDeploy]]

ORCHESTRATE

→ [[CodePipeline]]

STORE PACKAGES

→ [[CodeArtifact]]

CODE INFRASTRUCTURE

→ [[CDK]]

---

## Quick Comparison

CodeCommit = STORE CODE

CodeBuild = BUILD + TEST

CodeDeploy = DEPLOY

CodePipeline = ORCHESTRATE

CodeArtifact = STORE PACKAGES

CDK = PROGRAMMING LANGUAGE

---

## Related Notes

- [[CodeCommit]]
- [[CodeBuild]]
- [[CodeDeploy]]
- [[CodePipeline]]
- [[CodeArtifact]]
- [[CDK]]
- [[CloudFormation]]
- [[Developer Tools Cheat Sheet]]