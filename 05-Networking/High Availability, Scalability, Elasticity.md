See also: [[Elastic Load Balancing (ELB)]]

See also: [[05-Networking/VPC]]
## What Problem Does It Solve?

Explains how AWS architectures handle changing workloads, maintain availability, and automatically adjust resources based on demand.

These concepts help applications:

- Handle increased traffic
- Reduce downtime
- Survive infrastructure failures
- Automatically adjust capacity
- Optimize resource usage and cost

---

## Related Concepts

### Scalability

The ability of a system to handle increased load.

Two Types:

- Vertical Scaling
- Horizontal Scaling

---

### Vertical Scaling

Increase the size of an existing instance.

Example:

t2.micro → t2.large

Benefits:

- Easy to implement
- Common for databases

Limitations:

- Hardware limits exist
- Eventually cannot scale further

### Memory Trick

Vertical = Scale Up

---

### Horizontal Scaling

Increase the number of instances.

Example:

1 EC2 Instance → 10 EC2 Instances

Benefits:

- Better fault tolerance
- Better scalability
- Common for web applications

### Memory Trick

Horizontal = Scale Out

---

### High Availability

Running applications across multiple Availability Zones.

Goal:

Survive the failure of an Availability Zone or data center.

Benefits:

- Fault tolerance
- Disaster recovery
- Reduced downtime

### Memory Trick

Multi-AZ = High Availability

---

### Elasticity

Ability to automatically scale resources up and down based on demand.

Benefits:

- Cost optimization
- Pay only for what is needed
- Matches workload demand

Example:

Traffic increases → Add servers

Traffic decreases → Remove servers

### Memory Trick

Elasticity = Auto Scaling

---

### Agility

Ability to provision resources quickly.

Example:

Create infrastructure in minutes instead of weeks.

### Exam Tip

Agility is NOT the same as scalability.

## Auto Scaling Groups (ASG)

### What Problem Does It Solve?

Automatically adjusts the number of EC2 instances based on demand.

The goal of an Auto Scaling Group is to:

- Scale Out when demand increases
- Scale In when demand decreases
- Maintain minimum capacity
- Maintain maximum capacity
- Replace unhealthy instances
- Automatically register new instances with a load balancer

### Memory Trick

ASG = Add / Remove Servers

---

## Auto Scaling Strategies

### Manual Scaling

Manually change the size of the Auto Scaling Group.

---

### Dynamic Scaling

Automatically responds to changing demand.

Example:

CPU > 70%

→ Add instances

CPU < 30%

→ Remove instances

---

### Target Tracking Scaling

Maintains a target metric.

Example:

Keep average CPU utilization around 40%.

### Memory Trick

Target Tracking = Thermostat

---

### Scheduled Scaling

Adjusts capacity based on known usage patterns.

Example:

Increase capacity every Friday at 5 PM.

### Memory Trick

Scheduled = Known Schedule

---

### Predictive Scaling

Uses Machine Learning to predict future traffic.

AWS can provision EC2 instances in advance based on expected demand.

Best For:

Predictable time-based workload patterns.

### Memory Trick

Predictive = Forecast Demand

---

## ASG Benefits

### Scalability

Automatically adds or removes EC2 instances.

### High Availability

Can maintain instances across multiple Availability Zones.

### Automatic Recovery

Can replace unhealthy instances.

### Cost Optimization

Helps avoid running unnecessary EC2 capacity.

### ELB Integration

New instances can automatically register with an Elastic Load Balancer.

---

## ELB vs Auto Scaling

| Service | Purpose |
|----------|----------|
| ELB | Distributes traffic |
| Auto Scaling | Adjusts capacity |
| ELB + ASG | High Availability + Scalability |

---

## Scenario Questions

A company wants to distribute traffic across multiple EC2 instances.

Answer:

Elastic Load Balancer

---

A company wants to automatically add servers when CPU reaches 80%.

Answer:

Auto Scaling Group

---

A company wants applications to survive an Availability Zone failure.

Answer:

Multi-AZ deployment with ELB and ASG

---

A company wants a single DNS endpoint for multiple servers.

Answer:

Elastic Load Balancer

---

## Exam Keywords

High Availability

Scalability

Elasticity

Auto Scaling Group

Multi-AZ

Target Tracking

Scale Up

Scale Out

Scale In

Predictive Scaling

---

## Quick Cheat Sheet

Vertical Scaling = Scale Up

Horizontal Scaling = Scale Out

High Availability = Multi-AZ

Elasticity = Automatic Scaling

Agility = Quickly Provision Resources

ASG = Add/Remove Servers

ELB = Distribute Traffic

Target Tracking = Thermostat

Scheduled Scaling = Known Schedule

Predictive Scaling = Forecast Demand
