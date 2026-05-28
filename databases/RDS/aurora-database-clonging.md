# Aurora Database Cloning

----------

- Create a new Aurora DB Cluster from an existing one 
- Faster than snapshots & restore
- Uses **copy-on-write** protocol:
 * Initially the new DB cluster uses the same data volume as the original DB cluster (fast and efficient - no copying is needed)

 * When updates are made to the new DB cluster data, then additional storage is allocated and data is copied to be separated.

- Very fast and cost-effective
- Useful to create a "staging" database from a "production" database without impacting the production database 

----------

