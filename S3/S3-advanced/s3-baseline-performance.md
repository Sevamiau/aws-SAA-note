# Amazon S3 Baseline Performance 

- Amazon S3 automatically scales to high request rates, latency 100-200 ms 
- Your app can achieve at least 3,500 PUT/COPY/POST/DELETE or 5,500 GET/HEAD requests per second per prefix in a bucket
- There are no limits to the number of prefixes in a bucket 

- Example (object path => prefix):
    * bucket/folder1/sub1/file => /folder1/sub1/
    * bucket/folder1/sub2/file => /folder1/sub2/
    * bucket/1/file => /1/ 
    * bucket/2/file => /2/ 

- If you spread reads across all four prefixes evenly, you can achieve 22,000 requests per second for GET and HEAD     


## Multi-Part Upload

- Recommended for files > 100MB, must use for files > 5GB 
- Can help parallelize uploads (speed up transfers)
- If one part fails, only that specific part needs to be re-uploaded


## S3 Transfer Acceleration

- Increase transfer speed by transferring file to an AWS edge location which will forward the data to the S3 bucket in the target region
- Compatible with Multi-Part Upload 


## S3 Byte-Range Fetches

- Parallelize GETs by requesting specific byte ranges
- Better resilience in case of failures — only the failed byte range needs to be retried
- Can be used to retrieve only partial data (e.g. only the header of a file)
