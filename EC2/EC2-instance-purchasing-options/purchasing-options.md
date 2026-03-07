# EC2 instances purchasing options

- On-demand instances: Short workload, predictable pricing, pay by second
- Reserved: (1, 3 years)
    .Reserved instances-long workloads
    .Convertible Reserved instances-long workloads with flexible instances
-Saving Plans (1, 3 years): Commitment to an amount of usage, long workload
-Spot instances: Short workloads, cheap, can lose instances(less reliable)
-Dedicated Hosts: book an entire physical server, control instance placement
-Dedicated instances: No other customers will share your hardware
-Capacity reservations: reserve capacity in a specific AZ for any duration

# EC2 On-demand

-Pay for what you use:    
    .Linux or win: billing per second, after the first minute
    .All other operating systems: billing per hour
-Has the highest cost but no upfront payment
-No long-term Commitment

-Recommended for short-term and un-interrupted workloads where you cant predcit how the app will behave

# EC2 Reserved instances

-Up to 72% discount compared to On-demand
-You Reserve a specific instance attributes (instance type, tenancy, OS)
-Reservation period: 1 year(+discount) or 3 years(+++discount)
-payment options: no upfront(+), partial upfront(++), all upfront(+++)
-Reserved instance scope-Regional or Zonal(reserve capacity in an AZ)
-Recommended for steady-state usage apps(Thing database)
-You can buy and sell in the Reserved instance Marketplace

-Convertible Reserved instance
    .Can change the EC2 instance type, instance family, OS, scope and tenancy.
    .Up to %66 discount

# EC2 Saving Plans

-Get a discount base on long-term usage (up to 72%0 sane as RI)
-Commit to a certain type of usage ($10/hour for 1 or 3 years)
-Use beyond EC2 Saving Plans is billed at the On-demand price 

-Locked to a specific instance family & AWS region (eg. M5 in us-east-1)
-flexible across:
    .Instance size(eg. m5.xlarge, m5.2xlarge)
    .OS(eg. linux or win)
    .Tenancy(Host, Dedicated, Default)

# EC2 Spot Instances

-Can get a discount of up to 90% compared to On-demand
-Instances that you can 'loose' at any point of time if tour mas price is less than the current spot price
-The MOST cost-efficient instances in AWS

-Useful for workloads that are resilient to failure:
    .Batch jobs
    .Data analysis
    .Image processing
    .Any distributed workloads
    .workloads with a flexible start and end time

NOT SUITED FOR CRITICAL JOBS OR DATABASES

# EC2 Dedicated Hosts

-A physical server with EC2 instance capacity fully Dedicated to your use
-Allows you address compliance requirements and use your existing server-bound software licenses(per-socket, per-core, per VM software licenses)
-purchasing options:
    .On-demand-pay per-second for active Dedicated Host
    .Reserved- 1 or 3 years(no upfront, partial upfront or all upfront)
-The most expensive option 

-Useful for software that have complicated licensing mode (BYOL- Bring your own license)
-Or for companies that have strong regulatory or compliances needs 

# EC2 Dedicated Instances

-Instances run on hardware that is dedicated to you
-May share hardware with other instances in same account
-No control over instance placement(can move hardware after stop/start)


# EC2 Capacity reservations

-Reserve On-demand instances capacity in a specific AZ for any duration
-You always have access to EC2 capacity when you need it 
-No time Commitment(create/cancel anytime), no billing discounts 
-Combine with regional reserved instances and saving plans to benefit from billing discounts 
-You are charged at On-demand rat whether you run instances or not

-Suitable for short-term un-interrupted workloads that needs to e in a specific AZ
