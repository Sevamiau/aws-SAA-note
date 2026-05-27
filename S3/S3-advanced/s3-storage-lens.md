# Amazon S3 Storage Lens 

- Understand, analyze, and optimize storage across entire AWS organization
- Discover anomalies, identify cost efficiencies, and apply data protection best practices across entire AWS organization (30 days usage & activity metrics)
- Aggregate data for organization, specific accounts, regions, buckets, or prefixes
- Default dashboard or create your own dashboard
- Can be configured to export metrics daily to an S3 bucket (CSV, Parquet)

## Default Dashboard

- Visualize summarized insights and trends for both free and advanced metrics
- Default dashboard shows Multi-Region and Multi-Account data 
- Preconfigured by Amazon S3 
- Can't be deleted but can be disabled 

## Metrics 

### Summary Metrics

- General insights about your S3 storage 
- StorageBytes, ObjectCount...
- **USE CASES**: Identify the fastest-growing (or not used) buckets and prefixes 

### Cost Optimization Metrics 

- Provide insights to manage and optimize your storage costs 
- NonCurrentVersionStorageBytes, IncompleteMultipartUploadStorageBytes...
- **USE CASES**: Identify buckets with incomplete multipart uploads older than 7 days, identify which objects could be transitioned to a lower-cost storage class

### Data-Protection Metrics

- Provide insights for data protection features
- VersioningEnabledBucketCount, MFADeleteEnabledBucketCount, SSEKMSEnabledBucketCount, CrossRegionReplicationRuleCount...
- **USE CASES**: Identify buckets that aren't following data protection best practices  

### Access-Management Metrics 

- Provide insights for S3 Object Ownership
- ObjectOwnershipBucketOwnerEnforcedBucketCount
- **USE CASES**: Identify which Object Ownership settings your buckets use 

### Event Metrics

- Provide insights for S3 Event Notifications
- EventNotificationsEnabledBucketCount — identify which buckets have S3 Event Notifications configured
