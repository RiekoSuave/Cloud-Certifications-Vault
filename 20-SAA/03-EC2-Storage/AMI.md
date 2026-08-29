## What Problem Does It Solve?

AMI provides:

PRECONFIGURED EC2 INSTANCES

Instead of launching a brand-new EC2 instance and manually installing everything again, you can create an image that already contains your desired configuration.

Think:

CONFIGURE EC2

↓

CREATE IMAGE

↓

LAUNCH IDENTICAL EC2 INSTANCES

### Memory Trick

AMI = EC2 TEMPLATE

---

## What Is an AMI?

AMI stands for:

AMAZON MACHINE IMAGE

An AMI is:

A CUSTOMIZED IMAGE

used to launch:

EC2 INSTANCES

An AMI can contain things such as:

- Operating system
    
- Software
    
- Configuration
    
- Monitoring tools
    

Think:

AMI

↓

OS

SOFTWARE

CONFIGURATION

↓

READY-TO-LAUNCH EC2

### Memory Trick

AMI = PREBUILT EC2

---

## Why Use an AMI?

Without an AMI:

LAUNCH EC2

↓

INSTALL OS SOFTWARE

↓

CONFIGURE APPLICATION

↓

INSTALL MONITORING

↓

READY

With an AMI:

LAUNCH AMI

↓

EC2 READY FASTER

Because your software and configuration are already packaged inside the AMI.

Think:

AMI

=

FASTER BOOT + FASTER CONFIGURATION

---

## AMI Architecture Thinking

Think of an AMI as the blueprint for an EC2 instance.

AMI

↓

LAUNCH

↓

EC2 INSTANCE

You can launch multiple EC2 instances from the same AMI.

Think:

AMI

↓

EC2 #1

↓

EC2 #2

↓

EC2 #3

This is useful when multiple servers need the same configuration.

---

## Types of AMIs

Your course introduces three main AMI sources.

### Public AMI

PUBLIC AMI

↓

AWS PROVIDED

These are AMIs made available for you to use.

Think:

AWS

↓

AMI

↓

YOUR EC2

---

### Your Own AMI

You can create and maintain:

CUSTOM AMIs

Think:

YOUR EC2

↓

CUSTOMIZE

↓

CREATE AMI

↓

YOUR AMI

This lets you standardize your own EC2 configuration.

---

### AWS Marketplace AMI

You can also launch:

AWS MARKETPLACE AMIs

These are created by third parties and may be:

PAID

Think:

THIRD PARTY

↓

PREBUILT AMI

↓

AWS MARKETPLACE

↓

EC2

### Memory Trick

AMI SOURCES

=

PUBLIC

YOUR OWN

MARKETPLACE

---

## AMIs Are Region-Specific

AMIs are built for:

A SPECIFIC AWS REGION

Think:

AMI

↓

ONE REGION

An AMI created in one Region is not automatically available in another Region.

However:

AMI

↓

COPY

↓

ANOTHER REGION

### Memory Trick

AMI = REGIONAL

BUT

AMI CAN BE COPIED

---

## Creating Your Own AMI

The basic AMI creation process is:

START EC2 INSTANCE

↓

CUSTOMIZE INSTANCE

↓

STOP INSTANCE

↓

CREATE AMI

↓

LAUNCH NEW EC2 FROM AMI

Stopping the EC2 instance before creating the AMI helps with:

DATA INTEGRITY

### Memory Trick

CUSTOMIZE

↓

STOP

↓

IMAGE

↓

LAUNCH

---

## AMI and EBS Snapshots

When you create an AMI from an EBS-backed EC2 instance:

CREATE AMI

↓

EBS SNAPSHOTS CREATED

The AMI references the storage needed to recreate the EC2 instance.

Think:

EC2

↓

EBS VOLUME

↓

CREATE AMI

↓

AMI

[EBS Snapshots](https://chatgpt.com/c/EBS%20Snapshots)

### Memory Trick

AMI CREATION

=

IMAGE + EBS SNAPSHOT

---

## AMI vs EBS Snapshot

Do not confuse:

AMI

and

EBS SNAPSHOT

### AMI

AMI

=

EC2 MACHINE TEMPLATE

It contains the configuration needed to launch an EC2 instance.

### EBS Snapshot

EBS SNAPSHOT

=

BACKUP OF EBS STORAGE

Think:

AMI

=

BUILD SERVER

EBS SNAPSHOT

=

RESTORE DISK

---

## Custom AMI Example

Imagine you need:

10 IDENTICAL WEB SERVERS

Without a custom AMI:

EC2 #1

↓

INSTALL SOFTWARE

EC2 #2

↓

INSTALL SOFTWARE

EC2 #3

↓

INSTALL SOFTWARE

...

With a custom AMI:

CONFIGURE ONE EC2

↓

CREATE AMI

↓

LAUNCH 10 EC2 INSTANCES

Think:

CONFIGURE ONCE

↓

REUSE MANY TIMES

---

## AMI and Auto Scaling

AMI becomes especially important when using:

[Auto Scaling Groups](https://chatgpt.com/c/Auto%20Scaling%20Groups)

An Auto Scaling Group may need to create new EC2 instances quickly.

Think:

AUTO SCALING GROUP

↓

NEEDS NEW INSTANCE

↓

LAUNCH FROM AMI

↓

READY EC2

A properly configured AMI reduces the amount of setup required after launch.

---

## AMI and EC2 User Data

Both AMIs and:

[02-Compute/EC2 User Data](https://chatgpt.com/c/02-Compute/EC2%20User%20Data)

can help configure EC2 instances.

But they solve the problem differently.

### AMI

AMI

=

PRE-PACKAGED CONFIGURATION

### User Data

USER DATA

=

RUN CONFIGURATION SCRIPT AT LAUNCH

Think:

AMI

=

BAKE CONFIGURATION INTO IMAGE

USER DATA

=

CONFIGURE DURING BOOT

### SAA Thinking

If software rarely changes and fast startup is important:

→ AMI

If configuration needs to happen dynamically during launch:

→ EC2 User Data

They can also be used together.

---

## Faster EC2 Deployment

AMI improves deployment speed because:

SOFTWARE

CONFIGURATION

OPERATING SYSTEM

can already be prepared.

Think:

PRECONFIGURE ONCE

↓

CREATE AMI

↓

LAUNCH REPEATEDLY

This is especially useful for:

- Scaling
    
- Standardized servers
    
- Recovery
    
- Repeated deployments
    

---

## Scenario Recognition

Need to launch many EC2 instances with the same configuration?

→ AMI

---

Need a reusable EC2 machine template?

→ AMI

---

Need the operating system and software already installed before EC2 launches?

→ AMI

---

Need faster EC2 boot and configuration?

→ Custom AMI

---

Need to reproduce an existing configured EC2 instance?

→ Create an AMI

---

Need an AMI in another AWS Region?

→ Copy the AMI to that Region

---

Need a third-party preconfigured server image?

→ AWS Marketplace AMI

---

Need a disk backup rather than an entire EC2 machine template?

→ EBS Snapshot

---

Need dynamic commands to execute when the EC2 instance launches?

→ EC2 User Data

---

## Exam Traps

AMI

=

AMAZON MACHINE IMAGE

AMI

=

EC2 TEMPLATE

AMI ≠ RUNNING EC2 INSTANCE

AMI ≠ EBS SNAPSHOT

AMI = REGION-SPECIFIC

AMI CAN BE COPIED ACROSS REGIONS

CUSTOM AMI = YOUR OWN CONFIGURATION

MARKETPLACE AMI = THIRD-PARTY IMAGE

CREATE AMI = ALSO CREATES EBS SNAPSHOTS

STOP INSTANCE BEFORE AMI CREATION = BETTER DATA INTEGRITY

AMI = PRECONFIGURE BEFORE LAUNCH

USER DATA = CONFIGURE DURING LAUNCH

---

## Quick Cheat Sheet

AMI

=

AMAZON MACHINE IMAGE

AMI

=

EC2 TEMPLATE

AMI CONTAINS

=

OS + SOFTWARE + CONFIGURATION

BENEFIT

=

FASTER EC2 BOOT / CONFIGURATION

PUBLIC AMI

=

AWS PROVIDED

CUSTOM AMI

=

YOU CREATE AND MAINTAIN IT

MARKETPLACE AMI

=

THIRD-PARTY IMAGE

AMI SCOPE

=

REGION

MOVE AMI TO ANOTHER REGION

=

COPY AMI

CREATE CUSTOM AMI

=

CONFIGURE EC2

↓

STOP EC2

↓

CREATE AMI

CREATE AMI

=

CREATES EBS SNAPSHOTS

AMI

=

BUILD SERVER

EBS SNAPSHOT

=

BACKUP DISK

---

## Master Memory Trick

EC2

=

SERVER

AMI

=

SERVER TEMPLATE

EBS SNAPSHOT

=

DISK BACKUP

USER DATA

=

BOOT SCRIPT

CUSTOM AMI

=

CONFIGURE ONCE

↓

LAUNCH MANY

---

## Related Notes

- [EC2](https://chatgpt.com/c/EC2)
    
- [EBS Volumes](https://chatgpt.com/c/EBS%20Volumes)
    
- [EBS Snapshots](https://chatgpt.com/c/EBS%20Snapshots)
    
- [02-Compute/EC2 User Data](https://chatgpt.com/c/02-Compute/EC2%20User%20Data)
    
- [Auto Scaling Groups](https://chatgpt.com/c/Auto%20Scaling%20Groups)
    
- [EC2 Image Builder](https://chatgpt.com/c/EC2%20Image%20Builder)
    
- [EC2 Instance Store](https://chatgpt.com/c/EC2%20Instance%20Store)
    
- [SAA EC2 Storage Cheat Sheet](https://chatgpt.com/c/SAA%20EC2%20Storage%20Cheat%20Sheet)