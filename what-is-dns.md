

----------

- **Domain Name System** which translates the human friendly hostnames into the machine IP adresses
- www.google.com => 172.217.18.36
- **DNS** is the backbone of the internet
- **DNS** uses hierarchical naming structure:
  * .com
  * example.com
  * www.example.com
  * api.example.com 

----------

## DNS terminologies 

- Domain Registrar: Amazon, Route 53, GoDaddy...
- DNS Records: A, AAAA, CANAME, NS ...
- Zone file: Contains DNS records 
- Name Server: Resolves DNS queries (authoritative or non-authoritatives)
- Top Level Domain (TLD): *.com, .us, .gov, .org* ...
- Second Level Domain (SLD): amazon.com, google.com ...


```
```
http://api.wwww.example.com.
│     │    │       │      │ └── last dot is Root
│     │    │       │      └── TLD
│     │    │       └── SLD
│     │    └── Sub Domain
│     └── FQDN (Fully Qualified Domain Name)
└── Protocol
```
```
