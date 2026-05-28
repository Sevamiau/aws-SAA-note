# IAM Policies Structure

- Policies are written in **JSON**
- Consist of:
  - `Version`: policy language version, always include `"2012-10-17"`
  - `Id`: identifier for the policy (optional), e.g. `"s3-Account-Permissions"`
  - `Statement`: one or more individual statements (required)

- Statements consist of:
  - `Sid`: identifier for the statement (optional)
  - `Effect`: whether the statement allows or denies access (`Allow` or `Deny`)
  - `Principal`: account/user/role to which this policy applies (optional)
  - `Action`: list of actions this policy allows or denies
  - `Resource`: list of resources the actions apply to
  - `Condition`: conditions for when this policy is in effect (optional)

---

## Example

```json
{
  "Version": "2012-10-17",
  "Id": "s3-Account-Permissions",
  "Statement": [
    {
      "Sid": "1",
      "Effect": "Allow",
      "Principal": {
        "AWS": ["arn:aws:iam::123456789012:root"]
      },
      "Action": [
        "s3:GetObject",
        "s3:PutObject"
      ],
      "Resource": ["arn:aws:s3:::mybucket/*"]
    }
  ]
}
```
