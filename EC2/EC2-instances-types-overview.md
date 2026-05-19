# EC2 Instance Types Overview

- You can use different types of EC2 instances optimized for different use cases
- AWS naming convention: `m5.2xlarge`
  - `m`: instance class
  - `5`: generation (AWS improves them over time)
  - `2xlarge`: size within the instance class

---

## General Purpose

- Great for a diversity of workloads such as web servers or code repositories
- Balance between Compute, Memory, and Networking

## Compute Optimized (C)

- Great for compute-intensive workloads requiring high performance processors:
  - Batch processing workloads
  - Media transcoding
  - High performance web servers
  - High performance computing (HPC)
  - Scientific modeling and machine learning
  - Dedicated gaming servers

## Memory Optimized (R)

- Use cases:
  - High performance relational/non-relational databases
  - Distributed web scale cache
  - In-memory databases optimized for BI (business intelligence)
  - Applications performing real-time processing of big unstructured data

## Storage Optimized (I)

- Great for storage-intensive tasks requiring high sequential read/write access to large datasets on local storage
- Use cases:
  - High frequency online transaction processing (OLTP) systems
  - Relational and NoSQL databases
  - Cache for in-memory databases (e.g. Redis)
  - Data warehousing applications
  - Distributed file systems
