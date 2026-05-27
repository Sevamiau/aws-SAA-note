# Amazon S3 Event Notifications

- S3: ObjectCreated, S3:ObjectRemoved, S3:ObjectRestore, S3:Replication...
- Object name filtering possible (*.jpg)
- **Use Cases**: Generate thumbnails of images uploaded to S3
- Can create as many "S3 events" as desired
- S3 event notifications typically deliver events in seconds but can sometimes take a minute or longer

## IAM Permissions

- Destinations require a **Resource Policy** to allow S3 to send events (S3 buckets cannot have IAM Roles attached)
    * **SNS Topic Policy** — allows S3 to Publish to the topic
    * **SQS Queue Policy** — allows S3 to SendMessage to the queue
    * **Lambda Resource-based Policy** — allows S3 to Invoke the function
- Policy must include `Principal: s3.amazonaws.com` and a Condition with the specific source bucket ARN
