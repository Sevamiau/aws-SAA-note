# IAM Password Policy

- Strong password = higher security
- In AWS you can set up a password policy:
  - Set a minimum password length
  - Require specific character types: uppercase letters, lowercase letters, numbers, non-alphanumeric characters
  - Allow all IAM users to change their own password
  - Require users to change their password after some time (password expiration)
  - Prevent password reuse

---

## Multi-Factor Authentication (MFA)

- Users have access to your account and can change configs or delete resources
- You want to protect your Root account and IAM users
- **MFA = password you know + security device you own**

## MFA Device Options in AWS

- **Virtual MFA device**: Google Authenticator or Authy — support multiple tokens on a single device
- **Universal 2nd Factor (U2F) security key** (YubiKey): supports multiple Root and IAM users with a single security key
- **Hardware Key Fob MFA device**: provided by Gemalto
