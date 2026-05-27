# Amazon S3 Event Notifications with Amazon EventBridge

- Advanced filtering options beyond file name (object size, metadata, tags...)
- Send events to over 18 AWS services simultaneously (Step Functions, Kinesis, CloudWatch...)
- **Archive**: store all S3 events for a custom retention period (or indefinitely)
- **Replay**: re-send past events to reprocess them (e.g. after fixing a Lambda bug)

- Must enable **Amazon EventBridge notification** setting in S3 Bucket Properties (off by default)
