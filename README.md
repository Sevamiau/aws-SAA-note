# AWS SAA-C03 Study Notes

Personal notes for the AWS Solutions Architect Associate exam.

**[STUDY-GUIDE.md](STUDY-GUIDE.md)** — complete, readable book compiled from all notes below. Start here for review.

---

## Security & Identity

### IAM — Identity & Access Management

| File | Topic |
|---|---|
| [Users & Groups](security-and-identity/IAM/users-groups.md) | Users, groups, and the least privilege principle |
| [Policies Structure](security-and-identity/IAM/IAM-policies-structure.md) | JSON policy format: Version, Statement, Effect, Action |
| [Roles](security-and-identity/IAM/iam-roles.md) | IAM Roles for EC2, Lambda, CloudFormation |
| [Password Policy & MFA](security-and-identity/IAM/IAM-password-policy.md) | Password requirements, MFA device options |
| [Security Tools](security-and-identity/IAM/iam-security-tools.md) | Credentials Report, Access Advisor |
| [Guidelines](security-and-identity/IAM/iam-guidelines.md) | Best practices: root account, least privilege |
| [Accessing AWS](security-and-identity/IAM/acces-aws.md) | Console vs CLI vs SDK, access keys |
| [AWS CLI](security-and-identity/IAM/aws-cli.md) | CLI basics and useful commands |
| [AWS SDK](security-and-identity/IAM/aws-sdk.md) | SDK overview and supported languages |
| [Regions & AZs](security-and-identity/IAM/aws-notes.md) | How to choose a region, availability zones |
| [IAM Summary](security-and-identity/IAM/iam-summary.md) | Quick reference cheat sheet |

### Security Groups

| File | Topic |
|---|---|
| [Security Groups](security-and-identity/security-groups/security-groups.md) | Stateful firewall for EC2 |
| [Intro](security-and-identity/security-groups/intro-to-security-groups.md) | Rules: inbound/outbound |
| [Good to Know](security-and-identity/security-groups/security-groups-good-to-know.md) | Common gotchas |
| [Classic Ports](security-and-identity/security-groups/classic-ports-to-know.md) | SSH 22, HTTP 80, HTTPS 443, RDS 3306, etc. |

---

## Compute

### EC2 — Elastic Compute Cloud

| File | Topic |
|---|---|
| [EC2 Overview](compute/EC2/EC2.md) | What EC2 is, core capabilities |
| [Sizing & Config](compute/EC2/EC2-sizing-config-options.md) | OS, CPU, RAM, storage, security groups, user data |
| [Instance Types](compute/EC2/EC2-instances-types-overview.md) | General, Compute, Memory, Storage optimized |
| [Purchasing Options](compute/EC2/EC2-instance-purchasing-options/purchasing-options.md) | On-Demand, Reserved, Spot, Dedicated |
| [Spot Instances](compute/EC2/EC2-instance-purchasing-options/EC2-spot-instance-request.md) | Spot request types, interruptions |
| [Spot Fleets](compute/EC2/EC2-instance-purchasing-options/spot-fleets.md) | Fleet strategies |
| [User Data / Bootstrapping](compute/EC2/EC2-user-data-bootstraping.md) | Bootstrap scripts on launch |
| [Placement Groups](compute/EC2/EC2-placement-groups/placement-groups.md) | Cluster, Spread, Partition |
| [Hibernate](compute/EC2/EC2-hibernate.md) | EC2 hibernate — RAM to EBS |
| [AMI Overview](compute/EC2/AMI/AMI-overview.md) | Amazon Machine Images |
| [Private vs Public IP](compute/EC2/private-vs-public-ip.md) | Elastic IPs, private vs public |
| [ENI](compute/EC2/ENI/ENI-1.md) | Elastic Network Interfaces |
| [Instance Metadata (IMDS)](compute/EC2/EC2-instance-metadata.md) | 169.254.169.254, IMDSv1 vs IMDSv2, SSRF protection |
| [Scalability & HA](compute/EC2/scalability-high-availability.md) | Vertical vs horizontal scaling, high availability |
| [SSH Access](compute/SSH/SSH-sumary-table.md) | SSH vs EC2 Instance Connect vs SSM |

### Auto Scaling Groups (ASG)

| File | Topic |
|---|---|
| [ASG Overview](compute/ASG-auto-scaling-groups/ASG.md) | What ASGs are, min/max/desired |
| [ASG Attributes](compute/ASG-auto-scaling-groups/ASG-attributes.md) | Launch template, capacity, health checks |
| [ASG in AWS](compute/ASG-auto-scaling-groups/ASG-in-AWS.md) | Console walkthrough concepts |
| [ASG with Load Balancers](compute/ASG-auto-scaling-groups/ASG-with-load-balancers.md) | ASG + ELB integration |
| [CloudWatch & Alarms](compute/ASG-auto-scaling-groups/ASG-cloudwatch-and-alarms-scaling.md) | Scaling based on CloudWatch alarms |
| [Scaling Policies](compute/ASG-auto-scaling-groups/ASG-scaling-policies/scaling-policies.md) | Target tracking, step, simple, scheduled |
| [Scaling Cooldowns](compute/ASG-auto-scaling-groups/ASG-scaling-policies/scaling-cooldowns.md) | Cooldown period — prevent thrashing |
| [Metrics to Scale On](compute/ASG-auto-scaling-groups/ASG-scaling-policies/metrics-to-scale-on.md) | CPU, request count, custom metrics |

### Load Balancing

| File | Topic |
|---|---|
| [Load Balancing Overview](compute/load-balancing/load-balancing.md) | Why we use load balancers |
| [Types of Load Balancers](compute/load-balancing/types-of-load-balancers.md) | ALB, NLB, GLB — when to use each |
| [Security Groups & LB](compute/load-balancing/security-groups-load-balancer.md) | How SGs work with ELBs |
| [ELB Overview](compute/load-balancing/ELB/elastic-load-balancer.md) | Elastic Load Balancer basics |
| [ELB Cross-Zone](compute/load-balancing/ELB/ELB-cross-zone.md) | Cross-zone load balancing |
| [ELB Sticky Sessions](compute/load-balancing/ELB/ELB-sticky-sessions.md) | Cookie-based session stickiness |
| [Cookie Names](compute/load-balancing/ELB/ELB-sticky-sessions-coockie-names.md) | AWSALB, AWSALBAPP, AWSALBTG |
| [SSL/TLS Basics](compute/load-balancing/ELB/ELB-ssl-tls-certificate-basics.md) | Certificates on load balancers |
| [SNI](compute/load-balancing/ELB/ELB-ssl-server-name-indication.md) | Server Name Indication — multiple certs on one LB |
| [SSL Resume](compute/load-balancing/ELB/ELB-ssl-certificates-resume.md) | SSL cert summary |
| [Connection Draining](compute/load-balancing/ELB/Conection-draining/ELB-conection-draining.md) | Deregistration delay |
| [ALB Overview](compute/load-balancing/ALB/application-load-balancer.md) | Layer 7, path/host/header routing |
| [ALB Target Groups](compute/load-balancing/ALB/ALB-target-groups.md) | EC2, Lambda, IP targets |
| [ALB Good to Know](compute/load-balancing/ALB/ALB-good-to-know.md) | Fixed hostname, X-Forwarded-For |
| [NLB Overview](compute/load-balancing/NLB/NLB.md) | Layer 4, ultra-low latency, static IP |
| [NLB Target Groups](compute/load-balancing/NLB/NLB-target-groups.md) | EC2, IP, ALB targets |
| [GLB Overview](compute/load-balancing/GLB/GLB.md) | Gateway Load Balancer — 3rd party appliances |
| [GLB Target Groups](compute/load-balancing/GLB/GLB-target-groups.md) | EC2, IP targets |

---

## Storage

### S3 — Simple Storage Service

| File | Topic |
|---|---|
| [S3 Introduction](storage/S3/s3-intro.md) | Overview, key concepts, durability |
| [Buckets](storage/S3/s3-buckets.md) | Bucket naming, regions, global namespace |
| [Objects](storage/S3/s3-objects.md) | Keys, size limits, metadata, versioning |
| [Versioning](storage/S3/s3-versioning.md) | Bucket-level versioning, version IDs, delete markers |
| [Security](storage/S3/s3-security.md) | IAM policies, bucket policies, ACLs, encryption |
| [Replication](storage/S3/s3-replication.md) | CRR (cross-region) and SRR (same-region) replication |
| [Storage Classes](storage/S3/s3-storage-class.md) | Standard, IA, Glacier, Intelligent-Tiering, Lifecycle |
| [Express One Zone Class](storage/S3/s3-express-one-zone-class.md) | High-performance single-AZ class, Directory Buckets |
| [Use Cases](storage/S3/s3-use-cases.md) | When S3 is the right answer |

#### S3 Advanced

| File | Topic |
|---|---|
| [Moving Between Storage Classes](storage/S3/S3-advanced/s3-moving-between-storage-classes.md) | Transition rules, when to use Standard IA vs Glacier |
| [Lifecycle Rules](storage/S3/S3-advanced/s3-lifecycle-rules.md) | Transition and expiration actions, prefix/tag filters |
| [S3 Analytics](storage/S3/S3-advanced/s3-analytics.md) | Storage class analysis, when to transition objects |
| [Requester Pays](storage/S3/S3-advanced/s3-requester-pays.md) | Shift data transfer costs to the requester |
| [Event Notifications](storage/S3/S3-advanced/s3-event-notifications.md) | Trigger Lambda/SQS/SNS on object events |
| [Event Notifications + EventBridge](storage/S3/S3-advanced/s3-event-notifications-eventbridge.md) | Route S3 events through EventBridge |
| [Baseline Performance](storage/S3/S3-advanced/s3-baseline-performance.md) | 3,500 PUT/5,500 GET per prefix per second |
| [Batch Operations](storage/S3/S3-advanced/s3-batch-operations.md) | Bulk actions on existing objects |
| [Storage Lens](storage/S3/S3-advanced/s3-storage-lens.md) | Organization-wide storage analytics |

#### S3 Security

| File | Topic |
|---|---|
| [Encryption](storage/S3/s3-security/s3-encryption.md) | SSE-S3, SSE-KMS, SSE-C, client-side |
| [DSSE-KMS](storage/S3/s3-security/s3-dsse-kms.md) | Dual-layer server-side encryption |
| [Default Encryption vs Bucket Policies](storage/S3/s3-security/s3-default-encryption-vs-bucket-policies.md) | Enforcement order |
| [CORS](storage/S3/s3-security/s3-cors.md) | Cross-origin resource sharing |
| [MFA Delete](storage/S3/s3-security/s3-mfa-delete.md) | Require MFA to delete versions |
| [Access Logs](storage/S3/s3-security/s3-access-logs.md) | Log all requests to another bucket |
| [Pre-Signed URLs](storage/S3/s3-security/s3-pre-signed-urls.md) | Temporary, signed access to private objects |
| [Glacier Vault Lock](storage/S3/s3-security/s3-glacier-vault-lock.md) | WORM policy for compliance |
| [Access Points](storage/S3/s3-security/s3-access-points.md) | Named endpoints with their own policies |

### EC2 Storage (EBS & EFS)

| File | Topic |
|---|---|
| [EBS Overview](compute/EC2/EC2-storage-section/EBS/EBS-volume.md) | EBS volumes — what they are |
| [EBS Volume Types](compute/EC2/EC2-storage-section/EBS/EBS-volume-types.md) | gp2/gp3, io1/io2, st1, sc1 |
| [EBS Snapshots](compute/EC2/EC2-storage-section/EBS/EBS-snapshots.md) | Backups, copy across regions |
| [EBS Snapshot Features](compute/EC2/EC2-storage-section/EBS/EBS-snapshots-features.md) | Archive, Recycle Bin, Fast Restore |
| [EBS Encryption](compute/EC2/EC2-storage-section/EBS/EBS-encryption.md) | Encrypt volumes and snapshots |
| [EC2 Instance Store](compute/EC2/EC2-instance-store.md) | High-performance ephemeral storage |
| [Multi-Attach (io1/io2)](compute/EC2/EC2-multi-attach-io1-io2-family.md) | Attach one EBS to multiple EC2s |
| [EFS Overview](compute/EC2/EC2-storage-section/EFS/EFS-elastic-file-system.md) | Elastic File System — shared NFS |
| [EFS Performance & Classes](compute/EC2/EC2-storage-section/EFS/EFS-performance-and-storage-classes.md) | Performance modes, storage tiers |
| [EFS vs EBS](compute/EC2/EC2-storage-section/EFS/EFS-vs-EBS.md) | When to use each |

### Storage Extras

| File | Topic |
|---|---|
| [Storage Comparison](storage/storage-comparasion.md) | EBS vs EFS vs S3 vs FSx — when to use what |
| [Amazon FSx](storage/storage-extras/amazon-fsx.md) | Managed file systems: Windows, Lustre, NetApp, OpenZFS |
| [FSx Principal Differences](storage/storage-extras/amazon-fsx-principal-diff.md) | Key exam distinctions between FSx types |
| [Snowball Overview](storage/storage-extras/snowball-overview.md) | Physical data transfer: Snowball Edge, Snowmobile |
| [Hybrid Cloud Storage](storage/storage-extras/hybrid-cloud-storage.md) | Storage Gateway: S3, FSx, Volume, Tape |
| [Transfer Family](storage/storage-extras/transfer-family.md) | SFTP/FTP/FTPS managed file transfer into S3/EFS |
| [DataSync](storage/storage-extras/datasync.md) | Online data migration from on-prem or other clouds |

---

## Databases

### RDS & Aurora

| File | Topic |
|---|---|
| [RDS Overview](databases/RDS/RDS-overview.md) | Managed relational DB service |
| [RDS Backups](databases/RDS/RDS-backups.md) | Automated backups, manual snapshots |
| [Storage Auto Scaling](databases/RDS/RDS-storage-auto-scaling.md) | Auto-grow storage |
| [Read Replicas](databases/RDS/read-replicas/RDS-read-replicas-for-read-scalability.md) | Scale reads, async replication |
| [Read Replica Use Cases](databases/RDS/read-replicas/RDS-use-cases.md) | Reporting, analytics workloads |
| [Network Cost](databases/RDS/read-replicas/RDS-network-cost.md) | Same-region replicas are free |
| [Multi-AZ](databases/RDS/read-replicas/RDS-multi-az.md) | Standby for HA, sync replication |
| [Single to Multi-AZ](databases/RDS/RDS-single-to-multi-az.md) | How to convert without downtime |
| [RDS Custom](databases/RDS/RDS-custom/RDS-custom.md) | Full OS/DB access (Oracle, SQL Server) |
| [Restore Options](databases/RDS/RDS-restore-options.md) | Restore from snapshot, point-in-time |
| [RDS Comparison](databases/RDS/RDS-comparation.md) | RDS vs Aurora vs ElastiCache |
| [Aurora Overview](databases/RDS/amazon-aurora/amazon-aurora.md) | AWS-optimized, 5× faster than MySQL |
| [Aurora DB Cluster](databases/RDS/amazon-aurora/aurora-db-cluster.md) | Writer + reader endpoints |
| [Aurora HA & Read Scaling](databases/RDS/amazon-aurora/aurora-ha-and-rd.md) | 6 copies across 3 AZs |
| [Aurora Replicas](databases/RDS/amazon-aurora/aurora-replicas.md) | Up to 15 read replicas |
| [Aurora Custom Endpoints](databases/RDS/amazon-aurora/aurora-custom-endpopints.md) | Route queries to specific replica sets |
| [Aurora Serverless](databases/RDS/amazon-aurora/aurora-serverless.md) | Auto-scaling, pay per use |
| [Aurora Global](databases/RDS/amazon-aurora/aurora-global.md) | Cross-region, < 1 sec replication lag |
| [Aurora Machine Learning](databases/RDS/amazon-aurora/aurora-machine-learning.md) | SageMaker & Comprehend integration |
| [Aurora Features](databases/RDS/amazon-aurora/aurora-features.md) | Backtrack, cloning, etc. |
| [Aurora Babelfish](databases/RDS/amazon-aurora/aurora-babelfish.md) | SQL Server wire protocol compatibility |
| [RDS Proxy](databases/RDS/aurora-rds-proxy.md) | Connection pooling, reduce DB load |
| [Database Cloning](databases/RDS/aurora-database-clonging.md) | Fast clone from existing cluster |
| [Security](databases/RDS/aurora-rds-aurora-security.md) | IAM auth, encryption, VPC isolation |

### ElastiCache

| File | Topic |
|---|---|
| [Overview](databases/Elasticache/elasticache-overview.md) | Managed Redis or Memcached |
| [DB Cache Pattern](databases/Elasticache/elasticache-db-cache.md) | Lazy loading / cache-aside pattern |
| [User Session Store](databases/Elasticache/elasticache-user-session-store.md) | Stateless app session management |
| [Redis vs Memcached](databases/Elasticache/elasticache-redis-vs-memcached.md) | Key differences for the exam |
| [Security](databases/Elasticache/elasticache-cache-security.md) | Redis AUTH, TLS, VPC |
| [Patterns](databases/Elasticache/elasticache-patterns-for-elasticache.md) | Lazy loading vs write-through |
| [Redis Use Cases](databases/Elasticache/elasticache-redis-use-cases.md) | Leaderboards, pub/sub, sorted sets |

---

## Networking & Content Delivery

### Route 53 — DNS

| File | Topic |
|---|---|
| [DNS Basics](networking/what-is-dns.md) | How DNS works, terminology |
| [Route 53 Overview](networking/route-53/route-53.md) | Authoritative DNS + domain registrar |
| [Records](networking/route-53/route-53-records.md) | A, AAAA, CNAME, NS, **Alias records**, Hosted Zones |
| [TTL](networking/route-53/route-53-ttl.md) | High vs low TTL trade-offs |
| [Health Checks](networking/route-53/route-53-health-checks.md) | Endpoint, calculated, CloudWatch alarm checks |
| [Ping Checks Comparison](networking/route-53/route-53-ping-checks.md) | ELB vs EC2 status vs Route 53 health checks |
| [Routing Policies](networking/route-53/route-53-policies.md) | Simple, Weighted, Latency, Failover, Geo, Geoproximity, IP-based |
| [Multi-Value Routing](networking/route-53/route-53-multi-value.md) | Client-side load balancing with health checks |
| [3rd Party Registrar](networking/route-53/own-registrar-vs-route53.md) | Use Route 53 DNS with GoDaddy domain |

### CloudFront & Global Accelerator

| File | Topic |
|---|---|
| [CloudFront Overview](networking/cloudfront/cloudfront-overview.md) | CDN, edge locations, origins, behaviors |
| [CloudFront with ALB/EC2 via VPC](networking/cloudfront/cloudfront-alb-ec2-as-an-origin-using-vpc.md) | Private origins using VPC |
| [Cache Invalidations](networking/cloudfront/cloudfront-cache-invalidations.md) | Force cache refresh by path |
| [Geo Restriction](networking/cloudfront/cloudfront-geo-restriction.md) | Allow/block by country |
| [CloudFront vs Global Accelerator](networking/cloudfront/cloudfront-vs-global-accelerator.md) | CDN caching vs network-layer acceleration |
| [Global Accelerator](networking/cloudfront/Global-Accelerator/global-accelerator.md) | Anycast IPs, AWS backbone routing |

---

## Application Integration

### SQS, SNS & Messaging

| File | Topic |
|---|---|
| [Intro to Messaging](application-integration/introduction-to-messaging/SQS/intro-to-messagin.md) | Why decouple with queues and topics |
| [SQS Standard Queue](application-integration/introduction-to-messaging/SQS/sqs-standard-queue.md) | At-least-once, unlimited throughput |
| [SQS Producing Messages](application-integration/introduction-to-messaging/SQS/sqs-producing-messages.md) | SendMessage API |
| [SQS Consuming Messages](application-integration/introduction-to-messaging/SQS/sqs-consuming-messages.md) | Polling, delete-after-process |
| [SQS Visibility Timeout](application-integration/introduction-to-messaging/SQS/sqs-invisibility-timeout.md) | Hide message during processing |
| [SQS Long Polling](application-integration/introduction-to-messaging/SQS/sqs-long-polling.md) | Reduce empty receive calls |
| [SQS FIFO Queue](application-integration/introduction-to-messaging/SQS/sqs-fifo-queue.md) | Ordered, exactly-once delivery |
| [SQS with ASG](application-integration/introduction-to-messaging/SQS/sqs-with-asg.md) | Scale EC2s from queue depth |
| [SNS Overview](application-integration/introduction-to-messaging/SNS/sns-overviw.md) | Pub/Sub, topics, subscriptions |
| [SNS + SQS Fan-Out](application-integration/introduction-to-messaging/sns-and-sqs-fanout.md) | One SNS → many SQS queues |
| [SNS → S3 via Kinesis Firehose](application-integration/introduction-to-messaging/sns-to-s3-trough-kdf.md) | SNS to S3 using KDF as subscriber |
| [SQS vs SNS vs Kinesis](application-integration/introduction-to-messaging/sqs-vs-sns-vs-kinesis.md) | When to use which |
| [Amazon MQ](application-integration/introduction-to-messaging/amazon-mq.md) | Managed ActiveMQ/RabbitMQ for migration |

### Kinesis

| File | Topic |
|---|---|
| [Kinesis Overview](application-integration/introduction-to-messaging/kinesis/kinesis-overview.md) | Data Streams — real-time ingestion |
| [Kinesis Data Firehose](application-integration/introduction-to-messaging/kinesis/kinesis-data-firehose.md) | Managed delivery to S3, Redshift, OpenSearch |
