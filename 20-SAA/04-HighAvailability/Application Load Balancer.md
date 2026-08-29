## What Problem Does It Solve?

A basic Load Balancer can distribute traffic across multiple servers.

But modern applications often need:

SMART HTTP ROUTING

For example:

/users

↓

USER SERVICE

/posts

↓

POST SERVICE

/images

↓

IMAGE SERVICE

The:

APPLICATION LOAD BALANCER

or:

ALB

solves this problem.

### Memory Trick

ALB

=

SMART HTTP ROUTER

---

## What Is an Application Load Balancer?

Application Load Balancer operates at:

LAYER 7

of the OSI model.

Layer 7 means:

HTTP

and:

HTTPS

Think:

CLIENT

↓

HTTP / HTTPS

↓

ALB

↓

APPLICATION SERVERS

### Memory Trick

ALB = LAYER 7

---

## ALB Protocols

Application Load Balancer supports:

HTTP

HTTPS

WebSocket

It is designed specifically for:

WEB TRAFFIC

Think:

WEB APPLICATION

↓

HTTP / HTTPS

↓

ALB

---

## ALB Architecture

A typical architecture looks like:

USERS

↓

APPLICATION LOAD BALANCER

↓

TARGET GROUP

↓

EC2 #1

EC2 #2

EC2 #3

The ALB receives requests and forwards them to:

TARGET GROUPS

### Memory Trick

ALB

↓

TARGET GROUP

↓

TARGETS

---

## What Is a Target Group?

A Target Group represents:

A GROUP OF BACKEND RESOURCES

that receive traffic from the Load Balancer.

Think:

ALB

↓

TARGET GROUP

↓

BACKEND APPLICATION

Targets can include:

- EC2 instances
- ECS tasks
- Lambda functions
- Private IP addresses

### Memory Trick

TARGET GROUP

=

WHERE ALB SENDS TRAFFIC

---

## ALB and EC2

A common architecture is:

USERS

↓

ALB

↓

TARGET GROUP

↓

EC2 INSTANCES

Think:

INTERNET TRAFFIC

↓

ALB

↓

HEALTHY EC2

---

## ALB and ECS

Application Load Balancer works especially well with:

ECS

Think:

ALB

↓

TARGET GROUP

↓

ECS TASKS

This is useful for:

CONTAINERIZED APPLICATIONS

We'll cover ECS later in:

[[02-Compute/ECS]]

---

## ALB and Lambda

ALB can also route requests to:

LAMBDA FUNCTIONS

Think:

HTTP REQUEST

↓

ALB

↓

LAMBDA

This provides another way to expose serverless application logic.

We'll cover Lambda later in:

[[02-Compute/Lambda]]

---

## ALB and Private IP Addresses

Target Groups can contain:

PRIVATE IP ADDRESSES

Think:

ALB

↓

PRIVATE IP TARGET

This means the target does not necessarily have to be a directly registered EC2 instance.

---

## Health Checks

ALB performs:

HEALTH CHECKS

against its Target Groups.

Think:

ALB

↓

HEALTH CHECK

↓

TARGET

If:

TARGET HEALTHY

↓

SEND TRAFFIC

If:

TARGET UNHEALTHY

↓

STOP SENDING TRAFFIC

### Memory Trick

ALB

=

ROUTE ONLY TO HEALTHY TARGETS

---

## Listener

An ALB uses:

LISTENERS

A Listener checks for connection requests using a configured:

PROTOCOL

and:

PORT

Example:

HTTPS

↓

PORT 443

Think:

CLIENT

↓

HTTPS : 443

↓

ALB LISTENER

↓

LISTENER RULES

↓

TARGET GROUP

### Memory Trick

LISTENER

=

ALB FRONT DOOR

---

## Listener Rules

Listener Rules determine:

WHERE REQUESTS SHOULD GO

Think:

REQUEST ARRIVES

↓

LISTENER

↓

CHECK RULE

↓

FORWARD TO TARGET GROUP

This allows ALB to make routing decisions based on information inside the HTTP request.

---

## Path-Based Routing

ALB supports:

PATH-BASED ROUTING

Example:

example.com/users

↓

USER TARGET GROUP

example.com/posts

↓

POST TARGET GROUP

Think:

/users

↓

SERVICE A

/posts

↓

SERVICE B

### Memory Trick

PATH

=

WHERE IN THE URL?

---

## Path-Based Routing Architecture

Imagine:

USERS

↓

ALB

Then:

/users

↓

TARGET GROUP A

↓

USER SERVICE

and:

/search

↓

TARGET GROUP B

↓

SEARCH SERVICE

This allows:

ONE LOAD BALANCER

to route traffic to:

MULTIPLE APPLICATIONS

---

## Host-Based Routing

ALB also supports:

HOST-BASED ROUTING

Think:

one.example.com

↓

TARGET GROUP A

two.example.com

↓

TARGET GROUP B

The ALB examines the:

HOSTNAME

and routes the request accordingly.

### Memory Trick

HOST

=

WHICH DOMAIN?

---

## Host-Based Routing Architecture

Imagine:

mobile.example.com

↓

ALB

↓

MOBILE APPLICATION

and:

shop.example.com

↓

ALB

↓

SHOP APPLICATION

Think:

SAME ALB

↓

DIFFERENT HOSTNAMES

↓

DIFFERENT BACKENDS

---

## Query String Routing

ALB can also route based on:

QUERY STRINGS

and:

HTTP HEADERS

Example:

example.com/products?id=123

The ALB can inspect HTTP request information and make routing decisions.

Think:

HTTP REQUEST DETAILS

↓

ALB RULES

↓

CORRECT TARGET GROUP

---

## ALB Is Great for Microservices

ALB is especially useful for:

MICROSERVICES

and:

CONTAINER-BASED APPLICATIONS

Imagine:

APPLICATION

↓

/users

↓

USER MICROSERVICE

/products

↓

PRODUCT MICROSERVICE

/orders

↓

ORDER MICROSERVICE

One ALB can route requests to the correct service.

### Memory Trick

MICROSERVICES

LOVE

ALB

---

## ALB and Multiple Applications

Without ALB routing:

APPLICATION A

↓

LOAD BALANCER A

APPLICATION B

↓

LOAD BALANCER B

APPLICATION C

↓

LOAD BALANCER C

With ALB:

ONE ALB

↓

MULTIPLE TARGET GROUPS

↓

MULTIPLE APPLICATIONS

Think:

ONE SMART LOAD BALANCER

↓

MANY APPLICATIONS

---

## ALB and Containers

Containers may run on:

DYNAMIC PORTS

For example:

EC2 HOST

↓

CONTAINER A : PORT 32768

CONTAINER B : PORT 32769

CONTAINER C : PORT 32770

ALB can route traffic to the correct:

PORT

on the backend target.

This makes ALB useful with:

[[02-Compute/ECS]]

### Memory Trick

ALB

=

CONTAINER FRIENDLY

---

## ALB Fixed Hostname

Application Load Balancer provides:

A FIXED DNS HOSTNAME

You do not receive:

A FIXED STATIC IP ADDRESS

for the ALB itself.

Think:

ALB

=

FIXED HOSTNAME

NOT

FIXED IP

### Exam Trap

Need a static IP?

Do not automatically choose:

ALB

Think instead about:

[[Network Load Balancer]]

---

## Client IP Address

When a client connects through an ALB:

CLIENT

↓

ALB

↓

EC2

The backend EC2 instance sees the ALB connection rather than using the original client IP as the source IP at the network layer.

To obtain the original client IP, ALB adds the:

X-FORWARDED-FOR

header.

Think:

CLIENT IP

↓

X-FORWARDED-FOR

↓

BACKEND APPLICATION

### Memory Trick

ALB CLIENT IP

=

X-FORWARDED-FOR

---

## X-Forwarded Headers

ALB can provide information about the original client request using headers such as:

X-FORWARDED-FOR

↓

ORIGINAL CLIENT IP

X-FORWARDED-PORT

↓

ORIGINAL PORT

X-FORWARDED-PROTO

↓

ORIGINAL PROTOCOL

Think:

ALB TERMINATES CONNECTION

↓

HEADERS PRESERVE CLIENT INFORMATION

---

## ALB Security Groups

Application Load Balancers support:

SECURITY GROUPS

A common architecture is:

INTERNET

↓

ALB SECURITY GROUP

↓

ALB

↓

EC2 SECURITY GROUP

↓

EC2

The EC2 Security Group can allow traffic specifically from:

THE ALB SECURITY GROUP

### Memory Trick

INTERNET

↓

ALB

↓

EC2

NOT

INTERNET

↓

EC2 DIRECTLY

---

## Internet-Facing ALB

An ALB can be:

INTERNET-FACING

Think:

INTERNET

↓

PUBLIC ALB

↓

PRIVATE EC2 INSTANCES

This is common for:

PUBLIC WEB APPLICATIONS

---

## Internal ALB

An ALB can also be:

INTERNAL

Think:

APPLICATION TIER

↓

INTERNAL ALB

↓

BACKEND SERVICES

This is useful when the Load Balancer should only be accessible from:

PRIVATE NETWORKS

### Memory Trick

PUBLIC USERS

↓

INTERNET-FACING ALB

PRIVATE APPLICATION TRAFFIC

↓

INTERNAL ALB

---

## ALB vs Classic Load Balancer

Classic Load Balancer is the:

OLDER GENERATION

Application Load Balancer provides more advanced:

HTTP ROUTING

Think:

CLB

=

OLD / BASIC

ALB

=

SMART HTTP ROUTING

For modern HTTP/HTTPS architectures:

THINK ALB

---

## ALB vs Network Load Balancer

### ALB

LAYER 7

↓

HTTP / HTTPS

↓

SMART ROUTING

### NLB

LAYER 4

↓

TCP / UDP

↓

EXTREME PERFORMANCE

Think:

HTTP DETAILS?

↓

ALB

NETWORK CONNECTION?

↓

NLB

---

## Architecture Thinking

Imagine an online application:

USERS

↓

ALB

Then:

/shop

↓

SHOP TARGET GROUP

↓

EC2 / ECS

/orders

↓

ORDER TARGET GROUP

↓

EC2 / ECS

/images

↓

IMAGE TARGET GROUP

↓

EC2 / ECS

The ALB provides:

ONE ENTRY POINT

↓

MULTIPLE ROUTING RULES

↓

MULTIPLE APPLICATION SERVICES

---

## Scenario Recognition

Need HTTP or HTTPS load balancing?

→ Application Load Balancer

---

Need Layer 7 load balancing?

→ Application Load Balancer

---

Need path-based routing?

→ Application Load Balancer

---

Need:

/users

and:

/products

sent to different applications?

→ Application Load Balancer

---

Need host-based routing?

→ Application Load Balancer

---

Need multiple domains routed through one Load Balancer?

→ Application Load Balancer

---

Need routing based on query strings or HTTP headers?

→ Application Load Balancer

---

Need one Load Balancer for multiple microservices?

→ Application Load Balancer

---

Need dynamic port mapping for containers?

→ Application Load Balancer

---

Need ECS tasks behind a Load Balancer?

→ Application Load Balancer

---

Need Lambda as a Load Balancer target?

→ Application Load Balancer

---

Need backend private IP addresses as targets?

→ Application Load Balancer

---

Need original client IP in an HTTP application?

→ X-Forwarded-For

---

Need a static IP address for the Load Balancer?

→ Think Network Load Balancer

NOT ALB

---

## Exam Traps

ALB

=

LAYER 7

ALB

=

HTTP / HTTPS

ALB

=

SMART ROUTING

---

PATH-BASED ROUTING

=

ALB

---

HOST-BASED ROUTING

=

ALB

---

QUERY STRING / HTTP HEADER ROUTING

=

ALB

---

ALB

=

TARGET GROUPS

---

TARGETS CAN INCLUDE

=

EC2

ECS TASKS

LAMBDA

PRIVATE IPs

---

ALB

=

FIXED DNS HOSTNAME

ALB

≠

FIXED STATIC IP

---

ORIGINAL CLIENT IP

=

X-FORWARDED-FOR

---

ALB

=

MICROSERVICES + CONTAINERS

---

ALB

≠

BEST CHOICE FOR RAW TCP / UDP

That points toward:

NLB

---

## Quick Cheat Sheet

ALB

=

APPLICATION LOAD BALANCER

OSI LAYER

=

LAYER 7

PROTOCOLS

=

HTTP / HTTPS

ROUTING

=

PATH

HOST

QUERY STRING

HTTP HEADERS

BACKENDS

=

TARGET GROUPS

TARGET TYPES

=

EC2

ECS

LAMBDA

PRIVATE IP

HEALTH CHECKS

=

YES

SECURITY GROUPS

=

YES

MICROSERVICES

=

ALB

CONTAINERS

=

ALB

DYNAMIC PORT MAPPING

=

SUPPORTED

FIXED DNS

=

YES

FIXED STATIC IP

=

NO

CLIENT IP

=

X-FORWARDED-FOR

---

## Master Memory Trick

ALB

=

APPLICATION-AWARE LOAD BALANCER

Think:

HTTP REQUEST

↓

ALB READS REQUEST

↓

HOST?

PATH?

QUERY?

HEADER?

↓

CHOOSE TARGET GROUP

↓

HEALTHY TARGET

And:

ALB

=

LAYER 7

↓

HTTP / HTTPS

↓

SMART ROUTING

↓

MICROSERVICES

↓

CONTAINERS

---

## Related Notes

- [[Scalability & High Availability]]
- [[Elastic Load Balancing]]
- [[Network Load Balancer]]
- [[Gateway Load Balancer]]
- [[Load Balancer Stickiness]]
- [[Cross-Zone Load Balancing]]
- [[Auto Scaling Groups]]
- [[EC2]]
- [[EC2 Security Groups]]
- [[02-Compute/ECS]]
- [[02-Compute/Lambda]]
- [[SAA High Availability Cheat Sheet]]