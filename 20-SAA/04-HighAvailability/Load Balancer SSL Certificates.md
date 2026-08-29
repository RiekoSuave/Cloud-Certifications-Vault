## What Problem Does It Solve?

Normal HTTP traffic travels:

UNENCRYPTED

across the network.

For secure applications, we need:

ENCRYPTION IN TRANSIT

Think:

CLIENT

↓

HTTPS

↓

LOAD BALANCER

↓

APPLICATION

SSL/TLS Certificates allow the connection between:

CLIENT

and

LOAD BALANCER

to be encrypted.

### Memory Trick

SSL / TLS

=

ENCRYPT DATA IN TRANSIT

---

## SSL vs TLS

SSL stands for:

SECURE SOCKETS LAYER

TLS stands for:

TRANSPORT LAYER SECURITY

TLS is:

THE NEWER VERSION

Today:

TLS CERTIFICATES

are primarily used.

However, people commonly still call them:

SSL CERTIFICATES

Think:

SSL

↓

OLDER TERM

TLS

↓

MODERN TECHNOLOGY

### Memory Trick

SSL = OLD NAME

TLS = MODERN VERSION

---

## What Does an SSL/TLS Certificate Do?

An SSL/TLS certificate allows traffic between:

CLIENT

and

LOAD BALANCER

to be:

ENCRYPTED IN TRANSIT

Think:

USER

↓

HTTPS ENCRYPTED

↓

LOAD BALANCER

### Memory Trick

HTTPS

=

HTTP + ENCRYPTION

---

## SSL/TLS Architecture

A common architecture is:

USER

↓

HTTPS

↓

LOAD BALANCER

↓

HTTP

↓

EC2 INSTANCE

Think:

PUBLIC INTERNET

↓

ENCRYPTED

PRIVATE VPC

↓

CAN USE HTTP

The Load Balancer can terminate the:

SSL / TLS CONNECTION

before forwarding traffic to backend instances.

This is known as:

SSL TERMINATION

---

## SSL Termination

SSL Termination means:

LOAD BALANCER HANDLES HTTPS

Think:

CLIENT

↓

HTTPS

↓

LOAD BALANCER

↓

DECRYPT

↓

HTTP

↓

EC2

This reduces the need for every backend EC2 instance to independently manage the public-facing SSL/TLS connection.

### Memory Trick

SSL TERMINATION

=

HTTPS STOPS AT THE LOAD BALANCER

---

## Public SSL Certificates

Public SSL/TLS certificates are issued by:

CERTIFICATE AUTHORITIES

or:

CA

Examples include certificate authorities such as:

- DigiCert
- GlobalSign
- Let's Encrypt

Think:

CERTIFICATE AUTHORITY

↓

VERIFIES CERTIFICATE

↓

CLIENT TRUSTS WEBSITE

---

## Certificate Expiration

SSL/TLS certificates have:

EXPIRATION DATES

Therefore they must be:

RENEWED

Think:

CERTIFICATE

↓

EXPIRATION DATE

↓

RENEW

### Memory Trick

CERTIFICATES

=

NOT PERMANENT

---

## Load Balancer Certificates

AWS Load Balancers use:

X.509 CERTIFICATES

These are:

SSL / TLS SERVER CERTIFICATES

Think:

HTTPS LISTENER

↓

X.509 CERTIFICATE

↓

ENCRYPTED CONNECTION

---

## AWS Certificate Manager

Certificates can be managed using:

[AWS Certificate Manager](<AWS Certificate Manager>)

or:

ACM

Think:

ACM

↓

MANAGE SSL / TLS CERTIFICATES

↓

LOAD BALANCER

You can also:

UPLOAD YOUR OWN CERTIFICATE

### Memory Trick

ACM

=

AWS CERTIFICATE MANAGER

---

## HTTPS Listener

To accept HTTPS traffic, the Load Balancer uses an:

HTTPS LISTENER

Think:

CLIENT

↓

HTTPS : 443

↓

LOAD BALANCER LISTENER

The HTTPS Listener requires:

A DEFAULT CERTIFICATE

### Memory Trick

HTTPS LISTENER

=

NEEDS CERTIFICATE

---

## Default Certificate

An HTTPS Listener must have:

ONE DEFAULT CERTIFICATE

Think:

HTTPS REQUEST

↓

LOAD BALANCER

↓

DEFAULT CERTIFICATE

The default certificate is used when another appropriate certificate cannot be selected.

---

## Multiple SSL Certificates

A Load Balancer can support:

MULTIPLE DOMAINS

with:

MULTIPLE SSL CERTIFICATES

Example:

www.example.com

↓

CERTIFICATE A

shop.example.com

↓

CERTIFICATE B

Think:

ONE LOAD BALANCER

↓

MULTIPLE HOSTNAMES

↓

MULTIPLE CERTIFICATES

This is made possible using:

SNI

---

## What Is SNI?

SNI stands for:

SERVER NAME INDICATION

SNI solves the problem of:

MULTIPLE SSL CERTIFICATES

on:

ONE LOAD BALANCER / SERVER

Think:

ONE LOAD BALANCER

↓

DOMAIN A CERTIFICATE

DOMAIN B CERTIFICATE

DOMAIN C CERTIFICATE

### Memory Trick

SNI

=

SELECT THE RIGHT CERTIFICATE

---

## How SNI Works

During the initial:

SSL / TLS HANDSHAKE

the client tells the server:

WHICH HOSTNAME IT WANTS

Think:

CLIENT

↓

"I WANT www.example.com"

↓

LOAD BALANCER

↓

SELECT www.example.com CERTIFICATE

If the Load Balancer has the correct certificate:

USE CORRECT CERTIFICATE

Otherwise:

USE DEFAULT CERTIFICATE

### Memory Trick

SNI

=

CLIENT SAYS HOSTNAME FIRST

---

## SNI Architecture

Imagine one ALB serving:

domain1.example.com

and:

www.mycorp.com

The ALB has:

CERTIFICATE #1

↓

domain1.example.com

CERTIFICATE #2

↓

www.mycorp.com

Client requests:

www.mycorp.com

↓

SNI

↓

ALB SELECTS CERTIFICATE #2

↓

CORRECT TARGET GROUP

Think:

HOSTNAME

↓

CORRECT CERTIFICATE

↓

CORRECT APPLICATION

---

## SNI Support

SNI works with newer-generation Load Balancers:

APPLICATION LOAD BALANCER

and:

NETWORK LOAD BALANCER

It also works with:

CLOUDFRONT

Think:

ALB

=

SNI

NLB

=

SNI

CLOUDFRONT

=

SNI

---

## SNI and Classic Load Balancer

Classic Load Balancer does:

NOT

support SNI.

Think:

CLB

↓

OLDER GENERATION

↓

NO SNI

### Memory Trick

SNI

=

NEWER LOAD BALANCERS

NOT CLB

---

## Classic Load Balancer Certificates

Classic Load Balancer supports:

ONE SSL CERTIFICATE

Think:

ONE CLB

↓

ONE CERTIFICATE

If you need:

MULTIPLE HOSTNAMES

with:

MULTIPLE SSL CERTIFICATES

you would need:

MULTIPLE CLASSIC LOAD BALANCERS

### Memory Trick

CLB

=

ONE CERT

---

## Application Load Balancer Certificates

Application Load Balancer supports:

MULTIPLE LISTENERS

and:

MULTIPLE SSL CERTIFICATES

It uses:

SNI

to select the correct certificate.

Think:

ALB

↓

MULTIPLE CERTIFICATES

↓

SNI

### Memory Trick

ALB

=

MULTI-CERT + SNI

---

## Network Load Balancer Certificates

Network Load Balancer also supports:

MULTIPLE LISTENERS

and:

MULTIPLE SSL CERTIFICATES

It uses:

SNI

to select the correct certificate.

Think:

NLB

↓

MULTIPLE CERTIFICATES

↓

SNI

### Memory Trick

NLB

=

MULTI-CERT + SNI

---

## Certificate Comparison

### Classic Load Balancer

CERTIFICATES

=

ONE

SNI

=

NO

Think:

CLB

=

OLD + ONE CERT

---

### Application Load Balancer

CERTIFICATES

=

MULTIPLE

SNI

=

YES

Think:

ALB

=

MULTI-CERT

---

### Network Load Balancer

CERTIFICATES

=

MULTIPLE

SNI

=

YES

Think:

NLB

=

MULTI-CERT

---

## SSL/TLS Security Policy

An HTTPS listener can use a:

SECURITY POLICY

The security policy determines which:

SSL / TLS PROTOCOL VERSIONS

and related security settings are supported.

Think:

CLIENT

↓

SSL / TLS VERSION

↓

LOAD BALANCER SECURITY POLICY

This can be important when supporting:

LEGACY CLIENTS

that require older SSL/TLS versions.

### Memory Trick

SECURITY POLICY

=

WHICH TLS VERSIONS ARE ALLOWED?

---

## SSL Certificate Architecture Thinking

Imagine:

INTERNET USERS

↓

HTTPS

↓

ALB

↓

HTTP

↓

PRIVATE EC2 INSTANCES

The ALB handles:

CERTIFICATE

↓

TLS HANDSHAKE

↓

ENCRYPTION / DECRYPTION

The EC2 instances focus on:

APPLICATION PROCESSING

Think:

ALB

=

PUBLIC HTTPS FRONT DOOR

---

## Multiple Domain Architecture

Imagine:

shop.example.com

and:

api.example.com

both use the same:

APPLICATION LOAD BALANCER

Think:

CLIENT

↓

HTTPS

↓

SNI HOSTNAME

↓

ALB

Then:

shop.example.com

↓

SHOP CERTIFICATE

↓

SHOP TARGET GROUP

and:

api.example.com

↓

API CERTIFICATE

↓

API TARGET GROUP

### Memory Trick

ONE ALB

+

SNI

=

MULTIPLE HTTPS WEBSITES

---

## Scenario Recognition

Need encryption between clients and a Load Balancer?

→ SSL/TLS Certificate

---

Need HTTPS?

→ SSL/TLS Certificate

---

Need AWS to manage Load Balancer certificates?

→ AWS Certificate Manager

---

Need an HTTPS Listener?

→ Configure a certificate

---

Need one Load Balancer to host multiple HTTPS domains with different certificates?

→ SNI

---

Need the client to indicate the hostname during the TLS handshake?

→ SNI

---

Need multiple SSL certificates on an ALB?

→ SNI

---

Need multiple SSL certificates on an NLB?

→ SNI

---

Need multiple SSL certificates on a Classic Load Balancer?

→ Not supported with SNI

Think:

MULTIPLE CLBs

---

Need support for legacy SSL/TLS clients?

→ Load Balancer Security Policy

---

## Exam Traps

SSL / TLS

=

ENCRYPTION IN TRANSIT

---

TLS

=

NEWER THAN SSL

---

LOAD BALANCER CERTIFICATE

=

X.509 CERTIFICATE

---

ACM

=

MANAGE SSL / TLS CERTIFICATES

---

HTTPS LISTENER

=

DEFAULT CERTIFICATE REQUIRED

---

SNI

=

SERVER NAME INDICATION

---

SNI

=

MULTIPLE CERTIFICATES ON ONE LOAD BALANCER

---

SNI

=

CLIENT SENDS HOSTNAME DURING TLS HANDSHAKE

---

ALB

=

SNI SUPPORTED

---

NLB

=

SNI SUPPORTED

---

CLB

=

SNI NOT SUPPORTED

---

CLB

=

ONE SSL CERTIFICATE

---

ALB / NLB

=

MULTIPLE SSL CERTIFICATES

---

SECURITY POLICY

=

SUPPORTED SSL / TLS VERSIONS

---

## Quick Cheat Sheet

SSL

=

SECURE SOCKETS LAYER

TLS

=

TRANSPORT LAYER SECURITY

TLS

=

NEWER VERSION

PURPOSE

=

ENCRYPTION IN TRANSIT

HTTPS

=

ENCRYPTED HTTP

CERTIFICATE TYPE

=

X.509

CERTIFICATE MANAGEMENT

=

ACM

HTTPS LISTENER

=

CERTIFICATE REQUIRED

DEFAULT CERTIFICATE

=

REQUIRED

SNI

=

SERVER NAME INDICATION

SNI PURPOSE

=

MULTIPLE CERTIFICATES

ALB SNI

=

YES

NLB SNI

=

YES

CLB SNI

=

NO

CLB CERTIFICATES

=

ONE

ALB / NLB CERTIFICATES

=

MULTIPLE

SECURITY POLICY

=

TLS VERSION SUPPORT

---

## Master Memory Trick

CLIENT

↓

HTTPS

↓

SSL / TLS CERTIFICATE

↓

LOAD BALANCER

↓

HTTP

↓

EC2

And:

ONE DOMAIN

↓

ONE CERTIFICATE

MULTIPLE DOMAINS

↓

MULTIPLE CERTIFICATES

↓

SNI

Remember:

ALB

=

SNI

NLB

=

SNI

CLB

=

NO SNI

Think:

SNI

=

"WHICH WEBSITE ARE YOU TRYING TO REACH?"

↓

LOAD BALANCER SELECTS CORRECT CERTIFICATE

---

## Related Notes

- [Elastic Load Balancing](<Elastic Load Balancing>)
- [Application Load Balancer](<Application Load Balancer>)
- [Network Load Balancer](<Network Load Balancer>)
- [Gateway Load Balancer](<Gateway Load Balancer>)
- [Load Balancer Stickiness](<Load Balancer Stickiness>)
- [Cross-Zone Load Balancing](<Cross-Zone Load Balancing>)
- [AWS Certificate Manager](<AWS Certificate Manager>)
- [CloudFront](05-Networking/CloudFront.md)
- [Auto Scaling Groups](<Auto Scaling Groups>)
- [SAA High Availability Cheat Sheet](<SAA High Availability Cheat Sheet>)