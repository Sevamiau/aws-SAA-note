# AWS Regions & Availability Zones

## How to Choose an AWS Region

Things to consider:

1. **Compliance** with data governance and legal requirements — data never leaves a region without your explicit permission
2. **Proximity to customers** — reduced latency
3. **Available services** within a region — new services and features aren't available in every region
4. **Pricing** — varies region to region, transparent on the service pricing page

---

## AWS Availability Zones

- Each region has many availability zones (usually 3, min is 3, max is 6)
- Example: `ap-southeast-2a`, `ap-southeast-2b`, `ap-southeast-2c`
- Each AZ is one or more discrete data centers with redundant power, networking, and connectivity
- AZs are separate from each other so they are isolated from disasters
- AZs are connected with high-bandwidth, ultra-low latency networking
