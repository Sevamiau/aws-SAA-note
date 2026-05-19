# Amazon S3 — Introduction

- Amazon S3 is one of the main building blocks of AWS
- Advertised as "infinitely scaling" storage
- Many websites use Amazon S3 as a backbone
- Many AWS services use Amazon S3 as an integration

## What S3 is used for

- **Static file storage**: images, videos, files, backups
- **Static website hosting**: serve HTML/CSS/JS directly from a bucket
- **Data lake**: store huge amounts of data for analytics
- **Disaster recovery & backup**: durable storage (11 nines = 99.999999999% durability)
- **Software delivery**: distribute software packages

## Key concepts

| Concept | Description |
|---|---|
| **Bucket** | Container for objects, defined at the region level |
| **Object** | A file stored in a bucket (up to 5TB per object) |
| **Key** | The full path of an object within a bucket |
| **Versioning** | Keep multiple versions of an object |
| **Durability** | 11 nines (99.999999999%) — S3 stores data across multiple AZs |
| **Availability** | 99.99% for S3 Standard |

## SAA-C03 Exam Tips

- S3 is **not** a file system — there are no real directories, just keys with slashes
- S3 buckets are **regional** but the namespace is **global** (bucket names must be globally unique)
- For objects > 5GB, use **multi-part upload**
- S3 is the go-to answer for: static website hosting, data lake, backup, and log storage scenarios
