# Amazon S3 — Objects

## Keys

- Every object has a **key** — the full path to the object within the bucket
- Examples:
  - `s3://my-bucket/my_file.txt` → key is `my_file.txt`
  - `s3://my-bucket/my_folder1/another_folder/my_file.txt` → key is `my_folder1/another_folder/my_file.txt`
- The key is composed of a **prefix** + **object name**
- There are no real directories — just keys with slashes in their names (the UI makes it look like folders)

## Object Properties

| Property | Details |
|---|---|
| **Value** | The actual file content (the body) |
| **Max size** | 5 TB per object |
| **Multi-part upload** | Required for files > 5 GB |
| **Metadata** | List of text key/value pairs — system or user-defined |
| **Tags** | Unicode key/value pairs, up to 10 — useful for security/lifecycle rules |
| **Version ID** | Assigned when versioning is enabled on the bucket |

## SAA-C03 Exam Tips

- S3 is **object storage**, not block storage — you cannot mount it like a disk
- For files > 5 GB, **multi-part upload** is mandatory (not just recommended)
- "Directories" in S3 are an illusion — the key `/folder/file.txt` is just a long key name
