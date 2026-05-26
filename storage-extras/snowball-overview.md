# Amazon Snow Family Overview

- Highly-secure, portable devices to collect and process data at the edge and migrate into and out of AWS 
- Helps migrate up to Petabytes of data

| Device | Compute | Memory | Storage (SSD) |
| --------------- | --------------- | --------------- | --------------- |
| Snowball Edge Storage Optimized | 104 vCPUs | 416 GB | 210 TB |
| Snowball Edge Compute Optimized | 104 vCPUs | 416 GB | 28 TB |

## Data Migration With Snowball 

- **Challenges:** 
    * Limited Connectivity 
    * Limited bandwidth
    * High network cost
    * Shared bandwidth (cant maximize the line)
    * Connection stability 

|  | Time to Transfer |
|  | 100 Mbps | 1 Gbps | 10 Gbps |
| --------------- | --------------- | --------------- | --------------- | --------------- |
| 10 TB | 12 days | 30 hours |  | 3 hours |
| 100 TB| 124 days | 12 days | 30 hours |
| 1 PB | 3 years | 124 days | 12 days |



## What is Edege Computing?

- Proccess data while its being created on and edge location:
    * A truck on the road, a ship on the sea, a mining station underground

- These locations may have limited internet and no access to Computing power
- We setup a Snowball Edge device to do edge Computing
    * Snowball Edge Compute Optimized (dedicated for that use case) & Storage Optimized 
    * Run EC2 Instances or Lambda Functions at the Edge 
- **Use Cases:** preprocess data, machine learnign, trasncoding media.




