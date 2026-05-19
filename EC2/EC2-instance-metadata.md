# EC2 Instance Metadata Service (IMDS)

- Allows EC2 instances to learn about themselves without using an IAM role
- URL: `http://169.254.169.254/latest/meta-data/`
- This is a **link-local address** — only accessible from within the instance itself

## What you can retrieve

- Instance ID, type, AMI ID
- Public and private IP addresses
- IAM role name (but **not** the IAM policy)
- Temporary IAM credentials (if a role is attached)
- Security groups, hostname, availability zone

```bash
# Example — get instance public IP from inside the instance
curl http://169.254.169.254/latest/meta-data/public-ipv4

# Get IAM role credentials
curl http://169.254.169.254/latest/meta-data/iam/security-credentials/<role-name>
```

---

## IMDSv1 vs IMDSv2

| | IMDSv1 | IMDSv2 |
|---|---|---|
| How it works | Simple GET request | Session-oriented (PUT first to get token, then use token) |
| Security | Vulnerable to SSRF attacks | Protected against SSRF |
| AWS recommendation | Legacy | **Use IMDSv2** |

### IMDSv2 flow
```bash
# Step 1 — get a session token (valid up to 6 hours)
TOKEN=$(curl -X PUT "http://169.254.169.254/latest/api/token" \
  -H "X-aws-ec2-metadata-token-ttl-seconds: 21600")

# Step 2 — use the token in requests
curl -H "X-aws-ec2-metadata-token: $TOKEN" \
  http://169.254.169.254/latest/meta-data/public-ipv4
```

---

## Exam tips

- If an exam question mentions **SSRF vulnerability** on EC2 → answer involves enforcing **IMDSv2**
- You can disable IMDSv1 at the instance level or enforce IMDSv2 across an account via SCP
- IMDS is not the same as **user data** (`/latest/user-data`) — user data is the bootstrap script, metadata is instance info
