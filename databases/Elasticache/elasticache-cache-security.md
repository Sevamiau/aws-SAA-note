# Elasticache - Cache Security

----------

- Elasticache supports IAM authentication for Redis 
- IAM policies on Elasticache are only used for AWS API-level Security

- Redis AUTH:
  * You can set a "password/token" when you create a Redis cluster
  * This is an extra level of Security for your cache (on top of Security groups)
  * Support SSL in-flight encryption

- Memcached:
  * Supports SASL-based authentication (advanced) 

----------

