## What Problem Does It Solve?

[[S3 Performance]] techniques help applications achieve higher throughput and faster transfers when reading from or writing to S3.

They solve questions such as:

> **"How can I upload very large files faster?"**

> **"How can I increase request throughput?"**

> **"How can users far away from the S3 Region upload data faster?"**

> **"How can I speed up large downloads?"**

The main SAA performance tools are:

- Prefix scaling
- [[S3 Multipart Upload]]
- [[S3 Transfer Acceleration]]
- [[S3 Byte-Range Fetches]]

> [!tip] Memory Trick
> **S3 Performance = Parallelize + Spread + Use the Edge**

---

# Baseline S3 Performance

S3 automatically scales to high request rates.

Typical latency is roughly:

**100–200 ms**

The Maarek slides emphasize that S3 can achieve at least:

**3,500 PUT / COPY / POST / DELETE requests per second per prefix**

and:

**5,500 GET / HEAD requests per second per prefix**

> [!tip] Magic Numbers
> **Writes = 3,500 per prefix**
>
> **Reads = 5,500 per prefix**

---

# What Is an S3 Prefix?

A prefix is part of an object's key path.

Examples:

`bucket/folder1/sub1/file`

Prefix:

`/folder1/sub1/`

Another:

`bucket/folder1/sub2/file`

Prefix:

`/folder1/sub2/`

Another:

`bucket/1/file`

Prefix:

`/1/`

Different prefixes can scale independently.

---

# Prefix Scaling

There is no fixed limit on the number of prefixes you can create in a bucket.

That means throughput can scale by distributing requests across multiple prefixes.

Example:

Prefix 1  
↓  
5,500 GET/HEAD per second

Prefix 2  
↓  
5,500 GET/HEAD per second

Prefix 3  
↓  
5,500 GET/HEAD per second

Prefix 4  
↓  
5,500 GET/HEAD per second

If reads are evenly distributed:

**4 × 5,500 = 22,000 GET/HEAD requests per second**

### Architecture Thinking

More Prefixes  
↓  
Parallel Request Capacity  
↓  
Higher Aggregate Throughput

> [!tip] Memory Trick
> **Each prefix gets its own performance lane**

---

# Prefix Example

Suppose objects are organized as:

`bucket/images1/photo.jpg`

`bucket/images2/photo.jpg`

`bucket/images3/photo.jpg`

If requests are spread across these prefixes, S3 can scale throughput across them.

This is useful for:

- High-volume applications
- Data lakes
- Analytics workloads
- Large-scale object processing

---

# Multipart Upload

[[S3 Multipart Upload]] divides a large file into smaller parts that can be uploaded independently.

Architecture:

Large File  
↓  
Split into Parts  
↓  
├── Part 1 Upload
├── Part 2 Upload
├── Part 3 Upload
└── Part 4 Upload
↓  
S3 Combines Parts  
↓  
Complete Object

---

## Multipart Upload Size Rules

The Maarek slides give two very important thresholds.

### Recommended

For files larger than:

**100 MB**

use Multipart Upload.

### Required

For files larger than:

**5 GB**

Multipart Upload is mandatory.

> [!tip] Memory Trick
> **100 MB = Recommended**
>
> **5 GB = Required**

---

# Why Multipart Upload Is Faster

The biggest performance benefit is:

**Parallelization**

Instead of:

One Giant Upload  
↓  
One Network Stream

you can have:

Part 1  
Part 2  
Part 3  
Part 4  
↓  
Uploading simultaneously

This can significantly improve upload performance.

---

# Multipart Upload Resilience

Multipart Upload also improves reliability.

Suppose:

Part 1 ✅  
Part 2 ✅  
Part 3 ❌  
Part 4 ✅

You do not necessarily need to restart the entire large file.

You can retry:

**The failed part**

This is especially useful for:

- Large files
- Unreliable connections
- Global users
- Backup uploads

---

# Incomplete Multipart Uploads

If an upload starts but is never completed:

Uploaded parts may remain in S3.

Those parts can consume storage.

Use:

[[S3 Lifecycle Rules]]

to automatically remove:

**Incomplete Multipart Uploads**

### Architecture Pattern

Multipart Upload  
↓ interrupted  
Incomplete Parts  
↓  
Lifecycle Rule  
↓  
Cleanup

---

# Transfer Acceleration

[[S3 Transfer Acceleration]] speeds up long-distance transfers between clients and S3.

Instead of sending data directly across the public internet all the way to the bucket's Region:

Client  
↓  
Nearest AWS Edge Location  
↓  
AWS Global Network  
↓  
S3 Bucket

> [!tip] Memory Trick
> **Transfer Acceleration = Enter AWS sooner**

---

# Transfer Acceleration Architecture

Example:

User in Australia  
↓  
Nearby AWS Edge Location  
↓  
AWS Private Backbone  
↓  
S3 Bucket in United States

Instead of:

Australia  
↓  
Public Internet Entire Distance  
↓  
U.S. S3 Bucket

This can improve upload and download performance over long distances.

---

# Why Transfer Acceleration Helps

Transfer Acceleration takes advantage of:

**AWS Edge Locations**

The client transfers the file to a nearby edge location.

AWS then carries the data through its optimized global network toward the S3 bucket.

### Architecture Thinking

Long Geographic Distance  
↓  
Internet Latency  
↓  
Transfer Acceleration  
↓  
Edge Location  
↓  
AWS Backbone

---

# Transfer Acceleration + Multipart Upload

These features are compatible.

This can create a powerful large-file upload architecture:

Large File  
↓  
Split into Parts  
↓  
Parallel Uploads  
↓  
Nearest Edge Location  
↓  
AWS Network  
↓  
S3 Bucket

### Memory Trick

**Multipart = Parallel**

**Acceleration = Edge**

Together:

**Parallel + Edge**

---

# Multipart Upload vs Transfer Acceleration

These improve performance in different ways.

## Multipart Upload

Improves transfer by:

**Parallelizing parts**

Best clue:

**Large File**

---

## Transfer Acceleration

Improves transfer by:

**Using nearby AWS edge locations + AWS global network**

Best clue:

**Long geographic distance**

### Exam Decision

> **Huge file → Multipart Upload**
>
> **Far-away user → Transfer Acceleration**
>
> **Huge file + far-away user → Use both**

---

# S3 Byte-Range Fetches

[[S3 Byte-Range Fetches]] improve download performance by retrieving different portions of an object in parallel.

Instead of downloading:

Entire Object  
↓  
One GET

you request:

Bytes 0–999  
Bytes 1000–1999  
Bytes 2000–2999  
Bytes 3000–3999

in parallel.

Architecture:

Large S3 Object  
↓  
├── Range 1 GET
├── Range 2 GET
├── Range 3 GET
└── Range 4 GET
↓  
Application Combines Data

---

# Why Byte-Range Fetches Help

The Maarek slides highlight two benefits:

1. Faster downloads through parallel GETs
2. Better resilience if one request fails

If one range request fails:

Retry that range

instead of:

Restarting the entire object download

> [!tip] Memory Trick
> **Byte Range = Multipart Upload in reverse**
>
> Multipart:
>
> **Parallel uploads**
>
> Byte Range:
>
> **Parallel downloads**

---

# Download Only Part of an Object

Byte-Range Fetches can also be useful when the application only needs:

**Part of a large object**

Example:

Huge File  
↓  
Need only first portion  
↓  
Request specific byte range

This avoids downloading unnecessary data.

---

# Architecture Thinking

## Scenario 1 — 500 MB Upload

A company uploads 500 MB files to S3.

They want faster uploads.

**Choose → [[S3 Multipart Upload]]**

Why?

Multipart Upload is recommended above:

**100 MB**

---

## Scenario 2 — 10 GB Upload

An application must upload a:

**10 GB object**

**Choose → Multipart Upload**

Why?

For files over:

**5 GB**

Multipart Upload is mandatory.

---

## Scenario 3 — Global Users Upload Large Videos

Users around the world upload large videos into an S3 bucket located in one Region.

Uploads are slow because users are geographically far from the bucket.

**Choose:**

[[S3 Transfer Acceleration]]  
+  
[[S3 Multipart Upload]]

Why?

Multipart:

Parallelizes the large upload.

Transfer Acceleration:

Uses nearby edge locations.

---

## Scenario 4 — Large Download

An analytics application downloads multi-gigabyte S3 objects.

The company wants higher download throughput.

**Choose → [[S3 Byte-Range Fetches]]**

Parallelize multiple range GET requests.

---

## Scenario 5 — Extremely High Read Throughput

An application needs more than 5,500 GET/HEAD requests per second.

Traffic can be distributed across multiple object prefixes.

**Choose → Spread requests across prefixes**

Each prefix can scale independently.

---

## Scenario 6 — One Download Segment Fails

An application downloads a huge S3 object using several byte ranges.

One request fails.

Only the failed range needs to be retried.

This provides:

**Better resilience**

---

# Performance Strategy

A useful way to think about S3 optimization:

## Many Requests

Use:

**Multiple prefixes**

---

## Large Upload

Use:

[[S3 Multipart Upload]]

---

## Long-Distance Transfer

Use:

[[S3 Transfer Acceleration]]

---

## Large Download

Use:

[[S3 Byte-Range Fetches]]

---

## Large Long-Distance Upload

Use:

**Multipart + Transfer Acceleration**

---

# Scenario Recognition

## Immediately Think Prefix Scaling When You See

- Very high request rate
- Thousands of GET requests
- Requests per second
- Multiple prefixes
- High throughput

---

## Immediately Think Multipart Upload When You See

- Large object
- Greater than 100 MB
- Greater than 5 GB
- Parallel upload
- Upload retries
- Speed up large upload

---

## Immediately Think Transfer Acceleration When You See

- Global users
- Far from bucket Region
- Long-distance upload
- Edge location
- AWS global network
- Faster geographic transfers

---

## Immediately Think Byte-Range Fetches When You See

- Large object download
- Parallel GET
- Specific portion of object
- Faster download
- Retry only failed download segment

---

# Exam Traps

## Trap 1 — S3 Supports Only 5,500 GET Requests per Bucket

False.

The performance figure is:

**Per prefix**

Multiple prefixes can scale aggregate throughput.

---

## Trap 2 — Multipart Upload Is Only for Files Above 5 GB

False.

It is:

**Recommended above 100 MB**

and:

**Required above 5 GB**

---

## Trap 3 — Transfer Acceleration Uses CloudFront Caching

Not exactly.

Transfer Acceleration uses:

**AWS Edge Locations + AWS global network**

to accelerate transfers to S3.

Its goal is:

**Transfer performance**

not normal CDN content caching.

---

## Trap 4 — Transfer Acceleration and Multipart Upload Cannot Be Combined

False.

They are:

**Compatible**

and can be used together.

---

## Trap 5 — Byte-Range Fetches Speed Up Uploads

False.

Byte-Range Fetches optimize:

**Downloads / GET requests**

Multipart Upload optimizes:

**Uploads**

---

## Trap 6 — One Failed Multipart Part Requires Full Upload Restart

False.

Individual parts can be retried.

---

## Trap 7 — Prefixes Are Limited to Four

False.

The Maarek slide states:

**There is no limit to the number of prefixes in a bucket.**

Four prefixes are simply used in the example.

---

# Quick Cheat Sheet

| Requirement | Best Technique |
|---|---|
| High GET/HEAD throughput | Multiple Prefixes |
| GET/HEAD baseline | 5,500/sec/prefix |
| PUT/COPY/POST/DELETE baseline | 3,500/sec/prefix |
| Large upload | Multipart Upload |
| Multipart recommended | Over 100 MB |
| Multipart required | Over 5 GB |
| Global long-distance transfer | Transfer Acceleration |
| Uses Edge Locations | Transfer Acceleration |
| Large parallel download | Byte-Range Fetch |
| Retry only part of download | Byte-Range Fetch |
| Large + geographically distant upload | Multipart + Transfer Acceleration |

---

## Master Memory Trick

> [!tip] Master Memory Trick
> **S3 Performance = 3–5–100–5**
>
> **3,500**
>
> → Write requests per second per prefix
>
> **5,500**
>
> → Read requests per second per prefix
>
> **100 MB**
>
> → Multipart recommended
>
> **5 GB**
>
> → Multipart required

Then:

**Many requests → Spread prefixes**

**Huge upload → Multipart**

**Far away → Transfer Acceleration**

**Huge download → Byte Range**

And:

> **Upload = Break into PARTS**
>
> **Download = Break into RANGES**