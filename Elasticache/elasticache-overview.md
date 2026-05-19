# Amazon ElastiCache Overview

----------

- The same way RDS is to get managed Relational Databases, ElastiCache is to get managed Redis or Memached
- Caches are in-memory databases with really high performance and low latency
- Helps reduce load off of databases for read intensive workloads 
- Helps make your app stateless 
- AWS takes care of OS maintenance / patching, optimizations, set up, config, monitoring, failure recovery and backups

- **Using ElastiCache involves heavy app code changes**

---

## When to use ElastiCache

Use ElastiCache when your database is the bottleneck because the same data is being read repeatedly. Instead of hitting the DB every time, the app reads from the cache (fast) and only goes to the DB on a cache miss.

Common triggers in exam scenarios:
- "Database is overwhelmed with read traffic" → add ElastiCache in front of it
- "Store user session data so any instance can pick up the session" → ElastiCache session store
- "Reduce latency for frequently accessed data" → ElastiCache

Not a drop-in replacement for a database — only useful for data that can tolerate being slightly stale.

