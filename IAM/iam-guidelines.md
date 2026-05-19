# IAM Guidelines & Best Practices

- Don't use the root account except for AWS account setup
- One physical user = One AWS user
- Assign users to groups and assign permissions to groups
- Create a strong password policy
- Use and enforce Multi-Factor Authentication (MFA)
- Use access keys for programmatic access (CLI/SDK)
- Audit permissions of your account using **IAM Credentials Report** & **IAM Access Advisor**
- **Never share** IAM users or access keys
