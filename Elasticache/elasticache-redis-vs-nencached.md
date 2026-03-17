# Elasticache - Redis vs Memecached

----------


- **REDIS**:
  * Multi AZ with auto-failover
  * Read Replicas to scale reads and have high availability 
  * Data durability using AOF presistance
  * Backup and restore features
  * Supports Sets and Sorted Sets 

*VS*

- **MEMECACHED**
 * Multi-node for partitioning of data (sharding)
 * No high availability (replication)
 * Non persistent 
 * Backup and restore (serverless)
 * Multi-threaded architecture

----------

