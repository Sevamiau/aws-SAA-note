# EFS - Performance and storage classes 

-EFS Scale
    .1000s of concurrent NFS clients, 10 GB+ /s throughput
    .Grow to petabyte-scale network file system, automatically

-Performance Mode (set at EFS creation time)
    .General Purpose (default) - Latency sensitive use cases (web servers, cms, etc...)
    .Max I/O - Higher latency, throughput, highly parallel (big data, media processing)

-throughput mode:
    .Bursting - 1 TB = 50 MiB/s + burst of up to 100MiB/s 
    .Provisioned - Set your throughput regardless of storage size. ex: 1GiB/s for 1 TB store


## Storage classes:

-Storage tiers (lifecycle management feature - move file after N days)
    .Standard: For frecuently accessed files
    .Infrequent acces (EFS-IA): Cost to retrieve files, lower price to store
    .Archive: Rarely accessed data (few times each year) 50% cheaper
    .Implement lifecycle policies to move files between storage 

## Availability and durability:
    .Standard: Multi AZ, great for prod 
    .One zone: One AZ. great for dev, backuo, enabled by default, compatible with IA (EFS one zone-IA)

-Over 90% in cost savings
