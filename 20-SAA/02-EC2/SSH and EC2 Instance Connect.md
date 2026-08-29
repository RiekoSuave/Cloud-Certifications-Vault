## What Problem Does It Solve?

SSH and EC2 Instance Connect allow you to:

REMOTELY CONNECT

to an EC2 instance.

This lets you administer and control the server without physically being near it.

### Memory Trick

SSH = REMOTE CONTROL FOR LINUX

---

## What Is SSH?

SSH stands for:

SECURE SHELL

SSH allows you to control a:

REMOTE MACHINE

using the:

COMMAND LINE

Think:

YOUR COMPUTER

↓

INTERNET

↓

SSH

↓

EC2 INSTANCE

---

## SSH Port

SSH uses:

PORT 22

### Memory Trick

SSH = 22

This connects directly with:

[[EC2 Security Groups]]

Your Security Group must allow the necessary traffic on:

PORT 22

---

## Basic SSH Architecture

Think:

YOUR COMPUTER

↓

PORT 22

↓

[[EC2 Security Groups]]

↓

EC2 INSTANCE

↓

COMMAND LINE ACCESS

---

## SSH and Linux

Your course focuses on SSH for connecting to:

LINUX EC2 INSTANCES

On:

MAC

and

LINUX

the course uses SSH.

### Memory Trick

Linux Server?

→ SSH

---

## Windows Connection Methods

Your course distinguishes connection methods based on the computer you're using.

### Mac / Linux

→ SSH

### Older Windows

→ PuTTY

### Windows 10+

→ SSH

### All

→ EC2 INSTANCE CONNECT

The exact connection tool matters less for the SAA exam than understanding:

SSH

=

REMOTE COMMAND-LINE ACCESS

---

# EC2 Instance Connect

## What Is EC2 Instance Connect?

EC2 Instance Connect allows you to:

CONNECT TO EC2

from within your:

WEB BROWSER

Think:

AWS CONSOLE

↓

BROWSER CONNECTION

↓

EC2 INSTANCE

### Memory Trick

Instance Connect = SSH FROM THE BROWSER

---

## Key File Difference

Traditional SSH commonly involves using your downloaded:

KEY FILE

EC2 Instance Connect does NOT require you to manually use that downloaded key file.

Instead, your course explains that AWS uploads a:

TEMPORARY KEY

onto the EC2 instance.

Think:

EC2 INSTANCE CONNECT

↓

AWS TEMPORARY KEY

↓

EC2

---

## Temporary Key

This is an important distinction.

Traditional connection:

YOUR KEY FILE

↓

SSH

↓

EC2

EC2 Instance Connect:

AWS

↓

TEMPORARY KEY

↓

EC2

↓

BROWSER CONNECTION

### Memory Trick

Instance Connect = TEMPORARY KEY

---

## Port 22 Is Still Required

This is an important exam trap.

Even though EC2 Instance Connect operates through your browser:

PORT 22

STILL NEEDS TO BE OPEN

according to your course.

Think:

BROWSER

does NOT mean:

NO SSH PORT

### Memory Trick

Instance Connect still needs 22

---

## Course OS Limitation

Your course specifically states that EC2 Instance Connect works:

OUT OF THE BOX

with:

AMAZON LINUX 2

Keep this association for questions based on this course material.

---

# SSH vs EC2 Instance Connect

| Feature | SSH | EC2 Instance Connect |
| --- | --- | --- |
| Remote EC2 access | Yes | Yes |
| Command-line access | Yes | Yes |
| Browser-based | No | Yes |
| Manually use downloaded key file | Commonly yes | No |
| Temporary key uploaded by AWS | No | Yes |
| Port 22 required | Yes | Yes |

---

## Fast Memory Trick

SSH

= TERMINAL

EC2 INSTANCE CONNECT

= BROWSER

BOTH

= PORT 22

---

# Security Groups and SSH

Before SSH can reach the EC2 instance:

[[EC2 Security Groups]]

must allow the appropriate:

INBOUND TRAFFIC

on:

PORT 22

Think:

SSH REQUEST

↓

SECURITY GROUP

↓

PORT 22 ALLOWED?

YES

↓

EC2

---

## SSH Security Best Practice From Course

Your Security Group note covered the course recommendation to maintain:

A SEPARATE SECURITY GROUP

for:

SSH ACCESS

This helps keep administrative access controlled separately.

---

# SSH Troubleshooting

Your course recommends trying:

EC2 INSTANCE CONNECT

if traditional SSH is giving you problems.

The important conceptual troubleshooting path is:

CAN'T CONNECT

↓

CHECK CONNECTION METHOD

↓

CHECK PORT 22 / SECURITY GROUP

↓

TRY EC2 INSTANCE CONNECT

---

# Scenario Recognition

Need command-line control of a remote Linux EC2 instance?

→ SSH

---

Which port is used for SSH?

→ PORT 22

---

Need to connect to EC2 directly from your browser?

→ EC2 INSTANCE CONNECT

---

Don't want to manually use your downloaded key file?

→ EC2 INSTANCE CONNECT

---

Which method has AWS upload a temporary key to EC2?

→ EC2 INSTANCE CONNECT

---

Using EC2 Instance Connect but port 22 is blocked?

→ CONNECTION WILL NOT WORK

---

Using Mac/Linux to remotely control a Linux EC2 instance?

→ SSH

---

# Exam Traps

SSH

= PORT 22

SSH

= REMOTE COMMAND LINE

EC2 Instance Connect

= BROWSER

EC2 Instance Connect

= TEMPORARY KEY

EC2 Instance Connect

≠ NO PORT 22

PORT 22 STILL MUST BE OPEN

Course association:

AMAZON LINUX 2

→ EC2 Instance Connect works out-of-the-box

---

# Quick Cheat Sheet

SSH

= SECURE SHELL

PURPOSE

= REMOTE COMMAND LINE

PORT

= 22

LINUX / MAC

= SSH

OLDER WINDOWS

= PuTTY

WINDOWS 10+

= SSH

BROWSER

= EC2 INSTANCE CONNECT

INSTANCE CONNECT KEY

= TEMPORARY KEY

INSTANCE CONNECT PORT

= STILL 22

---

# Master Memory Trick

TERMINAL?

→ SSH

BROWSER?

→ EC2 INSTANCE CONNECT

EITHER WAY:

↓

PORT 22

↓

[[EC2 Security Groups]]

↓

EC2 INSTANCE

---

## Related Notes

- [[EC2]]
- [[EC2 Security Groups]]
- [[EC2 IAM Roles]]
- [[Private vs Public IP]]
- [[Elastic IP]]
- [[EC2 Comparison]]
- [[SAA EC2 Cheat Sheet]]