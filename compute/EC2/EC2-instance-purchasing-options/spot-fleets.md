# Spot Fleets

-Spot Fleets=set of spot instances + (optional) on-demand instances
-The spot Fleet will try to meet the target capacity with price constraints
    .Define possible launch pools: Instance type(m5.large),OS, availability zone 
    .Can have multiple launch pools, so that the fleet can choose
    .spot fleet stops launching instances when reaching capacity or max cost 

-Strategies to allocate Spot instances
    .LowestPrice: From the pool with the lowest price (cost optimization, short workload)
    .Diversified: distributed across all pools (great for availability, long workloads)
    .capacityOptimized: pool with the optimal capacity for the number of instances
    .priceCapacityOptimized (recommended): pools with highest capacity available, then select the pool with the lowest price (best choice for most workloads)

Spot Fleets allows us to automatically request spot instances with the lowest price
