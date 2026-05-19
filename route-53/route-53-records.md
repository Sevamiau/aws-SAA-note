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

----------

## Hosted Zones 

- A container for records that define how to route traffic to a domain and its subdomains 

- **Public Hosted Zones** - Contains records that specify how to route traffic on the internet (public domain names) *application1.mypublicdomain.com*
- **Private Hosted Zones** - Contain records that specify how you route traffic within one or more VPC's (private domain names)

- You pay $0.50 per month per hosted zone


