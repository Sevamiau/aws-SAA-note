# Amazon S3 Access Points 

- Access Points simplify security management for S3 buckets 
- Each Access Point has:
    * Its own DNS name (internet origin or VPC origin)
    * An Access Point policy (similar to bucket policy) — manages security at scale 


## VPC Origin

- Access Point can be restricted to be accessible only from within a VPC
- Must create a VPC Endpoint to access the Access Point (Gateway or Interface Endpoint)
- Three policies must all allow access: VPC Endpoint Policy, Access Point Policy, and S3 Bucket Policy


## Object Lambda

- Use AWS Lambda Functions to change the object before it is retrieved by the caller application
- Only one S3 bucket is needed, on top of which we create S3 Access Point and S3 Object Lambda Access Points
