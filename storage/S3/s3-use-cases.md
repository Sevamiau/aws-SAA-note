# Amazon S3 — Use Cases

## Common Use Cases

- Backup and storage
- Disaster recovery
- Archive (cold storage via S3 Glacier)
- Hybrid cloud storage
- Application hosting
- Media hosting (images, videos)
- Data lakes and big data analytics
- Software delivery
- Static website hosting

## When to Choose S3 on the Exam

| Scenario | Why S3 |
|---|---|
| Store user-uploaded images/videos | Cheap, durable object storage |
| Host a static website | S3 static website hosting feature |
| Store application logs | Scalable, cheap, integrates with Athena for queries |
| Backup RDS/EC2 snapshots | Cross-region replication available |
| Share large files between teams | Pre-signed URLs for temporary access |
| Archive data cheaply | S3 Glacier / Glacier Deep Archive |
| Build a data lake | Store structured/unstructured data at scale, query with Athena or Redshift Spectrum |

## SAA-C03 Exam Tips

- S3 is the default answer for: static website hosting, log storage, backups, and data lake scenarios
- For **temporary access** to private objects, use **pre-signed URLs** (not making the bucket public)
- For **archival at lowest cost**, use **S3 Glacier Deep Archive**
- S3 integrates natively with Lambda, CloudFront, Athena, Glue, and many other AWS services
