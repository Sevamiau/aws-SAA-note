# EBS Encryption

 -When you create an encrypted EBS volume, you get the following:
    .Data at rest is encrypted inside the volume
    .All the data in flight moving between the instance and the volume is encrypted
    .All snapshots are encrypted
    .All volumes created from the snapshot are encrypted too 

-Encryption and decryption are handled transparently (you have nothing to do)
-Encryption has a minimal impact on latency
-EBS Encryption leverages keys from KMS (AES-256)
-Copying an unencrypted snapshot allows Encryption

## Encrypt an unencrypted EBS volume

-Create an EBS snapshot of the volume
-Encrypt the EBS snapshot (using copy)
-Create a new EBS volume from the snapshot (the volume will also be encrypted)
-Now you can attach the encrypted volume to the original instance 


