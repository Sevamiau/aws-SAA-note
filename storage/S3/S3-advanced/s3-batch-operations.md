# Amazon S3 Batch Operations

- Perform bulk operations on existing S3 objects with a single request
- Examples: 
    * Modify object metadata & properties 
    * Copy objects between S3 buckets
    * **Encrypt un-encrypted objects**
    * Modify ACLs, tags
    * Restore objects from S3 Glacier
    * Invoke Lambda Function to perform a custom action on each object 

- A job consists of a list of objects, the action to perform, and optional parameters
- S3 Batch Operations manages retries, tracks progress, sends completion notifications, generates reports
- You can use S3 Inventory to get object list and use Athena to query and filter your objects 
