## What Problem Does It Solve?

Transfers very large amounts of data when network transfer is too slow or impractical.

Snow Family solves the problem of moving massive datasets using physical devices instead of relying entirely on the internet.

Think:

Huge Dataset

↓

Physical Snow Device

↓

Ship Device

↓

AWS

### Memory Trick

Snow = Move Data Physically

---

## Type

Physical Data Transfer / Edge Computing

---

## What Is AWS Snowball?

Your course describes AWS Snowball as:

Highly secure, portable devices used to:

- Collect data
- Process data at the edge
- Migrate data into AWS
- Migrate data out of AWS

Snowball can help migrate:

Up to Petabytes of Data

### Memory Trick

Snowball = Portable AWS Data Device

---

## When Should You Think Snow?

Think Snow when the question mentions:

- Very large datasets
- Petabytes of data
- Slow network connection
- Limited internet connectivity
- Physical data transfer
- Offline migration

### Exam Recognition

"Internet connection is too slow to migrate a massive dataset"

→ Snow Family

---

## Snow Family Devices

Your existing course summary identifies:

### Snowcone

Small Portable Device

### Snowball

Larger Data Transfers

### Snowmobile

Massive Data Transfers

### Memory Pattern

Snowcone = SMALL

Snowball = LARGE

Snowmobile = MASSIVE

---

## Physical Data Migration

Instead of transferring a massive dataset entirely across the network:

Data Center

↓

Load Data onto Snow Device

↓

Physical Transport

↓

AWS

This is useful when network transfer would take too long.

### Common Use Cases

- Data center migrations
- Large backups
- Large-scale data transfer
- Moving petabytes of data

---

## Edge Computing

Snowball Edge can also perform:

Edge Computing

Edge computing means processing data close to where the data is being created.

Your course examples include:

- Truck on the road
- Ship at sea
- Mining station underground

These locations may have:

Limited Internet

and

Limited Computing Power

### Memory Trick

Edge Computing = Process Data Where It Is Created

---

## Snowball Edge

Your course says Snowball Edge devices can be used to provide computing capabilities at edge locations.

Two versions mentioned are:

- Snowball Edge Compute Optimized
- Snowball Edge Storage Optimized

### Compute Optimized

Think:

More Focus on Computing

### Storage Optimized

Think:

More Focus on Storage

---

## Computing at the Edge

Your course states that Snowball Edge can run:

- EC2 instances
- Lambda functions

at the edge.

Think:

Remote Location

↓

Snowball Edge

↓

EC2 / Lambda

↓

Process Data Locally

### Memory Trick

Snowball Edge = AWS Compute at Remote Locations

---

## Edge Computing Use Cases

Your course gives examples including:

- Preprocessing data
- Machine learning
- Media transcoding

### Scenario

A mining operation has limited internet connectivity and needs to process data locally.

→ Snowball Edge

---

## Snowball Edge Pricing Concepts

Your course identifies several high-level pricing concepts.

You pay for:

- Device usage
- Data transfer OUT of AWS

Your course states:

Data Transfer IN to Amazon S3 = $0.00 per GB

### On-Demand

Includes a one-time service fee per job.

Your course gives examples of included usage periods for Storage Optimized devices.

Shipping days are NOT counted toward those included usage days.

Additional usage days are charged separately.

### Committed Upfront

Your course also mentions:

- Monthly commitments
- 1-year commitments
- 3-year commitments

for edge-computing use cases.

### Exam Memory

Data Transfer IN to S3 = Free

---

## Snow Family vs Transfer Family

These are very different.

### Snow Family

Think:

PHYSICAL Transfer

### Transfer Family

Think:

NETWORK File Transfer

| Snow Family | Transfer Family |
| --- | --- |
| Physical devices | Network transfer |
| Offline migration | Online file transfer |
| Huge datasets | File transfers |
| Petabyte-scale migration | FTP / SFTP |

### Memory Trick

Snow = SHIP IT

Transfer Family = SEND IT OVER NETWORK

---

## Common Use Cases

- Data center migrations
- Large backups
- Petabyte-scale transfers
- Limited network connectivity
- Edge computing
- Remote data processing

---

## Scenario Questions

A company needs to move petabytes of data to AWS, but its internet connection is too slow.

→ Snow Family

---

A company needs a physical device to transfer a massive dataset.

→ Snow Family

---

A remote location has limited internet connectivity and needs to process data locally.

→ Snowball Edge

---

A company needs to run EC2 instances or Lambda functions at an edge location.

→ Snowball Edge

---

A company needs to preprocess data before sending it back to AWS.

→ Snowball Edge

---

A company needs FTP/SFTP-based file transfers over a network.

→ Transfer Family

NOT Snow Family

---

## Don't Confuse These

Snow Family = Physical Data Transfer

Transfer Family = Network File Transfer

Snowcone = Small

Snowball = Large

Snowmobile = Massive

Snowball Edge = Edge Computing

---

## Exam Keywords

Snow Family

Snowball

Snowball Edge

Snowcone

Snowmobile

Physical Device

Offline Transfer

Petabytes

Edge Computing

Limited Internet Connectivity

EC2 at the Edge

Lambda at the Edge

---

## Memory Tricks

Snow = Move Data Physically

Snowcone = SMALL

Snowball = LARGE

Snowmobile = MASSIVE

Snowball Edge = EDGE COMPUTING

Edge Computing = Process Data Where It Is Created

Snow = SHIP IT

Transfer Family = NETWORK

---

## Quick Cheat Sheet

Snow Family = Physical Data Transfer

Snow = Huge Datasets

Snow = Slow / Limited Network

Snowball = Up to Petabytes

Snowball Edge = Edge Computing

Snowball Edge → EC2 + Lambda

Edge Computing = Process Data Where Created

Snowcone = Small

Snowball = Large

Snowmobile = Massive

Snow = SHIP IT

Transfer Family = NETWORK TRANSFER