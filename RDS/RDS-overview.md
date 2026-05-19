# Amazon RDS Overview

- RDS = Relational Database Service
- Managed DB service — uses SQL as the query language
- Supported engines:
  - PostgreSQL
  - MySQL
  - MariaDB
  - Oracle
  - Microsoft SQL Server
  - IBM DB2
  - Aurora (AWS proprietary)

---

## RDS vs self-managing a DB on EC2

| | RDS (managed) | DB on EC2 |
|---|---|---|
| OS patching | AWS handles it | You handle it |
| Backups | Automated | Manual |
| Multi-AZ / HA | Built-in option | You build it |
| Read replicas | Built-in option | You build it |
| SSH access | No | Yes |
| Cost | Higher | Lower (but more work) |

**Exam trap**: "You need to SSH into the database OS" or "install a custom DB plugin" → you cannot do this on RDS → use RDS Custom or run DB on EC2.

RDS is the right answer unless the question explicitly needs OS-level access.

---

## RDS managed benefits

- Automated provisioning and OS patching
- Continuous backups with point-in-time restore (up to 35 days)
- Monitoring dashboards
- Read replicas for improved read performance
- Multi-AZ for disaster recovery
- Maintenance windows for upgrades
- Vertical and horizontal scaling
- Storage backed by EBS
- **You cannot SSH into RDS instances**
