# RDS - From Single-AZ to Multi-AZ

----------

- Zero downtime operation (no need to stop the DB)
- Just click on *modify* for the database

## The following happens internally:
  * A snapshot is taken
  *A new DB is restored from the snapshot in a new AZ 
  * Synchronization is established between the two databases 

----------


