# S3 security

- User-Based:
  * IAM policies: Which API calls should be allowed for a specific user from IAM

- Resource-Based:
  * Bucket Policies: Bucket wide rules from the S3 console - allows cross account
  * Object Access Control List (ACL) - finer grain (can be disabled)
  * Bucket Access Control List (ACL) — less common (can be disabled)

- Note: an IAM principal can access an S3 object if:
  * The user IAM permissions ALLOW it OR the resource policy ALLOWS it
  * AND there's no explicit DENY

- Encryption: encrypt objects in Amazon S3 using encryption keys

## S3 Bucket Policies

- Grant public access to the bucket
- Force objects to be encrypted at upload
- Grant access to another account (cross-account)

