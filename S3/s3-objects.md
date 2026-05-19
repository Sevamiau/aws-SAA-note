# S3 objects

- Objects (files) have a key
- The key is the full path:
  * s3://my-bucket/my_file.txt ---- ***my_file.txt is the key***
  * S3://my-bucket/my_folder1/another_folder/my_file.txt ***my_folder1/another_folder/my_file.txt***

- the key is composed of prefix + object name
  * s3://my-bucket/my_folder1/another_folder/my_file.txt

- theres no concept of 'directories' within buckets (although the UI will trick you to think otherwise)
- just keys with very long names that contain slashes


- Object values are the content of the body:
  * Max object size is 5TB
  * If uploading more than 5GB, must use **multi-part upload**

- Metadata (list of text key/value pairs — system or user metadata)
- Tags (unicode key/value pair — up to 10) — useful for security/lifecycle
- Version  ID (if versioning is enabled)
