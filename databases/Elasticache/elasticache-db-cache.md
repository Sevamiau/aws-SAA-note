# Elasticache Solutions Architecture - DB cache 

----------

-ElastiCache is AWS’s "In-Memory" storage service.If Aurora is the high-speed hard drive of your application, ElastiCache is the RAM.

- Applications queries Elasticache, if not available, get from RDS and store in Elasticache
- Helps relieve load in RDS 
- Cache must have an invalidation strategy to make sure only the most current data is used in there 


----------

