# RDS Proxy

- Fully managed database proxy that sits between your app and RDS/Aurora
- Pools and shares DB connections — reduces the number of open connections to the database
- Reduces CPU/RAM stress on the database from connection overhead
- Serverless, autoscaling, multi-AZ (highly available)
- Reduces failover time for RDS and Aurora by up to 66%
- Supports: RDS (MySQL, PostgreSQL, MariaDB, SQL Server) and Aurora (MySQL, PostgreSQL)
- No code changes required for most apps
- Enforces IAM authentication, stores credentials in Secrets Manager
- Never publicly accessible — must be inside a VPC

---

## When to use it

**Lambda connecting to RDS** is the classic use case. Lambda functions scale to thousands of concurrent executions, each opening its own DB connection. Without a proxy, this overwhelms the database with too many simultaneous connections. RDS Proxy pools those connections so the DB only sees a manageable number.

Other cases:
- Any app that opens many short-lived connections (serverless, microservices)
- You want automatic failover to be faster without changing app code
- You want to enforce IAM auth for DB access without modifying the DB

---

## Exam trap

- "Lambda function connecting to RDS is causing too many connections" → RDS Proxy
- "Reduce DB failover time" → RDS Proxy
- RDS Proxy is never in a public subnet — always accessed from within the VPC
