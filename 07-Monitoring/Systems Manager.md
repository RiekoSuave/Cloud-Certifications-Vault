See also: [CloudFormation](CloudFormation)

## What Problem Does It Solve?

Automates operational tasks and system management at scale.

AWS Systems Manager solves the problem of managing large numbers of servers individually.

Instead of manually managing each server:

Many Servers

↓

Systems Manager

↓

Manage Them at Scale

### Memory Trick

Systems Manager = Manage Systems at Scale

---

## Type

Operations Management

---

## What Is AWS Systems Manager?

AWS Systems Manager (SSM) helps manage:

- EC2 instances
- On-premises systems

at scale.

It provides operational insights into the state of your infrastructure and includes a suite of management tools.

### Memory Trick

SSM = Manage Servers

---

## Hybrid AWS Service

Systems Manager can manage:

AWS EC2 Instances

AND

On-Premises Servers

This makes Systems Manager a:

Hybrid AWS Service

Think:

AWS Servers

+

On-Premises Servers

↓

Systems Manager

↓

Centralized Management

### Memory Trick

SSM = AWS + On-Premises Management

---

## Key Systems Manager Features

Your course emphasizes several important capabilities:

- Patching automation
- Run commands across servers
- Operational insights
- Parameter Store
- Session Manager

### Memory Trick

Systems Manager = Patch + Run + Manage

---

## Patch Management

Systems Manager can automate patching across servers.

This is useful when managing:

Large Fleets of Servers

Instead of manually patching each machine:

Systems Manager

↓

Automated Patching

↓

Improved Compliance

### Scenario

A company needs to patch thousands of servers automatically.

→ AWS Systems Manager

### Memory Trick

Mass Patching = Systems Manager

---

## Run Commands Remotely

Systems Manager can run commands across an entire fleet of servers.

Think:

One Command

↓

Systems Manager

↓

Many Servers

This reduces the need to manually connect to each server.

### Scenario

An administrator wants to execute a command across many EC2 instances.

→ AWS Systems Manager

---

## SSM Agent

Systems Manager uses the:

SSM Agent

The SSM Agent must be installed on systems that Systems Manager controls.

Your course notes that it is installed by default on:

- Amazon Linux AMIs
- Some Ubuntu AMIs

The agent allows Systems Manager to:

- Run commands
- Patch servers
- Configure servers

### Important Exam Clue

If an instance cannot be controlled using Systems Manager:

Check the SSM Agent

### Memory Trick

No SSM Control?

Check the Agent

---

## Supported Operating Systems

Your course states that Systems Manager works with:

- Linux
- Windows
- macOS
- Raspberry Pi OS (Raspbian)

---

## Session Manager

Systems Manager includes:

Session Manager

Session Manager allows you to start a secure shell on:

- EC2 instances
- On-premises servers

Your course emphasizes that Session Manager does NOT require:

- SSH access
- Bastion hosts
- SSH keys
- Port 22

This can improve security.

### Memory Trick

Session Manager = Secure Server Access Without SSH

---

## Session Manager Logging

Session Manager can send session log data to:

- Amazon S3
- CloudWatch Logs

Think:

Session Manager

↓

Session Logs

↓

S3 / CloudWatch Logs

---

## Parameter Store

Systems Manager includes:

Parameter Store

Parameter Store provides secure storage for:

- API keys
- Passwords
- Configuration values

Your course describes Parameter Store as:

- Serverless
- Scalable
- Durable

Access can be controlled using:

IAM

It also supports:

- Version tracking
- Optional encryption

### Memory Trick

Parameter Store = Store Configuration + Secrets

---

## CloudFormation vs Systems Manager

These services solve different problems.

### CloudFormation

Used to:

BUILD / DEPLOY Infrastructure

### Systems Manager

Used to:

MANAGE / OPERATE Systems

| CloudFormation | Systems Manager |
| --- | --- |
| Infrastructure deployment | Operations management |
| Infrastructure as Code | Manage systems |
| Templates | Patching |
| Build resources | Run commands |
| Create infrastructure | Maintain infrastructure |

### Memory Trick

CloudFormation = BUILD

Systems Manager = MANAGE

See:

[CloudFormation](CloudFormation)

---

## Common Use Cases

- Managing EC2 instances at scale
- Managing on-premises servers
- Automated patching
- Running commands remotely
- Server maintenance
- Secure server sessions
- Storing configuration parameters and secrets

---

## Scenario Questions

A company needs to patch thousands of servers automatically.

→ Systems Manager

---

A company needs to manage both EC2 and on-premises servers.

→ Systems Manager

---

An administrator wants to run commands across an entire fleet of servers.

→ Systems Manager

---

An administrator wants secure access to an EC2 instance without opening port 22 or managing SSH keys.

→ Systems Manager Session Manager

---

An administrator cannot manage an EC2 instance using Systems Manager.

What should they check?

→ SSM Agent

---

A company needs secure storage for API keys, passwords, and configuration values.

→ Systems Manager Parameter Store

---

A company wants to define and deploy AWS infrastructure using templates.

→ CloudFormation

NOT Systems Manager

---

## Don't Confuse These

Systems Manager = Manage Existing Systems

CloudFormation = Build Infrastructure

SSM Agent = Enables Systems Manager Control

Session Manager = Secure Server Access

Parameter Store = Configuration + Secrets

### Memory Trick

CloudFormation = BUILD

Systems Manager = MANAGE

SSM Agent = CONNECT

Session Manager = ACCESS

Parameter Store = STORE

---

## Exam Keywords

AWS Systems Manager

SSM

Operations Management

EC2

On-Premises

Hybrid

Patching

Automation

Run Commands

SSM Agent

Session Manager

Parameter Store

---

## Quick Cheat Sheet

Systems Manager = Manage Systems at Scale

Systems Manager = EC2 + On-Premises

Patching → Systems Manager

Fleet Commands → Systems Manager

SSM Agent → Enables Management

Session Manager → Secure Access Without SSH

No Port 22 → Session Manager

Parameter Store → Configuration + Secrets

CloudFormation = BUILD

Systems Manager = MANAGE