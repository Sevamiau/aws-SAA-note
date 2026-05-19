# IAM: Users & Groups

- IAM = Identity and Access Management, **global service**
- IAM is global — you cannot choose a region for it
- **Root account**: created by default, should not be used or shared
- **Users**: people within your organization, can be grouped
- **Groups**: contain users only — groups cannot contain other groups
- Users don't have to belong to a group, and users can belong to multiple groups

---

## IAM Permissions

- Users or groups can be assigned JSON documents called **policies**
- These policies define the **permissions** of the users
- In AWS apply the **least privilege principle**: don't give more permissions than a user needs
