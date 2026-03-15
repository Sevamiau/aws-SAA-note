# RDS Backups

----------

- Automated backups:
 * Daily full backup of the database (during the backup window)
 * Transaction logs are backed-up by RDS every five minutes 
 * => ability to restore to any point in time (from oldest backup to 5 minutes ago)
 * 1 to 35 days of retention, set 0 to disable automated backups 

- Manual DB snaphots
  * Manually triggered by the user 
  * Retention of backup for as long as you want

- **TRICK**: In a stopped RDS database you will still pay for storage. If you plan on stopping it for a long time, will be convienient for you to take a snapshot and delete the original DB  restore later. The snapshot will cost way less than than the actual storage of the RDS DB.


## Aurora Backups

- Automated Backups:
 * 1 to 35 days  (cannot be disabled)
 * point-in-time recovery in that timeframe


- Manual DB snapshot:
  * Manually triggered by the user
  * Retention of backup for as long as you want
----------

