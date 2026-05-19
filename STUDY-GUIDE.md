# AWS SAA-C03 Study Guide

A complete, readable study guide compiled from personal notes.  
Topics covered: IAM, EC2, Storage, Security Groups, Load Balancing, ASG, RDS, Aurora, ElastiCache, Route 53, S3.

---

## Table of Contents

1. [IAM — Identity and Access Management](#1-iam--identity-and-access-management)
2. [EC2 — Elastic Compute Cloud](#2-ec2--elastic-compute-cloud)
3. [EC2 Storage — EBS, EFS, Instance Store](#3-ec2-storage)
4. [Security Groups](#4-security-groups)
5. [Load Balancing](#5-load-balancing)
6. [Auto Scaling Groups](#6-auto-scaling-groups)
7. [RDS and Aurora](#7-rds-and-aurora)
8. [ElastiCache](#8-elasticache)
9. [Route 53](#9-route-53)
10. [S3 — Simple Storage Service](#10-s3--simple-storage-service)

---

# 1. IAM — Identity and Access Management

## What it is

IAM is the service that controls who can do what in your AWS account. It is a **global service** — there are no regions for IAM, it applies to the whole account.

Every time someone or something tries to perform an action in AWS (a user clicking in the console, a script calling the API, an EC2 instance calling S3), IAM is the system that decides whether to allow or deny that action.

## Core concepts

**Root account**: created automatically when you open an AWS account. Has unrestricted access to everything. You should only use it once to set up your account, then never again. Do not share it.

**Users**: represent a person or a system. They have credentials (a password for the console, access keys for the CLI/SDK). A user that has no permissions can do nothing.

**Groups**: collections of users. You attach permissions to the group, and every user in the group inherits them. Groups cannot contain other groups.

**Policies**: JSON documents that define permissions. They say: for this action, on this resource, allow or deny. You attach policies to users, groups, or roles.

**Roles**: like a user, but for AWS services. When an EC2 instance needs to read from S3, you don't give it a username and password — you attach a Role to it. The instance assumes that role and gets temporary credentials automatically.

## How permissions are evaluated

An IAM principal (user, role) can access a resource if:
- An IAM policy **allows** it, OR the resource policy **allows** it
- AND there is no explicit **deny**

Explicit deny always wins. If a policy says deny, nothing else can override it.

## Policy structure

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "AllowS3Read",
      "Effect": "Allow",
      "Action": ["s3:GetObject"],
      "Resource": ["arn:aws:s3:::my-bucket/*"]
    }
  ]
}
```

Key fields:
- `Version`: always `"2012-10-17"`
- `Effect`: `Allow` or `Deny`
- `Action`: what operation (e.g. `s3:GetObject`, `ec2:DescribeInstances`, `*` for everything)
- `Resource`: which specific resource the action applies to
- `Principal`: who the policy applies to (used in resource-based policies)
- `Condition`: optional restrictions (e.g. only allow from a specific IP)

## How to access AWS

| Method | Protected by | Use for |
|---|---|---|
| AWS Console | Password + MFA | Manual, interactive work |
| AWS CLI | Access Keys | Scripts, automation |
| AWS SDK | Access Keys | Code inside applications |

Access keys are like a username (Access Key ID) and password (Secret Access Key). Never share them. Never commit them to code.

## IAM Roles for services

Common pattern: an EC2 instance needs to call other AWS services (read from S3, write to DynamoDB). Instead of hardcoding credentials, you attach an IAM Role to the instance. AWS automatically provides temporary credentials that rotate.

Common roles:
- EC2 Instance Role
- Lambda Execution Role
- CloudFormation Role

## Security tools

**IAM Credentials Report** (account-level): lists all users and the status of their credentials — whether they have passwords, access keys, MFA enabled, and when they last used them. Use this to audit your account.

**IAM Access Advisor** (user-level): shows what services a user has been granted permissions for, and when they last accessed each one. Use this to trim permissions down to what is actually used (least privilege).

## MFA

MFA requires two things: something you know (password) and something you own (a device). If a password is stolen, the account is still protected because the attacker doesn't have the device.

Options:
- Virtual MFA app (Google Authenticator, Authy) — multiple tokens on a phone
- U2F hardware key (YubiKey) — physical USB key
- Hardware key fob — physical device from Gemalto

## Best practices

- Never use the root account after initial setup
- One physical person = one AWS user (never share accounts)
- Assign users to groups, assign permissions to groups
- Enforce MFA on all users, especially root
- Use roles for services instead of hardcoded credentials
- Apply least privilege — only grant what is actually needed
- Audit regularly with Credentials Report and Access Advisor

## AWS Regions and Availability Zones

**Regions**: separate geographic areas (us-east-1, eu-west-1, etc.). Most AWS services are region-scoped. Choosing a region involves:
1. Compliance — data may be required to stay within a country
2. Proximity — closer to your users means lower latency
3. Service availability — newer services launch in some regions first
4. Pricing — varies by region

**Availability Zones (AZs)**: each region has 3 to 6 AZs (e.g. us-east-1a, us-east-1b, us-east-1c). Each AZ is one or more physical data centers with independent power, cooling, and networking. They are close enough to have low-latency connections between them, but far enough to be isolated from each other's failures.

Designing across multiple AZs is the foundation of high availability in AWS.

---

# 2. EC2 — Elastic Compute Cloud

## What it is

EC2 is virtual servers in the cloud. EC2 = Elastic Compute Cloud, and it is one of the most important AWS services — nearly every architecture involves it.

The four core capabilities of EC2:
1. Rent virtual machines (EC2 instances)
2. Store data on virtual drives (EBS)
3. Distribute load across machines (ELB)
4. Scale automatically (ASG)

## Instance configuration

When you launch an instance you choose:
- Operating system (Linux, Windows, macOS)
- CPU and RAM
- Storage (network-attached via EBS/EFS, or physical via Instance Store)
- Network card and public IP settings
- Firewall rules (Security Group)
- Bootstrap script (User Data)

## User Data

A shell script you provide when launching an instance. Runs **once**, at first boot, as root. Use it to install software, apply updates, download files, configure the system — anything you'd do manually after launch. Automating this is what makes infrastructure repeatable.

```bash
#!/bin/bash
yum update -y
yum install -y httpd
systemctl start httpd
systemctl enable httpd
```

## Instance types

AWS naming convention: `m5.2xlarge`
- `m` = instance family
- `5` = generation
- `2xlarge` = size within the family

| Family | Optimized for | Pick when |
|---|---|---|
| General Purpose (t, m) | Balance of CPU/RAM/network | Web servers, code repos, small DBs |
| Compute Optimized (c) | High CPU performance | Batch processing, HPC, gaming servers, ML inference |
| Memory Optimized (r, x) | Large amounts of RAM | In-memory databases, big data processing, real-time analytics |
| Storage Optimized (i, d) | High sequential read/write on local storage | OLTP, NoSQL, data warehousing, distributed file systems |

## Purchasing options

| Option | Commitment | Discount | Use when |
|---|---|---|---|
| On-Demand | None | None | Short-term, unpredictable workload |
| Reserved | 1 or 3 years | Up to 72% | Steady-state app that runs 24/7 (e.g. a database) |
| Savings Plans | 1 or 3 years | Up to 72% | Same discount as Reserved but flexible across instance size and OS |
| Spot | None | Up to 90% | Fault-tolerant jobs that can be interrupted |
| Dedicated Host | 1/3 years or on-demand | - | BYOL licenses, compliance requiring full server control |
| Dedicated Instance | None | - | Hardware isolation without needing full host control |
| Capacity Reservation | None | None | Guaranteed capacity in a specific AZ for a short critical window |

**Reserved vs Savings Plans**: Reserved locks you to a specific instance type and region. Savings Plans commit to a dollar-per-hour spend and let you change instance type, OS, and size freely within a family.

**Dedicated Host vs Dedicated Instance**: a Dedicated Host gives you visibility into the physical server (sockets, cores) — required for BYOL licenses. A Dedicated Instance just guarantees no other AWS customer shares your hardware.

**Exam trap**: "minimize cost for a steady-state workload" → Reserved or Savings Plans. "batch jobs that can be interrupted" → Spot. "BYOL license" → Dedicated Host.

## Spot instances

Spot instances use spare AWS capacity at up to 90% discount. AWS can reclaim them with a 2-minute warning when capacity is needed elsewhere.

- Define a max price you're willing to pay. If the spot price exceeds it, the instance is stopped or terminated.
- Spot Block: reserve a spot instance for 1-6 hours without interruption (rare reclaims possible)
- You must cancel the Spot Request before terminating the instance — cancelling the request does not terminate running instances

**Never use for**: databases, stateful applications, anything that can't tolerate interruption.

**Use for**: batch processing, data analysis, image processing, distributed workloads, any job with a flexible start and end time.

## Placement Groups

Controls the physical placement of instances in AWS infrastructure.

| Strategy | What it does | Limit | Use when |
|---|---|---|---|
| Cluster | All instances on the same rack in one AZ | None | Need maximum network bandwidth between instances (10 Gbps) |
| Spread | Each instance on a separate rack | 7 instances per AZ | Small number of critical instances that must not share failure |
| Partition | Groups of instances on separate racks (partitions) | 7 partitions per AZ, hundreds of instances | Large distributed systems: HDFS, Cassandra, Kafka |

**Exam trap**: Spread has a hard limit of 7 instances per AZ. If a question describes more than 7 instances needing isolation, Partition is the answer.

## EC2 Hibernate

Normal stop: instance shuts down, EBS data is kept.  
Normal terminate: instance is deleted, root EBS volume deleted (by default).  
Hibernate: the contents of RAM are written to the root EBS volume, then the instance stops. On next start, RAM is restored and the OS resumes from where it left off.

Requirements:
- Root EBS volume must be encrypted
- RAM must be less than 150 GB
- Not supported on bare metal instances
- Max hibernate duration: 60 days

Use for: long-running processes you want to pause, services with slow startup that you want to resume instantly.

## AMI (Amazon Machine Image)

An AMI is a template for launching an EC2 instance. It captures the OS, installed software, configuration, and EBS volume snapshot. When you launch from an AMI, the instance starts with everything pre-installed.

Types:
- AWS-provided public AMIs (Amazon Linux, Ubuntu, Windows)
- Your own AMIs (created from running instances)
- AWS Marketplace AMIs (third-party, may cost extra)

AMIs are region-specific. You can copy an AMI to other regions.

Process for creating your own AMI:
1. Launch an instance and configure it
2. Stop the instance (for data consistency)
3. Create an AMI — this also creates EBS snapshots
4. Launch new instances from that AMI

## Instance Metadata Service (IMDS)

From inside an EC2 instance, you can query metadata about the instance itself without using any credentials:

```
http://169.254.169.254/latest/meta-data/
```

This address is only reachable from within the instance. You can retrieve: instance ID, instance type, public/private IP, IAM role name, availability zone, security groups, and temporary credentials from the attached role.

**IMDSv1 vs IMDSv2**:

| | IMDSv1 | IMDSv2 |
|---|---|---|
| Access method | Direct GET request | Session-based (PUT first to get token, then use token) |
| Security | Vulnerable to SSRF | Protected against SSRF |
| AWS recommendation | Legacy | Use IMDSv2 |

IMDSv2 example:
```bash
TOKEN=$(curl -X PUT "http://169.254.169.254/latest/api/token" \
  -H "X-aws-ec2-metadata-token-ttl-seconds: 21600")

curl -H "X-aws-ec2-metadata-token: $TOKEN" \
  http://169.254.169.254/latest/meta-data/public-ipv4
```

**Exam trap**: "SSRF vulnerability on EC2" → enforce IMDSv2. User data is at `/latest/user-data`, metadata is at `/latest/meta-data/` — they are different endpoints.

## ENI (Elastic Network Interface)

An ENI is a virtual network card. Every EC2 instance has at least one (the primary). ENIs can be:
- Created independently and attached to instances
- Moved between instances (useful for failover: detach from a failing instance, attach to a standby)

An ENI can have:
- One primary private IPv4, and one or more secondary private IPv4s
- One Elastic IP per private IPv4
- One public IPv4
- One or more security groups
- A MAC address

ENIs are bound to a specific AZ.

## Private vs Public IP

**Public IP**: visible on the internet, must be globally unique, changes when you stop/start the instance (unless you use an Elastic IP).

**Private IP**: only reachable within the VPC, stays the same across stop/start.

**Elastic IP**: a static public IPv4 address you own and can attach to any instance. Free while in use, charged when not attached. You get 5 per region by default.

Avoid Elastic IPs when possible — they indicate a fragile architecture. Better alternatives: use DNS with a load balancer, or Route 53 health checks for failover.

## Scalability and High Availability

**Vertical scaling** (scale up/down): increase the size of the instance (e.g. t2.micro → t2.large). Simple but has a hardware limit, and requires downtime to change instance type.

**Horizontal scaling** (scale out/in): add or remove instances. Requires the application to be stateless or to share state externally. No hardware limit.

**High Availability**: run instances across multiple AZs so that if one data center fails, the application keeps running. Always pair HA with horizontal scaling.

---

# 3. EC2 Storage

## Comparison: EBS vs EFS vs Instance Store

| | EBS | EFS | Instance Store |
|---|---|---|---|
| Type | Block storage | Network file system (NFS) | Physical disk on host |
| Attached to | 1 instance (except io1/io2 Multi-Attach) | Many instances across AZs | 1 instance |
| AZ scope | 1 AZ | Multi-AZ | 1 AZ (tied to the instance) |
| Persistence | Yes | Yes | Lost on stop or terminate |
| OS support | Linux + Windows | Linux only | Linux + Windows |
| Performance | Good | Good | Best (physically attached) |
| Cost model | Pay for provisioned size | Pay per GB used | Included with instance |

## EBS — Elastic Block Store

EBS is a network drive attached to your instance. Think of it as a USB stick over the network. Because it is network-based, there is a small latency penalty compared to a physical disk, but it can be detached from one instance and attached to another.

Key properties:
- Locked to one AZ. To move it to another AZ, take a snapshot and restore it in the target AZ.
- Provisioned capacity — you pay for the size you allocate, whether you use it or not.
- Can increase capacity over time without downtime.
- By default, the root volume is deleted on instance termination. Other attached volumes are not. You can change this behavior.

## EBS Volume Types

| Type | Class | Pick when |
|---|---|---|
| gp3 | SSD | Default choice for most workloads |
| gp2 | SSD | Legacy — prefer gp3 |
| io2 Block Express | SSD | Databases needing > 16,000 IOPS or sub-ms latency |
| io1 | SSD | Databases needing > 16,000 IOPS (older option) |
| st1 | HDD | Big Data, logs, data warehouses — high throughput sequential reads |
| sc1 | HDD | Infrequently accessed data — lowest cost |

Only **gp2/gp3** and **io1/io2** can be used as boot volumes. HDD types cannot.

**gp3** specifics: 3,000 IOPS and 125 MiB/s baseline. IOPS can be scaled to 16,000 and throughput to 1,000 MiB/s independently from size.

**gp2** specifics: IOPS is tied to disk size (3 IOPS per GiB). Max 16,000 IOPS reached at 5,334 GiB.

**io2 Block Express**: sub-millisecond latency, max 256,000 IOPS. Only type supporting EBS Multi-Attach.

**Exam trap**: "lowest cost, infrequently accessed" → sc1. "high sequential throughput for Big Data" → st1. "boot volume on HDD" → not possible, must use SSD.

## EBS Snapshots

Snapshots are point-in-time backups of EBS volumes stored in S3 (managed by AWS, not in your own bucket). You can use snapshots to:
- Back up data
- Copy a volume to another AZ or region (create snapshot, restore in target location)
- Create an AMI

Best practice: take snapshots when the instance is stopped to ensure data consistency. Snapshots use I/O — avoid running them during peak traffic.

Additional snapshot features:
- **EBS Snapshot Archive**: move a snapshot to a cheaper storage tier (75% cheaper). Takes 24-72 hours to restore.
- **Recycle Bin**: recover accidentally deleted snapshots (retention 1 day to 1 year).
- **Fast Snapshot Restore**: eliminates latency on first use of restored volume (expensive).

## EBS Encryption

When you create an encrypted EBS volume:
- Data at rest is encrypted
- Data in flight between the instance and the volume is encrypted
- Snapshots are encrypted
- Volumes restored from encrypted snapshots are encrypted

Encryption uses AWS KMS (AES-256). There is minimal latency impact.

To encrypt an existing unencrypted volume:
1. Take a snapshot of the unencrypted volume
2. Copy the snapshot and enable encryption during the copy
3. Create a new volume from the encrypted snapshot
4. Replace the original volume

## EBS Multi-Attach

Only available on io1 and io2 volumes. Allows one EBS volume to be attached to up to 16 EC2 instances in the same AZ simultaneously. Each instance has full read/write access. The application must handle concurrent writes (use a cluster-aware file system).

## EC2 Instance Store

A physical disk attached directly to the host machine. Not a network drive.

- Highest I/O performance of any EC2 storage option
- **Ephemeral**: data is lost when the instance is stopped or terminated, or if the hardware fails
- Backups and replication are your responsibility
- Good for: buffer, cache, temporary files, scratch data

**Exam trap**: "highest possible IOPS" → Instance Store, not even io2 matches it. Any mention of data that must survive a restart → use EBS instead.

## EFS — Elastic File System

EFS is a managed NFS (Network File System). Multiple EC2 instances — across multiple AZs — can mount and access the same file system simultaneously.

Properties:
- Linux only (POSIX/NFS protocol)
- Scales automatically — no capacity to provision, pay per GB stored
- Multi-AZ — inherently highly available
- More expensive than EBS gp2 (roughly 3x)
- Access controlled via security groups

Storage classes (save cost with lifecycle policies):
- EFS Standard: frequently accessed files
- EFS Infrequent Access (IA): automatically move files not accessed for N days, lower cost

Use EFS when:
- Multiple instances need to read/write the same files
- Shared content directory (WordPress, web servers in an ASG)
- Content management systems

**Exam trap**: "multiple EC2 instances sharing the same files" → EFS. "Windows instances need shared storage" → EFS is wrong (Linux only), use FSx for Windows instead. "single instance storage" → EBS is cheaper.

---

# 4. Security Groups

## What they are

Security groups are virtual firewalls that control traffic to and from EC2 instances. Every instance must have at least one security group.

They contain only **allow** rules — there is no explicit deny. Traffic that does not match any allow rule is implicitly denied.

Rules can reference:
- An IP range (CIDR) — e.g. `0.0.0.0/0` for anywhere
- Another security group — e.g. "allow traffic from the load balancer's security group"

Referencing another security group is more robust than using IPs, because IPs can change. If the load balancer's security group is referenced, any instance that is part of that security group is automatically allowed, regardless of its IP.

## Key properties

- Attached to instances, not to subnets
- Can be attached to multiple instances at the same time
- One instance can have multiple security groups
- Scoped to a region/VPC combination
- Security groups are **stateful**: if inbound traffic is allowed, the response is automatically allowed (you do not need a separate outbound rule for it)
- All inbound traffic is blocked by default
- All outbound traffic is allowed by default

The security group operates **outside** the instance. If traffic is blocked, the instance never sees it — a timeout means a security group issue. A "connection refused" response means the instance received the traffic and the application rejected it.

## Diagnosing connectivity issues

| Symptom | Likely cause |
|---|---|
| Request times out | Security group is blocking the traffic |
| Connection refused | Traffic reached the instance, app is not running or rejected it |
| Works from one IP, not another | Security group rule is too restrictive on source IP |

## Classic ports to know

| Port | Protocol | Use |
|---|---|---|
| 22 | SSH / SFTP | Connect to Linux instances |
| 80 | HTTP | Unencrypted web traffic |
| 443 | HTTPS | Encrypted web traffic |
| 3389 | RDP | Connect to Windows instances |
| 3306 | MySQL / Aurora | Database connections |
| 5432 | PostgreSQL | Database connections |

## SSH access

| OS | Method |
|---|---|
| macOS / Linux | `ssh -i key.pem ec2-user@<ip>` |
| Windows < 10 | PuTTY |
| Windows 10+ | SSH (built-in) or PuTTY |
| Any OS | EC2 Instance Connect (browser-based, no key needed) |

Best practice: maintain a separate security group just for SSH access. This makes it easy to audit and restrict who can reach port 22.

---

# 5. Load Balancing

## What it is and why

A load balancer is a server that receives incoming traffic and distributes it across multiple backend instances. From the user's perspective, there is one address. Behind it, any number of servers can be running.

Benefits:
- Spread load evenly across instances
- Single DNS entry point for your application
- Health checks — automatically stop routing to unhealthy instances
- SSL termination — handle HTTPS at the load balancer, use HTTP internally
- High availability across multiple AZs

## Types of load balancers

AWS has four managed load balancers. Always use ALB or NLB for new architectures.

| Load Balancer | OSI Layer | Protocols | Pick when |
|---|---|---|---|
| ALB (Application) | 7 | HTTP, HTTPS, WebSocket | Web apps, microservices, content-based routing |
| NLB (Network) | 4 | TCP, TLS, UDP | Ultra-low latency, static IP needed, non-HTTP traffic |
| GLB (Gateway) | 3 | IP (GENEVE) | Route traffic through 3rd-party security appliances |
| CLB (Classic) | 4+7 | HTTP, HTTPS, TCP | Legacy only, do not use for new work |

## ALB — Application Load Balancer

ALB operates at Layer 7 and understands HTTP. It can route requests based on:
- **Path**: `example.com/users` → Target Group A, `example.com/api` → Target Group B
- **Hostname**: `users.example.com` → one service, `api.example.com` → another
- **Query strings / headers**: `example.com/products?type=shoe` → specific backend

ALB is the right choice for microservices and containerized applications. It integrates with ECS and can route to Lambda functions.

ALB target groups can contain:
- EC2 instances
- ECS tasks
- Lambda functions
- Private IP addresses

ALB has a fixed DNS name (not a static IP). It does not support UDP.

**Exam trap**: "route based on URL path" → ALB. "WebSocket" → ALB. "need a static IP" → ALB cannot, use NLB.

## NLB — Network Load Balancer

NLB operates at Layer 4. It does not understand HTTP — it just forwards TCP/UDP packets.

- Handles millions of requests per second with very low latency
- Has a **static IP per AZ** (or you can assign Elastic IPs) — useful for clients that need to whitelist specific IPs
- Supports TCP, TLS, UDP

**Exam trap**: "static IP for the load balancer" → NLB. "UDP traffic" → NLB. "millions of requests per second with minimal latency" → NLB.

## GLB — Gateway Load Balancer

GLB routes all traffic through a fleet of third-party virtual appliances (firewalls, intrusion detection systems) before it reaches your application. It operates at Layer 3 using the GENEVE protocol on port 6081.

Use case: compliance requirement to inspect all traffic with a third-party security appliance.

## Health checks

Every load balancer continuously polls its backend instances on a specific port and path (e.g. HTTP GET `/health`). If the response is not 2xx, the instance is marked unhealthy and removed from rotation until it recovers.

Health checks are configured at the Target Group level for ALB and NLB.

## Sticky Sessions

By default, each request is distributed to any healthy instance. With sticky sessions enabled, the same client is always routed to the same instance. This is done via a cookie with an expiration time you control.

Use case: applications that store session data locally in the instance's memory (stateful apps).

Downside: uneven load distribution if some users are heavier than others.

A better long-term solution is to move session state out of the instance (to ElastiCache or DynamoDB) so stickiness is not needed at all.

## Cross-Zone Load Balancing

Without cross-zone: traffic is distributed 50/50 between AZs, regardless of how many instances are in each AZ. If AZ-A has 2 instances and AZ-B has 8, each AZ gets 50% — the 2 instances in AZ-A each handle 25% while the 8 in AZ-B each handle 6.25%.

With cross-zone: traffic is distributed evenly across all instances in all AZs. Each of the 10 instances gets 10%.

| Load Balancer | Cross-Zone default | Inter-AZ data cost |
|---|---|---|
| ALB | On (cannot be fully disabled) | Free |
| NLB / GLB | Off | Charged if enabled |

## SSL / TLS Certificates

Load balancers can terminate SSL connections. Clients connect over HTTPS, and the load balancer communicates with backend instances over HTTP internally. This offloads the encryption work from your instances.

Certificates are managed in AWS Certificate Manager (ACM). You can attach multiple certificates to one ALB using SNI (Server Name Indication), allowing a single load balancer to serve multiple domains.

**SNI**: when a client connects, it announces the hostname it wants to reach in the TLS handshake. The load balancer selects the right certificate for that hostname. This is how one ALB can handle `api.example.com` and `shop.example.com` with different certificates.

## Connection Draining (Deregistration Delay)

When an instance is removed from the load balancer (scale-in, deployment, health check failure), the LB stops sending it new requests but gives it time to finish in-flight requests. Default is 300 seconds. You can set it to 0 to terminate instantly.

---

# 6. Auto Scaling Groups

## What it is

An ASG automatically adjusts the number of EC2 instances running based on demand. It works in both directions: adds instances when load increases (scale out) and removes them when load decreases (scale in).

An ASG ensures:
- A minimum number of instances is always running
- A maximum is never exceeded
- Desired capacity is maintained
- New instances are automatically registered with the load balancer
- Unhealthy instances are replaced automatically

ASGs themselves are free. You only pay for the EC2 instances they create.

## Launch Template

The ASG uses a Launch Template to know what kind of instance to create. It contains:
- AMI and instance type
- User Data script
- EBS volume configuration
- Security Groups
- SSH key pair
- IAM Role
- Network and subnet configuration
- Load balancer Target Group

## Scaling policies

| Policy | How it works | Use when |
|---|---|---|
| Target Tracking | Keep a metric at a target (e.g. CPU at 40%) | Default — simplest, let AWS manage the math |
| Step Scaling | Add/remove N instances per alarm threshold crossed | Need different responses at different severity levels |
| Simple Scaling | Single response to one alarm | Legacy, prefer Step |
| Scheduled | Change capacity at a fixed time | Predictable traffic patterns |
| Predictive | ML-based forecast, scales before the spike | Recurring daily/weekly load patterns |

**Exam trap**: "adjust automatically to maintain performance" → Target Tracking. "scale before Black Friday" → Scheduled or Predictive. "react more aggressively when CPU hits 90% vs 70%" → Step Scaling.

## CloudWatch integration

ASGs can scale based on any CloudWatch metric: CPU utilization, network in/out, request count per target, custom application metrics. You create a CloudWatch Alarm that triggers a scaling policy.

## ASG with Load Balancers

When connected to a load balancer, the ASG and LB work together:
- New instances are automatically added to the target group
- The ASG uses ELB health checks instead of just EC2 health checks — if the app crashes (but the server is still on), the LB detects it and the ASG replaces the instance
- When scaling in, connection draining ensures active requests finish before the instance is terminated

This combination makes your application self-healing and elastic.

## Cooldown period

After a scaling action, the ASG waits for the cooldown period (default 300 seconds) before scaling again. This prevents rapid scaling up and down ("thrashing") while metrics are still settling.

Reduce the cooldown by using a pre-configured AMI so instances start serving traffic faster.

**Exam trap**: instances launching and terminating too rapidly → cooldown is too short. Scale-in happens too slowly → cooldown is too long.

---

# 7. RDS and Aurora

## RDS Overview

RDS (Relational Database Service) is a managed service for relational databases. AWS handles provisioning, OS patching, backups, monitoring, and failover. You just use the database.

Supported engines: PostgreSQL, MySQL, MariaDB, Oracle, SQL Server, IBM DB2, Aurora.

**You cannot SSH into an RDS instance.** If you need OS-level access, use RDS Custom (for Oracle and SQL Server only) or run the database on EC2 yourself.

## RDS vs self-managed DB on EC2

| | RDS | DB on EC2 |
|---|---|---|
| OS patching | AWS manages | You manage |
| Backups | Automated | Manual |
| Multi-AZ failover | Built-in option | You build it |
| Read replicas | Built-in option | You build it |
| SSH access | No (except RDS Custom) | Yes |
| Cost | Higher | Lower, more work |

**Exam trap**: "need to install a custom database plugin" or "need to access the OS" → RDS won't work → RDS Custom or EC2.

## Backups

**Automated backups**:
- Daily full backup during the backup window
- Transaction logs backed up every 5 minutes
- Point-in-time restore to any second within the retention period (1-35 days)
- Set retention to 0 to disable

**Manual snapshots**:
- Triggered by you
- Retained forever until you delete them
- Use before a risky migration or for long-term archival

**Exam trap**: a stopped RDS instance still charges for storage. If you plan to stop it for weeks, snapshot it, delete the DB, and restore from the snapshot later — much cheaper.

## Read Replicas

A read replica is a read-only copy of the primary database. Replication is **asynchronous** — there is a small delay (usually seconds).

- Up to 15 read replicas
- Replicas can be in the same AZ, different AZ, or different region
- You must point your application explicitly to the replica endpoint for reads
- Can be promoted to a standalone database (stops replication)

**Use for**: offloading read traffic from the primary, running analytics/reporting without affecting the production database.

**Exam trap**: "database is slow because too many users are reading" → add Read Replicas. Read replicas use async replication — there can be a tiny data delay. This is fine for reporting but not for financial transactions.

## Multi-AZ

Multi-AZ creates a synchronous standby replica in a different AZ. Replication is **synchronous** — every write is confirmed on both the primary and standby before returning success.

- The standby is invisible — you cannot connect to it, it receives no traffic
- If the primary fails, AWS automatically changes the DNS endpoint to point to the standby in 60-120 seconds, with no application code change required
- Provides zero data loss (synchronous replication)

**Use for**: high availability, not performance. The standby does not handle any traffic.

**The key distinction**:

| | Read Replica | Multi-AZ |
|---|---|---|
| Purpose | Performance (scale reads) | Availability (disaster recovery) |
| Replication | Asynchronous | Synchronous |
| Standby readable | Yes | No |
| Failover | Manual (you promote it) | Automatic |
| Data loss risk | Small (async lag) | Zero |

In production, it is common to use both at the same time.

## Storage Auto Scaling

RDS can automatically increase storage when it detects it is running low. You set a Maximum Storage Threshold. No downtime required.

Use this so you never have to manually resize storage or deal with a full-disk crash.

## RDS Security

- **Encryption at rest**: using AWS KMS (AES-256). Must be set at launch time. If the master is not encrypted, read replicas cannot be encrypted. To encrypt an existing unencrypted DB: snapshot → copy with encryption enabled → restore.
- **Encryption in transit**: TLS is ready by default. Use AWS TLS root certificates on the client side.
- **IAM Authentication**: instead of username/password, use IAM roles to authenticate to MySQL and PostgreSQL on RDS.
- **Security Groups**: control network access to the RDS instance.
- **Audit Logs**: can be sent to CloudWatch Logs for longer retention.

## RDS Custom

Gives you OS and database engine access on top of a managed service. Available only for Oracle and SQL Server. Use when you need to install custom database patches or configure the OS, but still want some managed infrastructure benefits.

## RDS Proxy

A fully managed proxy that sits between your application and RDS. It pools and reuses database connections.

Without a proxy: each application thread opens its own connection to the database. Lambda functions can scale to thousands of concurrent invocations — each opening a new connection — and quickly overwhelm a database.

With RDS Proxy: the proxy maintains a pool of connections to the database. All Lambda invocations share that pool. The database only sees a manageable number of connections.

Other benefits:
- Reduces failover time by up to 66% (the proxy handles reconnection)
- Enforces IAM authentication for database access
- Credentials stored in Secrets Manager
- Never publicly accessible — must be inside a VPC

**Exam trap**: "Lambda connecting to RDS is causing too many connections" → RDS Proxy. "Reduce RDS failover time" → RDS Proxy.

## Amazon Aurora

Aurora is AWS's proprietary, cloud-native relational database. It is compatible with MySQL and PostgreSQL (your existing drivers work). It is not open source.

Performance: 5x faster than MySQL on RDS, 3x faster than PostgreSQL on RDS. Costs about 20% more than standard RDS.

Architecture advantages over standard RDS:
- Storage is decoupled from compute and shared across all nodes
- Storage grows automatically in 10 GB increments, up to 128 TB
- 6 copies of data across 3 AZs (4 copies needed for writes, 3 for reads)
- Peer-to-peer replication and self-healing
- Failover in under 30 seconds (vs 60-120 seconds for RDS Multi-AZ)

## Aurora Cluster

An Aurora cluster has one **Writer** (master) and up to 15 **Readers** (replicas). All nodes share the same storage volume — there is no per-instance disk.

Two endpoints:
- **Writer Endpoint**: always points to the current master. Your app uses this for writes.
- **Reader Endpoint**: load balances reads across all replicas. Your app uses this for reads.

Because all nodes share storage, when the master fails, a replica is promoted instantly — no data sync needed. Failover is much faster than traditional databases.

Replicas can auto-scale based on read traffic.

## Aurora Serverless

Instead of choosing an instance size, you set a min/max capacity range in ACUs (Aurora Capacity Units, roughly 2 GB RAM each). Aurora automatically scales within that range.

- Scales in milliseconds (v2), no dropped connections
- Pay per second for the capacity actually used
- Can scale to zero (pause completely) when there are no connections — you pay nothing for compute while idle
- Good for: unpredictable traffic, dev/test environments, infrequently used applications

## Aurora Global Database

Spans multiple AWS regions. One primary region handles writes. Up to 5 secondary regions receive replicated data.

- Replication lag under 1 second (storage-level replication, does not impact primary CPU)
- Up to 16 read replicas per secondary region
- If the primary region fails, a secondary can be promoted in under 1 minute (RTO < 1 min, RPO ~ 1 sec)
- Secondary regions serve local reads with low latency for global users

**Exam trap**: "global application needs low latency reads and fast disaster recovery" → Aurora Global Database. "promote secondary region after primary region failure" → takes under 1 minute.

## Restoring RDS and Aurora

Restoring from a backup or snapshot always creates a **new database** — it does not overwrite the existing one.

- **Restore RDS MySQL from S3**: create an on-premises backup, upload to S3, restore onto a new RDS MySQL instance.
- **Restore Aurora MySQL from S3**: use Percona XtraBackup to create the backup, upload to S3, restore onto a new Aurora cluster.

---

# 8. ElastiCache

## What it is

ElastiCache is managed in-memory caching — either Redis or Memcached. Caches store data in RAM for sub-millisecond access, compared to milliseconds for a database query.

The primary use: prevent the database from being hit repeatedly for the same data. The application checks the cache first. On a cache hit, it returns the data immediately. On a miss, it queries the database and writes the result to the cache for next time.

**Important**: using ElastiCache requires application code changes. You have to add cache check and cache write logic in your app.

## Redis vs Memcached

| | Redis | Memcached |
|---|---|---|
| Multi-AZ | Yes, with auto-failover | No |
| Read replicas | Yes | No (sharding instead) |
| Persistence | Yes (AOF) | No |
| Backup and restore | Yes | Serverless only |
| Data structures | Strings, lists, sets, sorted sets, hashes | Strings only |
| Multi-threaded | No | Yes |

**Exam trap**: "highly available cache" → Redis. "leaderboard / sorted data" → Redis (sorted sets). "pub/sub messaging" → Redis. "simple cache, max throughput, no HA needed" → Memcached. The exam almost always points to Redis unless the question explicitly requires Memcached's specific features.

## Caching patterns

**Lazy Loading (Cache-Aside)**: check the cache first. If the data is not there (cache miss), query the database and write the result to the cache. Only cache what is actually requested.

- Pro: only caches what is used, cache failure doesn't break the app
- Con: first request after a cache miss is always slow (cache cold start), data can be slightly stale

**Write-Through**: whenever the application writes to the database, it also writes to the cache simultaneously.

- Pro: cache is always up to date, no stale data
- Con: writes are slower (two writes every time), caches data that may never be read

Most production systems use a combination: write-through for critical data, lazy loading for everything else.

**Cache Invalidation**: when the underlying data changes, the stale cache entry must be removed or updated. This is the hard part of caching — knowing when data is "too old."

## Session Store

A common architecture pattern: store user session data in ElastiCache instead of in the web server's memory.

Without a session store: user logs in, session data is stored in Server A's RAM. Next request goes to Server B (load balancer decision). Server B has no session data and tells the user to log in again.

With ElastiCache: session data is stored centrally. Any server can retrieve it. The application becomes stateless — any server can handle any request, which is required for horizontal scaling.

Why Redis works well for this: sub-millisecond reads for every HTTP request, and TTL support means inactive sessions are automatically evicted.

## Security

- **Redis AUTH**: password-based authentication when connecting to Redis
- **TLS in transit**: encrypt connections between app and ElastiCache
- **VPC**: ElastiCache clusters run inside a VPC, not publicly accessible
- Security Groups control network access

---

# 9. Route 53

## DNS basics

DNS (Domain Name System) translates human-readable hostnames into IP addresses. When you type `www.example.com`, your browser asks a DNS resolver what IP address that maps to, then connects to that IP.

DNS hierarchy:
```
http://api.example.com.
                     └── root (the trailing dot)
              └── TLD (.com)
       └── SLD (example.com)
  └── subdomain (api)
```

Terminology:
- **Domain Registrar**: where you buy a domain name (Route 53, GoDaddy, Namecheap)
- **DNS Records**: A, AAAA, CNAME, NS, etc.
- **Zone File**: a file containing DNS records for a domain
- **Name Server (NS)**: a server that answers DNS queries for a domain
- **TLD**: top-level domain (.com, .org, .net)
- **SLD**: second-level domain (amazon.com, google.com)

## Route 53 overview

Route 53 is AWS's DNS service. It is:
- **Authoritative**: you control the DNS records
- **A Domain Registrar**: you can buy domains directly
- The only AWS service with a 100% availability SLA
- Able to perform health checks on your resources

The name "Route 53" refers to port 53, the traditional DNS port.

## Record types

| Record | Maps | Notes |
|---|---|---|
| A | Hostname → IPv4 | Most common |
| AAAA | Hostname → IPv6 | |
| CNAME | Hostname → another hostname | Cannot be used at zone apex (root domain) |
| NS | Domain → name servers | Identifies which servers are authoritative for the domain |

## Alias Records

Alias is an AWS extension to DNS, not part of the standard specification. It maps a hostname to an AWS resource.

| | CNAME | Alias |
|---|---|---|
| Zone apex (`example.com`) | Not allowed | Allowed |
| Target | Any hostname | AWS resources only |
| Cost | Charged per query | Free |
| TTL | You set it | Managed by Route 53 |

Valid Alias targets: ALB, NLB, CloudFront, API Gateway, Elastic Beanstalk, S3 website endpoint, VPC Interface Endpoint, Global Accelerator, another Route 53 record.

**Exam trap**: "point the root domain (`example.com`) to an ALB" → you cannot use CNAME for this, use an Alias A record. "point to an EC2 instance DNS name" → Alias does not support EC2 DNS names, use a CNAME or A record with Elastic IP.

## Hosted Zones

A Hosted Zone is a container for records that define how to route traffic for a domain.

- **Public Hosted Zone**: routes traffic on the internet (public domains)
- **Private Hosted Zone**: routes traffic within a VPC (internal DNS names like `internal.company.com`)

Cost: $0.50 per month per hosted zone.

## TTL (Time to Live)

TTL tells DNS resolvers how long to cache a record before asking Route 53 again.

| TTL | Effect |
|---|---|
| High (e.g. 24 hours) | Less traffic to Route 53, lower cost, but record changes propagate slowly |
| Low (e.g. 60 seconds) | More traffic to Route 53, higher cost, but changes take effect quickly |

Before changing a DNS record, lower the TTL first. Then make the change. Then raise it back up.

Alias records do not have a configurable TTL — Route 53 manages it.

## Health Checks

Health checks allow Route 53 to monitor your endpoints and automatically change DNS routing if something goes down.

Three types:
1. **Endpoint monitoring**: Route 53 sends requests to your endpoint from ~15 global locations. If more than 18% report it healthy, it is considered healthy. Supports HTTP, HTTPS, TCP.
2. **Calculated health checks**: combine multiple health checks with AND/OR/NOT logic (up to 256 child checks).
3. **CloudWatch alarm monitoring**: for private resources inside a VPC that Route 53 cannot reach directly — create a CloudWatch metric, attach an alarm, and have the health check monitor that alarm.

Health checks pass when the endpoint responds with 2xx or 3xx. They can also check the first 5,120 bytes of the response body.

**Health checks vs ping checks**:

| Level | What it checks | Action on failure |
|---|---|---|
| EC2 Status Check | Physical hardware and hypervisor | ASG replaces the instance |
| ELB Health Check | Whether the application is responding | ELB stops routing traffic to it |
| Route 53 Health Check | Whether the public endpoint is reachable globally | Route 53 changes DNS to a backup |

## Routing Policies

Routing policies define how Route 53 responds to DNS queries. DNS does not route traffic — it only responds to queries with IP addresses. The client then connects to that IP.

### Simple

Returns one or more IP addresses for a single resource. If multiple values are returned, the client picks one at random. Cannot be associated with health checks.

### Weighted

Distributes requests across multiple records by percentage. Records must have the same name and type. Weights do not need to sum to 100.

- Weight 0 on a record stops traffic to it entirely
- If all records are weight 0, all records are returned equally

Use for: A/B testing, gradual rollouts (canary deployments), splitting traffic between regions.

**Canary deployment pattern**: run version 1 at weight 95 and version 2 at weight 5. If version 2 looks stable, gradually shift the weights until it is 100.

### Latency-based

Routes the user to the AWS region that provides the lowest measured latency. Based on actual network latency between the user and each region. Can be paired with health checks.

Use when performance for a global user base is the priority.

### Failover

Active-passive setup. One record is Primary, one is Secondary. Route 53 sends all traffic to the Primary. If the Primary's health check fails, traffic automatically switches to the Secondary. When Primary recovers, traffic switches back.

The Primary must have a health check. The Secondary can point to a static S3 page, a standby server, or another region.

Use for: disaster recovery. This is the "panic button" policy.

### Geolocation

Routes users based on their geographic location (continent, country, or US state). Does not consider latency — only location. Always create a default record for users who don't match any location rule.

Use for: serve localized content (language), enforce legal restrictions (block certain countries), regional load balancing.

**Exam trap**: "compliance" or "legal restrictions" or "localized content" → Geolocation. "minimize latency globally" → Latency-based.

### Geoproximity

Routes based on geographic location of users and resources, with the ability to bias traffic. A positive bias expands the region's effective "coverage area", pulling more traffic toward it. A negative bias shrinks it.

Requires Route 53 Traffic Flow to use.

Use when you want to shift traffic weight between regions without needing exact percentages.

### IP-Based

You provide CIDR ranges (lists of IP addresses) and map them to endpoints. Route 53 checks the client's IP against your list and routes accordingly.

Use for: routing specific ISPs to specific servers, overriding inaccurate geolocation data, routing internal office traffic to a beta environment.

**Exam trap**: "specific ISP's users need to go to a different server" → IP-based routing.

### Multi-Value Answer

Returns up to 8 healthy IP addresses to the client. The client picks one. Like Simple with multiple values, but each record can have an associated health check — unhealthy addresses are filtered out before returning results.

This is client-side load balancing — there is no central load balancer. Each IP is a separate server.

Use for: basic availability without the cost of a load balancer. Not a replacement for ALB — no advanced routing features.

**Comparison**:

| Policy | Health Checks | Returns |
|---|---|---|
| Simple (multiple values) | No | All addresses, including dead ones |
| Multi-Value | Yes | Up to 8 healthy addresses only |

## Third-party registrar with Route 53

If you bought your domain at GoDaddy or another registrar, you can still use Route 53 as your DNS provider:

1. Create a Hosted Zone in Route 53
2. Copy the NS (name server) records from Route 53
3. Update your registrar's NS settings to point to Route 53's name servers

The registrar and DNS provider are separate roles. Any domain registrar can delegate DNS to Route 53.

---

# 10. S3 — Simple Storage Service

## What it is

S3 is object storage — you store files (objects) in containers (buckets). It is one of the foundational AWS services, used for almost everything: backups, static websites, data lakes, software delivery, media hosting, log storage.

Key properties:
- Advertised as "infinitely scalable" — no storage limit per bucket
- 99.999999999% (11 nines) durability — objects are redundantly stored across multiple AZs
- 99.99% availability for S3 Standard
- Not a file system — there are no real directories, only keys with slashes in the name

## Buckets and objects

**Buckets**:
- Container for objects, created at the region level
- S3 looks global in the console, but buckets are actually regional
- Bucket names must be globally unique across all AWS accounts and regions
- Naming rules: lowercase letters and numbers only, 3-63 characters, no IPs, must not start with `xn--`, must not end with `-s3alias`

**Objects**:
- A file stored in a bucket
- Identified by a **key** — the full path: `my-folder/subfolder/file.txt`
- There are no actual directories. The slashes in the key are just part of the name. The console shows them as folders, but that is only visual.
- Max object size: 5 TB
- For objects larger than 5 GB, you must use **multi-part upload**

Object metadata:
- System metadata: content type, last modified, etc.
- User metadata: custom key-value pairs (up to 10 tags per object, useful for lifecycle and security rules)
- Version ID (if versioning is enabled on the bucket)

## Security

**User-based (IAM Policies)**: which API calls are allowed for a specific IAM user or role.

**Resource-based**:
- **Bucket Policy**: JSON policy attached to the bucket. Used to grant public access, enforce encryption, or allow cross-account access.
- **Object ACL**: fine-grained access control per object (can be disabled).
- **Bucket ACL**: less common (can be disabled).

An IAM principal can access an S3 object if:
- The user's IAM policy allows it, OR the resource policy allows it
- AND there is no explicit deny

## S3 Bucket Policies

Bucket policies are the most common way to manage S3 access. Common uses:
- Grant public read access to all objects (static website)
- Force all uploaded objects to be encrypted
- Allow another AWS account to read/write objects (cross-account access)
- Restrict access to a specific VPC endpoint

## When to use S3

| Scenario | Why S3 |
|---|---|
| Static website hosting | S3 can serve HTML/CSS/JS directly |
| Store user-uploaded files | Cheap, durable, scalable |
| Application logs | Integrates with Athena for SQL queries on log data |
| Backup and archive | Cross-region replication, Glacier for cheap archival |
| Share large files | Pre-signed URLs for temporary access |
| Data lake | Store raw data; query with Athena, process with EMR |

---

# Quick Reference: Exam Decision Guide

## "Which database should I use?"

| Requirement | Answer |
|---|---|
| Relational database, managed, SQL | RDS |
| Need OS/plugin access on relational DB | RDS Custom (Oracle/SQL Server) or DB on EC2 |
| Maximum performance relational DB | Aurora |
| DB must never go down | RDS or Aurora Multi-AZ |
| Too many reads hitting the DB | Add Read Replicas |
| Lambda functions overloading DB connections | RDS Proxy |
| Global users, < 1 second replication | Aurora Global Database |
| Unpredictable/intermittent DB traffic | Aurora Serverless |
| Cache frequently read data | ElastiCache |
| Session state for stateless app | ElastiCache |

## "Which load balancer?"

| Requirement | Answer |
|---|---|
| Route by URL path or hostname | ALB |
| WebSocket or HTTP/2 | ALB |
| Static IP on the load balancer | NLB |
| UDP or raw TCP | NLB |
| Millions of req/sec, ultra-low latency | NLB |
| Inspect traffic with a firewall appliance | GLB |

## "Which storage?"

| Requirement | Answer |
|---|---|
| Default block storage for EC2 | EBS gp3 |
| Highest IOPS / lowest latency block storage | EBS io2 Block Express |
| Lowest cost for infrequent access | EBS sc1 |
| Shared files across multiple EC2 (Linux) | EFS |
| Shared files for Windows EC2 | FSx for Windows |
| Maximum raw I/O, data loss acceptable | EC2 Instance Store |
| Object storage, backups, static files | S3 |

## "Which scaling approach?"

| Requirement | Answer |
|---|---|
| Maintain performance automatically | Target Tracking |
| Scale differently at different stress levels | Step Scaling |
| Scale for a known event (e.g. Friday spike) | Scheduled Scaling |
| Scale based on predicted patterns | Predictive Scaling |
| Instances launching/terminating too fast | Increase cooldown period |

## "Which EC2 purchasing option?"

| Requirement | Answer |
|---|---|
| Short-term, unpredictable | On-Demand |
| Always running, same instance type | Reserved |
| Always running, flexible instance type | Savings Plans |
| Batch jobs, fault-tolerant, cheap | Spot |
| BYOL license | Dedicated Host |
| Compliance: no shared hardware | Dedicated Instance |

## "Which Route 53 routing policy?"

| Requirement | Answer |
|---|---|
| Single resource | Simple |
| A/B testing, gradual rollout | Weighted |
| Route by user location | Geolocation |
| Route by latency to each region | Latency-based |
| Primary + backup site | Failover |
| Specific ISP or IP range | IP-based |
| Basic availability, multiple healthy IPs | Multi-Value |
| Shift traffic by adjusting geographic bias | Geoproximity |
