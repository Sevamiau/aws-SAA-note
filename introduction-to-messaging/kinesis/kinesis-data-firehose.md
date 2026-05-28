# Amazaon Data Firehose 

- Note: used to be called "Kinesis Data Firehose"
- Fully Managed Service:
    * Amazon Redshift / Amazon S3 / Amazon OpenSearch Service 
    * 3rd party: Splunk / MongoDB / Datadog / New Relic 
    * Custom HTTP Endpoint 

- Automatic scaling, serverless, pay for what you use. 
- Near Real-Time with buffering capability based on size / time 
- Supports CSV, JSON, Parquet, Avro, Raw Text, Binary data 
- Conversion to Parquet/ORC, compression with gzip / snappy 
- Custom data transformations using AWS Lambda (ex: CSV to JSON )

- Kinesis Data Stream VS Amazon Data Fire

| kinesis   | Firehose    |
|--------------- | --------------- |
| Streaming data collection   | Load straming data into s3 / Redshift / OpenSearch / 3rd party / custom HTTP   |
| Producer and consumer code| Fully Managed   |
| Real-Time   | Near Real-Time  |
| Provisioned / on-demand mode   | Automatic scaling    |
| Replay Capabillty    | No data storage     |
|                      |   Does not support replay capability |
