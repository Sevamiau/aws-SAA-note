# Amazon EFS - Elastic File System

- Managed NFS (Network File System) — can be mounted on many EC2 instances simultaneously
- Works across multiple AZs in the same region
- Highly available, scalable
- **Linux only** (POSIX/NFS) — not compatible with Windows
- Uses NFSv4.1 protocol
- Access controlled via security groups
- Encryption at rest using KMS
- Scales automatically — pay per GB used (no need to provision size upfront)
- More expensive than EBS gp2 (roughly 3x)

---

## When to use EFS

Use EFS when multiple instances need to share the same files at the same time:
- WordPress or web servers in an ASG all serving the same content
- Shared configuration files across instances
- Content management systems
- Any "shared file system" scenario

If only one instance needs the storage → use EBS (cheaper).

---

## Exam trap

- "Shared file storage across multiple EC2 instances" → EFS
- "Windows EC2 instances need shared storage" → EFS is wrong (Linux only) → use FSx for Windows
- EFS scales automatically — you never provision a size, you pay for what you use
- EFS is more expensive than EBS but you only pay for actual usage, not provisioned capacity
