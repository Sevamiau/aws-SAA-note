# Amazon S3 — Versioning

- Versioning is enabled at the **bucket level**
- Each time you upload an object with the same key, S3 stores it as a new version (1, 2, 3…)
- Best practice: enable versioning on all important buckets

## Benefits

- **Protect against accidental deletes** — deleted objects become a delete marker; prior versions are preserved and restorable
- **Easy rollback** — restore any previous version of an object at any time

## Important Behavior

| Scenario | Behavior |
|---|---|
| File uploaded before versioning was enabled | Gets version ID **`null`** |
| Suspending versioning | Does **not** delete existing versions — they are kept |
| Deleting a versioned object | Creates a **delete marker**; the object is not permanently removed |
| Permanently deleting a version | Must explicitly delete the specific version ID |

## SAA-C03 Exam Tips

- Versioning must be enabled to use **S3 Replication** or **MFA Delete**
- Once enabled, versioning can only be **suspended**, not fully disabled
- "Null" version ID = object existed before versioning was turned on
- Delete markers are themselves versioned objects — they can be removed to restore a file
