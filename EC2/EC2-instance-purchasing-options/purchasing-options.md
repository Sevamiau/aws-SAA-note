# EC2 Instance Purchasing Options

| Option | Commitment | Discount | Use when |
|---|---|---|---|
| On-Demand | None | None | Short-term, unpredictable workload |
| Reserved | 1 or 3 years | Up to 72% | Steady-state app (e.g. database always running) |
| Savings Plans | 1 or 3 years | Up to 72% | Same as Reserved but more flexible (any instance size/OS) |
| Spot | None | Up to 90% | Fault-tolerant batch jobs, can be interrupted |
| Dedicated Host | On-demand or 1/3 yr | - | Compliance needs or BYOL (bring your own license) |
| Dedicated Instance | None | - | Need hardware isolation but don't need full host control |
| Capacity Reservation | None | None | Need guaranteed capacity in a specific AZ |

---

## On-Demand

- Pay for what you use
  - Linux/Windows: billing per second after the first minute
  - Other OS: billing per hour
- Highest cost, no upfront payment, no commitment
- Use for short-term or unpredictable workloads

## Reserved Instances

- Up to 72% discount vs On-Demand
- Reserve specific instance attributes (type, region, OS, tenancy)
- Term: 1 year or 3 years
- Payment: no upfront / partial upfront / all upfront (more upfront = more discount)
- Scope: Regional or Zonal (zonal also reserves capacity in that AZ)
- You can buy and sell Reserved Instances in the Marketplace

**Convertible Reserved Instance**: can change instance type, family, OS, scope, tenancy — up to 66% discount

**Exam trap**: Reserved = commit to a specific instance type. Savings Plans = commit to a dollar amount per hour, more flexible.

## Savings Plans

- Commit to a dollar amount per hour (e.g. $10/hr) for 1 or 3 years
- Same 72% discount as Reserved
- Flexible across instance size, OS, and tenancy within the committed family and region
- Usage beyond the commitment is billed at On-Demand rates

## Spot Instances

- Up to 90% discount — cheapest option
- AWS can reclaim the instance with 2-minute warning if spot price exceeds your max bid
- **Not for**: databases, critical jobs, anything stateful
- **Good for**: batch processing, data analysis, image processing, distributed/fault-tolerant workloads

## Dedicated Hosts

- Full physical server reserved for you
- Lets you use existing per-socket/per-core software licenses (BYOL)
- Most expensive option
- Required for strong compliance or regulatory needs

## Dedicated Instances

- Instances run on hardware dedicated to your account
- May share hardware with other instances in the same account
- No control over placement — differs from Dedicated Host

**Dedicated Host vs Dedicated Instance**: Host gives you visibility and control over the physical server (needed for BYOL). Instance just guarantees no other AWS customer shares your hardware.

## Capacity Reservations

- Reserve On-Demand capacity in a specific AZ for any duration
- No time commitment, no billing discount
- You pay the On-Demand rate whether you use the capacity or not
- Combine with Reserved Instances or Savings Plans for discounts
- Use when you need guaranteed capacity available in a specific AZ for a short-term critical event
