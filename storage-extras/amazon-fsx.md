# Amazon FSx - Overview

- Launch 3rd party high-performance file systems on AWS
- Fully Managed Service 

## Amazon FSx For Windows (File Server)

- FSc for Windows is a fully managed Windows file system share drive 
- Support SMB protocol & Windows NTFS 
- Microsoft Active Directory Integrations, ACLs, user quotas.
- Can be mounter on Linux EC2 instances 
- Supports Microsoft Distributed File systems (DFS) Namespaces (group files across multiple FS)

- Scale up to 10s of GB/s, millions of IOPS, 100s PB of data 
- Storage Options:
    * SSD - Latency sensitive workloads (databases, media processing, data analysis)
    * HDD - broad sprectrum of workloads (home, Directory,CMS...)
- Can be accessed from your on-premises infrastructure (VPN or Direct Connect)
- Can be configured to be Multi-AZ (high availability)
- Data is backed-up daily to S3 

## FSx For Lustre 

- Lustre is a type of parallel distributed file system, for large-scale computing
- The name Lustre is derived from "Linux" and "Cluster"

- **Use Cases:**
    * Machine Learning, High Performance Computing (HCP)
    * Video Processing, Financial Modeling, Electronic Design Automation
    * Scales up to 100s GB/s, millions of IOPS, sub-ms latencies 

- Storage Options: 
    * SSD - Low-latency, IOPS intensive workloads, small & random file operations
    * HDD - Troughput-intensive workloads, large & sequential file operations

- Seamless Integrations With s3 
    * Can "read S3" asa file system (trough FSx)
    * Can write the output of the computations back to S3 (trough FSx)

- Can be used from on-premises servers (VPN or Direct Connect)

## FSx File System Deployment Options 

- Scratch File System 
    * Temporary storage 
    * Data is not replicated (does not persist if file server fails)
    * Hight burst (6x faster, 200MBps per TiB)
    * Usage: Short-term processing, optimize costs 

## FSx for NetApp ONTAP

- Managed NetApp ONTAP on AWS 
- File System compatible with NFS, SMB, iSCSI protocol
- Move workloads running on ONTAP or NAS to AWS 
- Works with:
    * Linux
    * Windows
    * MacOs 
    * VMware Cloud on AWS 
    * Amazon Workspace & AppStream 2.0
    * Amazon EC2, ECS and EKS 
- Storage shrinks or grows automatically 
- Snapshots, replication, low-cost, compression and data de-duplication 
- Point-in-time instantaneous cloning (helpful for testing new workloads)

## FSx for OpenZFS

- Managed OpenZFS file system on AWS 
- File System compatible with NFS (v1,v4,v4.1, v4.2)
- Move workloads running on ZFS to AWS 
- Works with:
    * Linux
    * Windows
    * MacOs
    * VMware Cloud on AWS 
    * Amazon Workspace & AppStream 2.0
    * Amazon EC2, ECS and EKS 

- Up to 1,000,000 IOPS with < 0.5ms latency 
- Snapshots, compression and low-cost
- Point-in-time instantaneous cloning
