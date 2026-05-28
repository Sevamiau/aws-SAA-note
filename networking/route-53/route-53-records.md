# Route 53 - Records

----------

- How you want to route traffic for a domain
- Each record contains:
  * domian/subdomain name - e.g: example.com
  * Record type - e.g: A or AAAA
  * Value - e.g: 12.34.56.78
  * Routing policy - How route 53 responds to queries
  * TTL (time to live) - Amount of time the record cached at DNS resolvers

- Route 53 supports the following DNS record types:
  * (must know) A/ AAAA/ CNAME/ NS 
  * (advanced) CAA/ DS/ MX/ NATPTR/ PTR/ SOA/ TXT/ SPF/ resolvers

----------

## Record types (The ones we should know for the exam)

- **A** - Maps a hostname to IPv4
- **AAAA** - Maps a hostname to IPv6
- **CNAME** - Maps a hostname to another hostname
  * The target is a domain name which must have an A or AAAA record 
  * Cant create a CNAME record for the top node of a DNS namespace (zone apex)
  * Example: You cant create for example.com but you can create for www.example.com

- **NS** - Name Servers for the Hosted Zone

---

## Alias Records

- AWS-specific extension to DNS — not part of the standard DNS spec
- Maps a hostname to an **AWS resource** (ALB, CloudFront, S3 website endpoint, API Gateway, Elastic Beanstalk, VPC endpoints, Global Accelerator, another Route 53 record)
- Works like an A record but the target is an AWS resource, not a raw IP

### Alias vs CNAME

| | CNAME | Alias |
|---|---|---|
| Zone apex (`example.com`) | ❌ Not allowed | ✅ Allowed |
| Target | Any hostname | AWS resources only |
| Cost | Charged per query | **Free** |
| TTL | You set it | Managed by Route 53 |
| Health checks | No (indirectly) | Yes (for some targets) |

### Exam trap
- "How do you point `example.com` (root domain) to an ALB?" → **Alias record**, not CNAME
- You **cannot** set an Alias record for an EC2 DNS name — only the resource types listed above
- Alias records are always of type **A** or **AAAA** (not a separate record type)

---

## Hosted Zones 

- A container for records that define how to route traffic to a domain and its subdomains 

- **Public Hosted Zones** - Contains records that specify how to route traffic on the internet (public domain names) *application1.mypublicdomain.com*
- **Private Hosted Zones** - Contain records that specify how you route traffic within one or more VPC's (private domain names)

- You pay $0.50 per month per hosted zone


