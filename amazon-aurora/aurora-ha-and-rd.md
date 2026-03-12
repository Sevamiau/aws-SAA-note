# Aurora High Availability and Read Scaling

----------

- 6 copies of your data across 3 AZ:
  * 4 copies out of 6 needed for writes
  * 3 copies out of 6 need for reads
  * Self healing with peer-to-peer replication
  * Storage is striped across 100s of volumes

- One Aurora instance takes writes (Master)
- Automated failover for master in less than 30 seconds
- Master + up to 15 Aurora Read Replicas
- support for Cross Region Replication

----------

