# AWS SAA-C03 Study Notes

Personal notes for the AWS Solutions Architect Associate exam.

---

## IAM — Identity & Access Management

| File | Topic |
|---|---|
| [Users & Groups](IAM/users-groups.md) | Users, groups, and the least privilege principle |
| [Policies Structure](IAM/IAM-policies-structure.md) | JSON policy format: Version, Statement, Effect, Action |
| [Roles](IAM/iam-roles.md) | IAM Roles for EC2, Lambda, CloudFormation |
| [Password Policy & MFA](IAM/IAM-password-policy.md) | Password requirements, MFA device options |
| [Security Tools](IAM/iam-security-tools.md) | Credentials Report, Access Advisor |
| [Guidelines](IAM/iam-guidelines.md) | Best practices: root account, least privilege |
| [Accessing AWS](IAM/acces-aws.md) | Console vs CLI vs SDK, access keys |
| [AWS CLI](IAM/aws-cli.md) | CLI basics and useful commands |
| [AWS SDK](IAM/aws-sdk.md) | SDK overview and supported languages |
| [Regions & AZs](IAM/aws-notes.md) | How to choose a region, availability zones |
| [IAM Summary](IAM/iam-summary.md) | Quick reference cheat sheet |

---

## EC2 — Elastic Compute Cloud

| File | Topic |
|---|---|
| [EC2 Overview](EC2/EC2.md) | What EC2 is, core capabilities |
| [Sizing & Config](EC2/EC2-sizing-config-options.md) | OS, CPU, RAM, storage, security groups, user data |
| [Instance Types](EC2/EC2-instances-types-overview.md) | General, Compute, Memory, Storage optimized |
| [Purchasing Options](EC2/EC2-instance-purchasing-options/purchasing-options.md) | On-Demand, Reserved, Spot, Dedicated |
| [Spot Instances](EC2/EC2-instance-purchasing-options/EC2-spot-instance-request.md) | Spot request types, interruptions |
| [Spot Fleets](EC2/EC2-instance-purchasing-options/spot-fleets.md) | Fleet strategies |
| [User Data / Bootstrapping](EC2/EC2-user-data-bootstraping.md) | Bootstrap scripts on launch |
| [Placement Groups](EC2/EC2-placement-groups/placement-groups.md) | Cluster, Spread, Partition |
| [Hibernate](EC2/EC2-hibernate.md) | EC2 hibernate — RAM to EBS |
| [AMI Overview](EC2/AMI/AMI-overview.md) | Amazon Machine Images |
| [Private vs Public IP](EC2/private-vs-public-ip.md) | Elastic IPs, private vs public |
| [ENI](EC2/ENI/ENI-1.md) | Elastic Network Interfaces |
| [Scalability & HA](EC2/scalability-high-availability.md) | Vertical vs horizontal scaling, high availability |

### EC2 Storage

| File | Topic |
|---|---|
| [EBS Overview](EC2/EC2-storage-section/EBS/EBS-volume.md) | EBS volumes — what they are |
| [EBS Volume Types](EC2/EC2-storage-section/EBS/EBS-volume-types.md) | gp2/gp3, io1/io2, st1, sc1 |
| [EBS Snapshots](EC2/EC2-storage-section/EBS/EBS-snapshots.md) | Backups, copy across regions |
| [EBS Snapshot Features](EC2/EC2-storage-section/EBS/EBS-snapshots-features.md) | Archive, Recycle Bin, Fast Restore |
| [EBS Encryption](EC2/EC2-storage-section/EBS/EBS-encryption.md) | Encrypt volumes and snapshots |
| [EC2 Instance Store](EC2/EC2-instance-store.md) | High-performance ephemeral storage |
| [Multi-Attach (io1/io2)](EC2/EC2-multi-attach-io1-io2-family.md) | Attach one EBS to multiple EC2s |
| [EFS Overview](EC2/EC2-storage-section/EFS/EFS-elastic-file-system.md) | Elastic File System — shared NFS |
| [EFS Performance & Classes](EC2/EC2-storage-section/EFS/EFS-performance-and-storage-classes.md) | Performance modes, storage tiers |
| [EFS vs EBS](EC2/EC2-storage-section/EFS/EFS-vs-EBS.md) | When to use each |

---

## Security Groups

| File | Topic |
|---|---|
| [Security Groups](security-groups/security-groups.md) | Stateful firewall for EC2 |
| [Intro](security-groups/intro-to-security-groups.md) | Rules: inbound/outbound |
| [Good to Know](security-groups/security-groups-good-to-know.md) | Common gotchas |
| [Classic Ports](security-groups/classic-ports-to-know.md) | SSH 22, HTTP 80, HTTPS 443, RDS 3306, etc. |

---

## Load Balancing

| File | Topic |
|---|---|
| [Load Balancing Overview](load-balancing/load-balancing.md) | Why we use load balancers |
| [Types of Load Balancers](load-balancing/types-of-load-balancers.md) | ALB, NLB, GLB — when to use each |
| [Security Groups & LB](load-balancing/security-groups-load-balancer.md) | How SGs work with ELBs |
| [ELB Overview](load-balancing/ELB/elastic-load-balancer.md) | Elastic Load Balancer basics |
| [ELB Cross-Zone](load-balancing/ELB/ELB-cross-zone.md) | Cross-zone load balancing |
| [ELB Sticky Sessions](load-balancing/ELB/ELB-sticky-sessions.md) | Cookie-based session stickiness |
| [Cookie Names](load-balancing/ELB/ELB-sticky-sessions-coockie-names.md) | AWSALB, AWSALBAPP, AWSALBTG |
| [SSL/TLS Basics](load-balancing/ELB/ELB-ssl-tls-certificate-basics.md) | Certificates on load balancers |
| [SNI](load-balancing/ELB/ELB-ssl-server-name-indication.md) | Server Name Indication — multiple certs on one LB |
| [SSL Resume](load-balancing/ELB/ELB-ssl-certificates-resume.md) | SSL cert summary |
| [Connection Draining](load-balancing/ELB/Conection-draining/ELB-conection-draining.md) | Deregistration delay |
| [ALB Overview](load-balancing/ALB/application-load-balancer.md) | Layer 7, path/host/header routing |
| [ALB Target Groups](load-balancing/ALB/ALB-target-groups.md) | EC2, Lambda, IP targets |
| [ALB Good to Know](load-balancing/ALB/ALB-good-to-know.md) | Fixed hostname, X-Forwarded-For |
| [NLB Overview](load-balancing/NLB/NLB.md) | Layer 4, ultra-low latency, static IP |
| [NLB Target Groups](load-balancing/NLB/NLB-target-groups.md) | EC2, IP, ALB targets |
| [GLB Overview](load-balancing/GLB/GLB.md) | Gateway Load Balancer — 3rd party appliances |
| [GLB Target Groups](load-balancing/GLB/GLB-target-groups.md) | EC2, IP targets |

---

## Auto Scaling Groups (ASG)

| File | Topic |
|---|---|
| [ASG Overview](ASG-auto-scaling-groups/ASG.md) | What ASGs are, min/max/desired |
| [ASG Attributes](ASG-auto-scaling-groups/ASG-attributes.md) | Launch template, capacity, health checks |
| [ASG in AWS](ASG-auto-scaling-groups/ASG-in-AWS.md) | Console walkthrough concepts |
| [ASG with Load Balancers](ASG-auto-scaling-groups/ASG-with-load-balancers.md) | ASG + ELB integration |
| [CloudWatch & Alarms](ASG-auto-scaling-groups/ASG-cloudwatch-and-alarms-scaling.md) | Scaling based on CloudWatch alarms |
| [Scaling Policies](ASG-auto-scaling-groups/ASG-scaling-policies/scaling-policies.md) | Target tracking, step, simple, scheduled |
| [Scaling Cooldowns](ASG-auto-scaling-groups/ASG-scaling-policies/scaling-cooldowns.md) | Cooldown period — prevent thrashing |
| [Metrics to Scale On](ASG-auto-scaling-groups/ASG-scaling-policies/metrics-to-scale-on.md) | CPU, request count, custom metrics |

---

## RDS & Databases

| File | Topic |
|---|---|
| [RDS Overview](RDS/RDS-overview.md) | Managed relational DB service |
| [RDS Backups](RDS/RDS-backups.md) | Automated backups, manual snapshots |
| [Storage Auto Scaling](RDS/RDS-storage-auto-scaling.md) | Auto-grow storage |
| [Read Replicas](RDS/read-replicas/RDS-read-replicas-for-read-scalability.md) | Scale reads, async replication |
| [Read Replica Use Cases](RDS/read-replicas/RDS-use-cases.md) | Reporting, analytics workloads |
| [Network Cost](RDS/read-replicas/RDS-network-cost.md) | Same-region replicas are free |
| [Multi-AZ](RDS/read-replicas/RDS-multi-az.md) | Standby for HA, sync replication |
| [Single to Multi-AZ](RDS/RDS-single-to-multi-az.md) | How to convert without downtime |
| [RDS Custom](RDS/RDS-custom/RDS-custom.md) | Full OS/DB access (Oracle, SQL Server) |
| [Restore Options](RDS/RDS-restore-options.md) | Restore from snapshot, point-in-time |
| [RDS Comparison](RDS/RDS-comparation.md) | RDS vs Aurora vs ElastiCache |
| [Aurora Overview](RDS/amazon-aurora/amazon-aurora.md) | AWS-optimized, 5× faster than MySQL |
| [Aurora DB Cluster](RDS/amazon-aurora/aurora-db-cluster.md) | Writer + reader endpoints |
| [Aurora HA & Read Scaling](RDS/amazon-aurora/aurora-ha-and-rd.md) | 6 copies across 3 AZs |
| [Aurora Replicas](RDS/amazon-aurora/aurora-replicas.md) | Up to 15 read replicas |
| [Aurora Custom Endpoints](RDS/amazon-aurora/aurora-custom-endpopints.md) | Route queries to specific replica sets |
| [Aurora Serverless](RDS/amazon-aurora/aurora-serverless.md) | Auto-scaling, pay per use |
| [Aurora Global](RDS/amazon-aurora/aurora-global.md) | Cross-region, < 1 sec replication lag |
| [Aurora Machine Learning](RDS/amazon-aurora/aurora-machine-learning.md) | SageMaker & Comprehend integration |
| [Aurora Features](RDS/amazon-aurora/aurora-features.md) | Backtrack, cloning, etc. |
| [Aurora Babelfish](RDS/amazon-aurora/aurora-babelfish.md) | SQL Server wire protocol compatibility |
| [RDS Proxy](RDS/aurora-rds-proxy.md) | Connection pooling, reduce DB load |
| [Database Cloning](RDS/aurora-database-clonging.md) | Fast clone from existing cluster |
| [Security](RDS/aurora-rds-aurora-security.md) | IAM auth, encryption, VPC isolation |

---

## ElastiCache

| File | Topic |
|---|---|
| [Overview](Elasticache/elasticache-overview.md) | Managed Redis or Memcached |
| [DB Cache Pattern](Elasticache/elasticache-db-cache.md) | Lazy loading / cache-aside pattern |
| [User Session Store](Elasticache/elasticache-user-session-store.md) | Stateless app session management |
| [Redis vs Memcached](Elasticache/elasticache-redis-vs-nencached.md) | Key differences for the exam |
| [Security](Elasticache/elasticache-cache-security.md) | Redis AUTH, TLS, VPC |
| [Patterns](Elasticache/elasticache-patterns-for-elasticache.md) | Lazy loading vs write-through |
| [Redis Use Cases](Elasticache/elasticache-redis-use-cases.md) | Leaderboards, pub/sub, sorted sets |

---

## Route 53 — DNS

| File | Topic |
|---|---|
| [DNS Basics](what-is-dns.md) | How DNS works, terminology |
| [Route 53 Overview](route-53/route-53.md) | Authoritative DNS + domain registrar |
| [Records](route-53/route-53-records.md) | A, AAAA, CNAME, NS, Hosted Zones |
| [TTL](route-53/route-53-ttl.md) | High vs low TTL trade-offs |
| [Health Checks](route-53/route-53-health-checks.md) | Endpoint, calculated, CloudWatch alarm checks |
| [Ping Checks Comparison](route-53/route-53-ping-checks.md) | ELB vs EC2 status vs Route 53 health checks |
| [Routing Policies](route-53/route-53-policies.md) | Simple, Weighted, Latency, Failover, Geo, Geoproximity, IP-based |
| [Multi-Value Routing](route-53/route-53-multi-value.md) | Client-side load balancing with health checks |
| [3rd Party Registrar](route-53/own-registrar-vs-route53.md) | Use Route 53 DNS with GoDaddy domain |

---

## S3 — Simple Storage Service

| File | Topic |
|---|---|
| [S3 Introduction](S3/s3-intro.md) | Overview, key concepts, durability |
| [Buckets](S3/s3-buckets.md) | Bucket naming, regions, global namespace |
| [Objects](S3/s3-objects.md) | Keys, size limits, metadata, versioning |
| [Security](S3/s3-security.md) | IAM policies, bucket policies, ACLs, encryption |
| [Use Cases](S3/s3-use-cases.md) | When S3 is the right answer |

---

## SSH & Connectivity

| File | Topic |
|---|---|
| [SSH Summary Table](SSH/SSH-sumary-table.md) | SSH vs EC2 Instance Connect vs SSM |
