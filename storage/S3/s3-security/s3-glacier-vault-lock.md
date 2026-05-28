# Amazon S3 Glacier Vault Lock 

- Adopt WORM (Write Once Read Many) model 
- Create a Vault Lock Policy 
- Lock the policy for future edits (can no longer be changed or deleted)
- Helpful for compliance and data retention 

## Object Lock (versioning must be enabled)

- Adopt a WORM model too 
- Block an object version deletion for a specified amount of time 
- **Retention Mode - Compliance:**
    * Object versions can't be overwritten or deleted by any user, including the root user
    * Object retention modes can't be changed and retention periods can't be shortened 
    
- **Retention Mode - Governance:**
    * Most users can't overwrite or delete an object version or alter its lock settings
    * Some users have special permissions to change the retention or delete the object 

- **Retention Period:** Protect the object for a fixed period, it can be extended

- **Legal Hold:**
    * Protect the object indefinitely, independent from retention period 
    * Can be freely placed and removed using the s3:PutObjectLegalHold IAM permission
