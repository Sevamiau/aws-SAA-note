# Amazon Aurora


Amazon Aurora is a high-performance, fully managed relational database service provided by AWS. It is part of the Amazon RDS (Relational Database Service) family but is built on a custom, cloud-native architecture that is significantly faster and more resilient than standard databases.

----------

- Aurora is a proprietary technology from AWS (not open source) 
- Postgres and MySQL are both supported as Aurora DB (that means your drivers will work as if Aurora was a Postgres or MySQL database)
- Aurora is 'AWS Cloud optimized' and claims 5x performance improvement over MySQL on RDS, over 3x the performance of Postgres on RDS
- Aurora storage automatically grows in increaments of 10GB, up to 256TB.
- Aurora can have up to 15 replicas and the replication process is faster than MySQL (sub 10 ms replica lag)
- Failover in Aurora is instantaneous. Its HA native.
- Aurora costs more than RDS (20%) but its more efficient

----------

