# Amazon S3 — Storage Classes

- S3 offers multiple storage classes optimized for different access patterns and cost requirements
- Objects can be moved between classes manually or automatically via **S3 Lifecycle Configurations**

## Classes Overview

| Storage Class | Availability | Key Trait |
|---|---|---|
| **S3 Standard** | 99.99% | Frequently accessed data, low latency, high throughput |
| **S3 Standard-IA** | 99.9% | Infrequently accessed, rapid access when needed, lower cost than Standard |
| **S3 One Zone-IA** | 99.5% | Single AZ only — data is lost if the AZ is destroyed |
| **S3 Glacier Instant Retrieval** | 99.9% | Archive with millisecond retrieval; min. 90-day storage duration |
| **S3 Glacier Flexible Retrieval** | 99.99% | Archive with flexible retrieval tiers (minutes to hours) |
| **S3 Glacier Deep Archive** | 99.99% | Lowest cost; for long-term storage with retrieval in hours |
| **S3 Intelligent-Tiering** | 99.9% | Auto-moves objects between tiers based on usage; no retrieval charges |

## Class Details

**S3 Standard — General Purpose**
- Used for frequently accessed data
- Sustains 2 concurrent facility failures
- Use cases: Big Data analytics, mobile and gaming apps, content distribution

**S3 Standard-IA (Infrequent Access)**
- Lower cost than S3 Standard, but a per-retrieval fee applies
- Use cases: disaster recovery, backups that need fast access when required

**S3 One Zone-IA**
- High durability (99.999999999%) within a single AZ
- Data is permanently lost if that AZ is destroyed
- Use cases: secondary backups of on-premise data, or data that can be recreated

**S3 Glacier Instant Retrieval**
- Low-cost archiving with millisecond retrieval
- Minimum storage duration: 90 days
- Use cases: data accessed roughly once a quarter

**S3 Glacier Flexible Retrieval**
- Retrieval tiers: Expedited (1–5 min), Standard (3–5 hrs), Bulk (5–12 hrs — free)
- Minimum storage duration: 90 days

**S3 Glacier Deep Archive**
- Lowest storage cost in S3
- Retrieval tiers: Standard (12 hrs), Bulk (48 hrs)
- Minimum storage duration: 180 days
- Use cases: compliance archives, data that is almost never accessed

**S3 Intelligent-Tiering**
- Small monthly monitoring and auto-tiering fee
- Automatically moves objects between access tiers based on usage patterns
- No retrieval charges

## SAA-C03 Exam Tips

- **S3 Standard-IA and One Zone-IA** both charge a retrieval fee — factor this in for frequently accessed workloads
- **One Zone-IA** is not suitable for primary backups — data is gone if the AZ fails
- **Glacier** classes have **minimum storage durations** — deleting early still incurs charges for the full minimum period
- **Intelligent-Tiering** is the right answer when access patterns are unknown or unpredictable
- Use **Lifecycle Policies** to automatically transition objects to cheaper classes as they age
