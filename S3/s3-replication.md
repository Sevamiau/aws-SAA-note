# Amazon S3 Replication

S3 supports two types of replication:
- **CRR (Cross-Region Replication)** — replicates objects to a bucket in a different AWS region
- **SRR (Same-Region Replication)** — replicates objects to a bucket in the same AWS region

## Requirements

- Versioning must be enabled on **both** source and destination buckets
- Buckets can belong to different AWS accounts
- Replication is **asynchronous** (not instant)
- Proper IAM permissions must be granted to S3

## Use Cases

| Type | Common Use Cases |
|------|-----------------|
| CRR  | Compliance requirements, lower latency for distant users, replication across accounts |
| SRR  | Log aggregation, keeping production and test accounts in sync |

## Important Notes

**Only new objects are replicated by default.**
- Objects that existed before replication was enabled are NOT replicated automatically.
- To replicate existing objects, use **S3 Batch Replication**.

**DELETE behavior:**
- Delete markers *can* be replicated to the destination (this is an optional setting you must turn on).
- Deletions by version ID are **never** replicated — this is intentional, to protect against malicious or accidental permanent deletes spreading across buckets.

**No chaining of replication:**
- If Bucket 1 replicates to Bucket 2, and Bucket 2 replicates to Bucket 3 — objects written to Bucket 1 will **not** reach Bucket 3.
- Each replication rule only covers a direct source → destination relationship.
