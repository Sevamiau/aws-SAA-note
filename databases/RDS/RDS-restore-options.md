# RDS & Aurora Restore options

----------

- Restoring a RDS / Aurora backup pr a snapshot creates a new database


- **Restoring MySQL RDS database from S3**
  * Create a backup of your on-premises database
  * Store it on Amazon S3 (object storage)
  * Restore the backup file onto a new RDS instance running MySQL

- **Restoring MySQL Aurora cluster from S3**
 * Create a backup of your on-premises database using Percona XtraBackup
 * Store the backup file on Amazon S3 
 * Restore the backup file onto a new Amazon cluster running MySQL

----------

