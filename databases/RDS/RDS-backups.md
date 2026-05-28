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

- **Exam trap**: a stopped RDS instance still charges you for storage. If you plan to stop it for a long time, snapshot it and delete the DB — restore from snapshot later. Snapshot storage is much cheaper than DB storage.

## Automated vs Manual — when each matters

- **Automated backups**: point-in-time recovery, retained up to 35 days — use for accidental data corruption or "restore to 10 minutes ago" scenarios
- **Manual snapshots**: kept forever until you delete them — use before a risky migration or for long-term archival


## Aurora Backups

- Automated Backups:
 * 1 to 35 days  (cannot be disabled)
 * point-in-time recovery in that timeframe


- Manual DB snapshot:
  * Manually triggered by the user
  * Retention of backup for as long as you want
----------

