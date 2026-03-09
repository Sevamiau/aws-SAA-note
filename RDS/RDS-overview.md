# Amazon RDS Overview

----------

- RDS stands for Relational Database Service
- Its a managed DB service for DB uses SQL as a query lenguage
- It allows you to create databases in the cloud that are managed by AWS 
  * Postgres
  * MySQL
  * MariaDB
  * Oracle
  * Microsoft SQL Server
  * IBM DB2
  * Aurora (Aws Propietary Database)

  ----------
# Advantage over using RDS versus deploying DB on EC2

- RDS is a manged service:
  * Automated provisioning, OS patching
  *Continuous backups and restore to specific timestamp (point in time restore)
  * Monitoring dashboards
  * Read replicas for improved read performance 
  * Multi AZ setup for DR (Disaster Recovery)
  * Maintenance windows for upgrades
  * Scaling capability (vertical and horizontal)
  * Storage backed by EBS 

- **BUT** you cant SSH into your instances


