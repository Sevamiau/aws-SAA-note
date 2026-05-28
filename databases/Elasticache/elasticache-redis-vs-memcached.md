# ElastiCache - Redis vs Memcached

## Comparison table

| | Redis | Memcached |
|---|---|---|
| Multi-AZ | Yes, with auto-failover | No |
| Read replicas | Yes | No (uses sharding instead) |
| Data persistence | Yes (AOF) | No |
| Backup & restore | Yes | Serverless only |
| Data structures | Strings, hashes, sets, sorted sets, lists | Strings only |
| Multi-threaded | No | Yes |
| Use case | Sessions, leaderboards, pub/sub, complex data | Pure caching, simple key-value, max throughput |

---

## When to use each

**Redis**: whenever you need the cache to survive a failure, or you need data structures beyond simple key-value (sorted sets for leaderboards, pub/sub for notifications).

**Memcached**: pure cache with no persistence needed, want to maximize throughput with multi-threaded architecture, simplest possible setup.

---

## Exam trap

- "High availability cache" → Redis (Memcached has no replication or failover)
- "Leaderboard" or "sorted data" → Redis (sorted sets)
- "Pub/Sub messaging" → Redis
- "Simple distributed cache, multi-threaded" → Memcached
- The exam almost always points to Redis unless the question explicitly says "simple cache, no HA needed"
