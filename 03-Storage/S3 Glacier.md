See also: [[S3]]

See also: [[03-Storage/S3 Storage Classes]]

See also: [[S3 Lifecycle Policies]]

See also: [[S3 Glacier Deep Archive]]

## What Problem Does It Solve?

Provides low-cost S3 object storage for archival data and backups.

Glacier storage classes are designed for data that is accessed infrequently but must still be retained.

---

## Type

Archive Storage

---

## What Is S3 Glacier?

S3 Glacier refers to storage classes designed for:

- Archives
- Backups
- Long-term data retention
- Infrequently accessed data

The tradeoff is generally:

Lower storage cost

↓

Less frequent access

↓

Potentially slower retrieval

### Memory Trick

Glacier = Cold Storage

---

## Glacier Storage Classes

Your course covers:

- S3 Glacier Instant Retrieval
- S3 Glacier Flexible Retrieval
- S3 Glacier Deep Archive

Each is designed for a different archival access requirement.

---

## Glacier Instant Retrieval

Designed for archival data that still needs:

Millisecond retrieval

### Best For

Data that is:

- Rarely accessed
- Still needs immediate retrieval when requested

Your course describes it as useful for data accessed approximately:

Once per quarter

### Minimum Storage Duration

90 days

### Memory Trick

Glacier Instant = Archive + Fast Retrieval

---

## Glacier Flexible Retrieval

Formerly known as:

Amazon S3 Glacier

Designed for archival data where retrieval can take longer.

### Retrieval Options

Your course identifies:

#### Expedited

Approximately:

1–5 minutes

#### Standard

Approximately:

3–5 hours

#### Bulk

Approximately:

5–12 hours

### Minimum Storage Duration

90 days

### Memory Trick

Flexible = Choose Retrieval Speed

---

## Glacier Instant vs Flexible

| Glacier Instant | Glacier Flexible |
|---|---|
| Millisecond retrieval | Minutes to hours |
| Immediate archive access | Flexible retrieval speeds |
| Rarely accessed | Cold archival data |
| 90-day minimum | 90-day minimum |

---

## Glacier Deep Archive

Deep Archive is intended for even longer-term archival storage.

Your course describes it as the lowest-cost archival option with much slower retrieval.

See:

[[S3 Glacier Deep Archive]]

---

## Common Use Cases

- Archives
- Backups
- Compliance records
- Long-term retention
- Rarely accessed data

---

## Glacier vs S3 Standard

### S3 Standard

Designed for frequently accessed data.

### Glacier

Designed for archival data.

| S3 Standard | Glacier |
|---|---|
| Frequent access | Rare access |
| Immediate access | Archive-oriented |
| General purpose | Long-term retention |
| Higher storage cost | Lower storage cost |

---

## Glacier vs Deep Archive

### Glacier Flexible Retrieval

Cold storage with multiple retrieval-speed options.

### Glacier Deep Archive

Designed for extremely long-term, rarely accessed data.

| Glacier Flexible | Deep Archive |
|---|---|
| Faster retrieval | Slower retrieval |
| 90-day minimum | 180-day minimum |
| Cold archive | Deep long-term archive |

---

## Lifecycle Connection

S3 Lifecycle configurations can help move older data into Glacier storage classes.

Example:

S3 Standard

↓

Standard-IA

↓

Glacier

↓

Deep Archive

See:

[[S3 Lifecycle Policies]]

---

## Exam Scenarios

Archived data must still be retrieved immediately.

→ Glacier Instant Retrieval

---

Archived data can wait several hours for retrieval.

→ Glacier Flexible Retrieval

---

A company wants different retrieval-speed options for cold archival data.

→ Glacier Flexible Retrieval

---

Data will almost never be accessed and needs the lowest-cost long-term archive.

→ Glacier Deep Archive

---

## Exam Keywords

Archive

Cold storage

Instant Retrieval

Flexible Retrieval

Retrieval time

Long-term retention

Backup

---

## Memory Tricks

Glacier = Cold Storage

Glacier Instant = Archive + Fast

Glacier Flexible = Choose Retrieval Speed

Deep Archive = Put It Away and Forget It