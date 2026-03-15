# RDS & Aurora Security

----------

- **At-test encryption**:
 * Database master & replicas encryption using AWS KMS (key management service) - must  be defined as launch time 
 * If the master is not encrypted the read replicas cannnot be encrypted
 * To encrypt an un-encrypted database go trough a DB snapshot and restore as encrypted

- **In-flight encryption**: TLS-ready by deafult. use the AWSTLS (transport layer security) riit certificates client-side
- **IAM Authentication**: IAM roles to connect to your database (instead of username/passwd)
- **Security Groups**: Control Network access to your RDS/Aurora DB  
- **No SSH Available**: Except on RDS Custom
- **Audit Logs can be enabled** and sent to CloudWatch Logs for longer retention 


----------

