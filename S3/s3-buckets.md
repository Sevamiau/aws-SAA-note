# S3 buckets

- amazon s3 allows people to store objects (files) in 'buckets' (directories)
- buckets are defined at the region level
- s3 looks like a global service but buckets are created in a region

- Naming:
  * Shared global namespace — must have a globally unique name (across all regions and accounts)
  * Account regional namespace — allows for 'reuse' of the same bucket name across regions

- Naming constrains:
  * No uppercase, no underscore
  * Not an ip 
  * Must start with lowercase letter or number
  * Must not start with the prefix xn--
  * Must not end with the suffix -s3alias 
