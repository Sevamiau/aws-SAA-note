# EBS Snapshot Features

-EBS Snapshot Archive:
    .Move a snapshot to an 'archive tier' that is 75% cheaper
    .Takes within 24 to 72 hours for restoring the archive

-Recycle Bin for EBS Snapshots 
    .Setup rules to retain deleted Snapshots so you can recover them after an accidental deletion
    .You can specify retention (from 1 day to 1 year)

-Fast Snapshot Restore (FSR)
    .Force full initialization of snapshots to have no latency on the first use (very expensive)
