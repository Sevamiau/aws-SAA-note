# Amazon S3 — Security

## Access Control Types

| Type | Mechanism | Notes |
|---|---|---|
| **User-Based** | IAM Policies | Control which API calls a specific IAM user/role can make |
| **Resource-Based** | Bucket Policies | Bucket-wide rules set from the S3 console; supports cross-account access |
| **Resource-Based** | Object ACL | Fine-grained per-object control (can be disabled) |
| **Resource-Based** | Bucket ACL | Less common; bucket-level ACL (can be disabled) |

## Access Decision Rule

An IAM principal can access an S3 object if:
- The IAM permissions **ALLOW** it, **OR** the resource policy **ALLOWS** it
- **AND** there is no explicit **DENY**

An explicit DENY always wins, regardless of any ALLOW.

## S3 Bucket Policies

Common uses:
- Grant **public access** to all objects in a bucket (e.g. for static websites)
- Force objects to be **encrypted at upload**
- Grant access to **another AWS account** (cross-account)

Bucket policies are JSON documents that specify principals, actions, and resources.

## Encryption

- S3 supports encrypting objects at rest using encryption keys
- Options: SSE-S3 (S3-managed), SSE-KMS (AWS KMS), SSE-C (customer-managed), or client-side encryption

## SAA-C03 Exam Tips

- **Bucket policies** are the standard way to grant cross-account or public access
- If both IAM policy and bucket policy exist, access is granted if **either** allows it (no explicit deny)
- ACLs are legacy — AWS recommends using bucket policies and IAM policies instead
- Block Public Access settings override bucket policies — enable them to prevent accidental public exposure
