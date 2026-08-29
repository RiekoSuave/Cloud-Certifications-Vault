## What Problem Does It Solve?

An Auto Scaling Group needs a way to measure:

HOW BUSY THE APPLICATION IS

before deciding whether to:

SCALE OUT

or:

SCALE IN

Scaling Metrics provide the:

SIGNALS

used by Auto Scaling policies.

Think:

APPLICATION LOAD

↓

METRIC

↓

CLOUDWATCH

↓

SCALING POLICY

↓

AUTO SCALING GROUP

### Memory Trick

METRIC

=

MEASURE THE LOAD

---

## What Is a Scaling Metric?

A Scaling Metric is a value that represents:

APPLICATION DEMAND

or:

RESOURCE UTILIZATION

Think:

CPU

REQUESTS

NETWORK TRAFFIC

CUSTOM APPLICATION LOAD

↓

METRIC

↓

ASG DECISION

The goal is to choose a metric that accurately reflects:

HOW MUCH CAPACITY THE APPLICATION NEEDS

---

## Good Metrics to Scale On

Your course highlights four important options:

CPUUtilization

↓

RequestCountPerTarget

↓

Average Network In / Out

↓

Custom CloudWatch Metrics

Think:

CPU-BOUND?

↓

CPUUtilization

REQUEST-BOUND?

↓

RequestCountPerTarget

NETWORK-BOUND?

↓

Network In / Out

SPECIAL APPLICATION SIGNAL?

↓

Custom Metric

---

## CPUUtilization

CPUUtilization measures:

AVERAGE CPU UTILIZATION

across the EC2 instances in the:

AUTO SCALING GROUP

Think:

EC2 #1 CPU

+

EC2 #2 CPU

+

EC2 #3 CPU

↓

AVERAGE CPU

↓

ASG SCALING DECISION

### Example

Target:

40% CPU

CPU rises above target:

↓

SCALE OUT

CPU falls below target:

↓

SCALE IN

### Memory Trick

CPU-BOUND APP

=

SCALE ON CPU

---

## When CPUUtilization Is a Good Metric

Use CPUUtilization when application demand is strongly related to:

CPU USAGE

Examples:

- Compute-heavy applications
- Processing workloads
- CPU-intensive web applications

Think:

MORE USERS

↓

MORE CPU

↓

CPU IS A GOOD SIGNAL

---

## CPUUtilization Limitation

CPU is not always the best representation of:

APPLICATION LOAD

Imagine:

REQUESTS ↑

but:

CPU REMAINS LOW

The application may still need more instances because of another bottleneck.

Think:

WRONG METRIC

↓

WRONG SCALING DECISION

### Exam Thinking

Choose the metric that best represents:

THE ACTUAL BOTTLENECK

---

## RequestCountPerTarget

RequestCountPerTarget measures:

HOW MANY REQUESTS

each Load Balancer target receives.

Think:

USERS

↓

[Application Load Balancer](<Application Load Balancer>)

↓

REQUEST COUNT

↓

TARGETS

This metric helps keep:

REQUESTS PER EC2 INSTANCE

at a stable level.

### Memory Trick

RequestCountPerTarget

=

HOW BUSY EACH TARGET IS

---

## RequestCountPerTarget Example

Imagine the desired target is:

1000 REQUESTS PER TARGET

You currently have:

2 EC2 INSTANCES

Traffic increases:

3000 REQUESTS

↓

1500 REQUESTS PER TARGET

This is above the desired level.

ASG can:

SCALE OUT

↓

ADD EC2

Now:

3000 REQUESTS

↓

3 EC2 INSTANCES

↓

1000 REQUESTS PER TARGET

### Memory Trick

MORE REQUESTS PER TARGET

↓

ADD TARGETS

---

## When RequestCountPerTarget Is a Good Metric

Use RequestCountPerTarget when:

WEB REQUEST VOLUME

is a strong indicator of application demand.

Think:

MORE HTTP REQUESTS

↓

MORE BACKEND CAPACITY NEEDED

This works especially well with:

APPLICATION LOAD BALANCER

+

AUTO SCALING GROUP

---

## CPU vs RequestCountPerTarget

### CPUUtilization

Measures:

SERVER COMPUTE LOAD

Think:

HOW HARD IS THE CPU WORKING?

---

### RequestCountPerTarget

Measures:

APPLICATION REQUEST LOAD

Think:

HOW MANY REQUESTS IS EACH TARGET HANDLING?

### Memory Trick

CPU

=

MACHINE LOAD

REQUEST COUNT

=

APPLICATION TRAFFIC

---

## Average Network In

Average Network In measures:

INCOMING NETWORK TRAFFIC

to the EC2 instances.

Think:

DATA ENTERING EC2

↓

NETWORK IN

If your application receives large amounts of incoming network data:

NETWORK IN

may be a useful scaling metric.

### Memory Trick

NETWORK IN

=

DATA COMING INTO EC2

---

## Average Network Out

Average Network Out measures:

OUTGOING NETWORK TRAFFIC

from EC2 instances.

Think:

DATA LEAVING EC2

↓

NETWORK OUT

If your application sends large amounts of data:

NETWORK OUT

may accurately represent load.

### Memory Trick

NETWORK OUT

=

DATA LEAVING EC2

---

## When Network Metrics Are Good

Use:

AVERAGE NETWORK IN

or:

AVERAGE NETWORK OUT

when your application is:

NETWORK-BOUND

Think:

APPLICATION BOTTLENECK

=

NETWORK

↓

SCALE ON NETWORK METRIC

Examples might include workloads where instances:

RECEIVE

or:

SEND

large amounts of data.

### Memory Trick

NETWORK-BOUND

=

SCALE ON NETWORK

---

## Custom Metrics

Sometimes none of the standard metrics accurately reflect:

APPLICATION DEMAND

In that case:

PUSH A CUSTOM METRIC

to:

[CloudWatch](07-Monitoring/CloudWatch.md)

Think:

APPLICATION

↓

CUSTOM BUSINESS METRIC

↓

CLOUDWATCH

↓

SCALING POLICY

↓

ASG

### Memory Trick

CUSTOM WORKLOAD

=

CUSTOM METRIC

---

## Custom Metric Example

Imagine an application processes:

JOBS IN A QUEUE

CPU utilization might remain low even while:

QUEUE LENGTH

continues growing.

Think:

QUEUE

↓

10 JOBS

↓

100 JOBS

↓

1000 JOBS

A better metric might be:

QUEUE DEPTH

Then:

QUEUE DEPTH ↑

↓

ASG SCALE OUT

QUEUE DEPTH ↓

↓

ASG SCALE IN

### Exam Thinking

If the question describes a workload-specific bottleneck:

THINK CUSTOM CLOUDWATCH METRIC

---

## Choosing the Right Metric

Do not automatically choose:

CPU

Ask:

WHAT ACTUALLY REPRESENTS APPLICATION LOAD?

Think:

CPU-BOUND?

↓

CPUUtilization

REQUEST-BOUND?

↓

RequestCountPerTarget

NETWORK-BOUND?

↓

Network In / Out

APPLICATION-SPECIFIC?

↓

Custom Metric

### Memory Trick

SCALE ON THE BOTTLENECK

---

## Scaling Metrics + Target Tracking

Metrics are commonly used with:

[Auto Scaling Group Scaling Policies](<Auto Scaling Group Scaling Policies>)

especially:

TARGET TRACKING

Example:

METRIC

=

CPUUtilization

TARGET

=

40%

or:

METRIC

=

RequestCountPerTarget

TARGET

=

1000

Think:

METRIC

+

TARGET VALUE

↓

TARGET TRACKING

↓

ASG ADJUSTS CAPACITY

---

## Scaling Metrics + CloudWatch

Auto Scaling metrics are monitored using:

CLOUDWATCH

Think:

EC2 / ALB / APPLICATION

↓

METRIC

↓

CLOUDWATCH

↓

ALARM / SCALING POLICY

↓

ASG

CloudWatch provides the:

OBSERVATION

The Auto Scaling Group performs the:

ACTION

### Memory Trick

CLOUDWATCH

=

MEASURE

ASG

=

RESPOND

---

## Scaling Metrics Architecture

Imagine:

USERS

↓

ALB

↓

AUTO SCALING GROUP

↓

EC2 EC2 EC2

CloudWatch monitors:

RequestCountPerTarget

Suppose:

TARGET

=

1000 REQUESTS

Traffic increases:

REQUESTS PER TARGET

↓

1500

↓

SCALING POLICY

↓

ASG SCALE OUT

↓

ADD EC2

↓

REQUESTS PER TARGET FALL

Think:

METRIC

↓

DECISION

↓

CAPACITY

---

## Metric Should Change With Capacity

A useful scaling metric should generally respond when:

CAPACITY CHANGES

Think:

LOAD ↑

↓

METRIC ↑

↓

ADD INSTANCES

↓

METRIC PER INSTANCE ↓

This allows Auto Scaling to:

STABILIZE

around the desired target.

### Example

RequestCountPerTarget:

MORE INSTANCES

↓

FEWER REQUESTS PER TARGET

This makes it a strong metric for:

TARGET TRACKING

---

## Bad Metric Thinking

Imagine scaling on a metric that does not change when capacity increases.

Think:

METRIC HIGH

↓

ADD INSTANCES

↓

METRIC STILL HIGH

↓

ADD MORE INSTANCES

This can lead to:

POOR SCALING BEHAVIOR

### SAA Thinking

Choose a metric that meaningfully reflects:

LOAD PER UNIT OF CAPACITY

when possible.

---

## Scenario Recognition

Application is CPU-bound?

→ CPUUtilization

---

Need average CPU across the ASG to remain around 40%?

→ CPUUtilization + Target Tracking

---

Need to keep requests per backend EC2 instance stable?

→ RequestCountPerTarget

---

Need to scale based on HTTP request volume behind an ALB?

→ RequestCountPerTarget

---

Application receives massive inbound network traffic?

→ Average Network In

---

Application sends massive outbound network traffic?

→ Average Network Out

---

Application is network-bound?

→ Network In / Out

---

Need to scale based on application-specific workload?

→ Custom CloudWatch Metric

---

CPU is low but a work queue continues growing?

→ Custom Metric such as Queue Depth

---

Need ASG scaling based on something CloudWatch can monitor?

→ CloudWatch Metric + Scaling Policy

---

## Exam Traps

CPUUtilization

=

AVERAGE CPU ACROSS ASG

---

RequestCountPerTarget

=

REQUEST LOAD PER TARGET

---

NETWORK-BOUND APPLICATION

=

NETWORK IN / OUT

---

CUSTOM APPLICATION DEMAND

=

CUSTOM CLOUDWATCH METRIC

---

CPU

≠

ALWAYS THE BEST METRIC

---

BEST SCALING METRIC

=

METRIC THAT REPRESENTS ACTUAL LOAD

---

CLOUDWATCH

=

MONITORS METRIC

ASG

=

CHANGES CAPACITY

---

RequestCountPerTarget

=

GOOD FOR ALB + ASG ARCHITECTURES

---

CUSTOM METRICS

=

PUSH TO CLOUDWATCH

---

## Quick Cheat Sheet

CPUUtilization

=

AVERAGE CPU ACROSS INSTANCES

BEST FOR

=

CPU-BOUND WORKLOADS

RequestCountPerTarget

=

REQUESTS PER BACKEND TARGET

BEST FOR

=

REQUEST-DRIVEN WEB APPLICATIONS

Average Network In

=

INCOMING NETWORK DATA

Average Network Out

=

OUTGOING NETWORK DATA

NETWORK METRICS

=

NETWORK-BOUND WORKLOADS

CUSTOM METRIC

=

APPLICATION-SPECIFIC LOAD

METRIC MONITORING

=

CLOUDWATCH

SCALING ACTION

=

AUTO SCALING GROUP

BEST RULE

=

SCALE ON THE ACTUAL BOTTLENECK

---

## Master Memory Trick

ASK:

WHAT MAKES THE APPLICATION BUSY?

CPU?

↓

CPUUtilization

REQUESTS?

↓

RequestCountPerTarget

NETWORK?

↓

Network In / Out

SOMETHING UNIQUE?

↓

Custom Metric

Think:

APPLICATION

↓

LOAD SIGNAL

↓

CLOUDWATCH METRIC

↓

SCALING POLICY

↓

ASG

↓

RIGHT NUMBER OF EC2 INSTANCES

### Master Rule

DON'T SCALE ON A METRIC JUST BECAUSE IT EXISTS

↓

SCALE ON THE METRIC THAT REPRESENTS THE WORKLOAD

---

## Related Notes

- [Auto Scaling Groups](<Auto Scaling Groups>)
- [Auto Scaling Group Scaling Policies](<Auto Scaling Group Scaling Policies>)
- [Application Load Balancer](<Application Load Balancer>)
- [Elastic Load Balancing](<Elastic Load Balancing>)
- [CloudWatch](07-Monitoring/CloudWatch.md)
- [EC2](EC2)
- [Scalability & High Availability](<Scalability & High Availability>)
- [SAA High Availability Cheat Sheet](<SAA High Availability Cheat Sheet>)