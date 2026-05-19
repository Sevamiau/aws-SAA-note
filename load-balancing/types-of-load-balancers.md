# Types of Load Balancers on AWS

AWS has 4 managed load balancers. Always use the newer generation.

## Quick decision table

| Load Balancer | Layer | Protocol | Pick this when |
|---|---|---|---|
| ALB (v2, 2016) | 7 (HTTP) | HTTP, HTTPS, WebSocket | Web apps, microservices, routing by path/host/headers |
| NLB (v2, 2017) | 4 (TCP) | TCP, TLS, UDP | Ultra-low latency, static IP needed, non-HTTP traffic |
| GLB (2020) | 3 (Network) | IP | Routing traffic through 3rd-party security appliances (firewalls, IDS) |
| CLB (v1, 2009) | 4 + 7 | HTTP, HTTPS, TCP, SSL | Legacy only — do not use for new architectures |

---

## ALB — Application Load Balancer

- Routes based on content: path (`/api`, `/images`), hostname, query strings, headers
- Great for microservices and containers (ECS)
- Has a fixed DNS name (not a static IP)
- Supports authentication via Cognito or OIDC

## NLB — Network Load Balancer

- Handles millions of requests per second with very low latency
- Has a **static IP per AZ** — useful when clients need to whitelist a fixed IP
- Supports TCP, UDP, TLS
- Use when ALB is too slow or you need a static IP

## GLB — Gateway Load Balancer

- Deploys, scales, and manages 3rd-party network appliances (e.g. Palo Alto, Fortinet firewalls)
- All traffic passes through the appliance before reaching your app
- Uses GENEVE protocol on port 6081

---

## Exam traps

- "Static IP for a load balancer" → NLB (ALB does not have a static IP)
- "Route based on URL path" → ALB
- "Inspect traffic with a firewall appliance" → GLB
- "WebSocket support" → ALB
- "UDP load balancing" → NLB
