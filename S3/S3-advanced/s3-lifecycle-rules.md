# Amazon S3 Lifecycle Rules

- **Transition Actions**:
    * Move objects to Standard IA class 60 days after creation
    * Move to Glacier for archiving after 6 months

- **Expiration Actions** — Configure objects to expire (delete) after some time
    * Access log files can be set to delete after 365 days
    * Can be used to delete old versions of files (if versioning is enabled)
    * Can be used to delete incomplete Multi-Part uploads

- Rules can be created for a certain prefix (example: s3://mybucket/mp3/*)
- Rules can be created for certain object tags (example: Department: Finance)



