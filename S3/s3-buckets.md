# Amazon S3 — Buckets

- S3 allows storing objects (files) inside **buckets** (containers)
- Buckets are defined at the **region level**
- S3 looks like a global service, but buckets are always created in a specific region

## Namespace

| Scope | Behavior |
|---|---|
| **Global namespace** | Bucket names must be globally unique across all AWS regions and accounts |
| **Regional creation** | Despite the global namespace, each bucket lives in one region |

## Naming Rules

- No uppercase letters, no underscores
- Must start with a lowercase letter or number
- Must not start with the prefix `xn--`
- Must not end with the suffix `-s3alias`
- Must not be formatted as an IP address (e.g. `192.168.1.1`)

## SAA-C03 Exam Tips

- Bucket names are **globally unique** — this is a common distractor in exam scenarios
- Buckets are **regional** — data residency and latency depend on which region you pick
- You cannot rename a bucket; you'd have to create a new one and migrate data
