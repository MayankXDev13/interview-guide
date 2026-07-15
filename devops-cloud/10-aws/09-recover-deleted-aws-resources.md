## Developer Deleted Critical AWS Resources

### Question

Developer deleted critical resources like S3, RDS and EC2. What will you
do?

### Short explanation of the question

Interviewers want to evaluate your disaster recovery process.

### Answer

Determine what was deleted, identify who performed the action using
CloudTrail, recover resources from backups or versioning, and prevent
future incidents.

### Detailed explanation

Recovery options: - S3 → Versioning, Cross-Region Replication, Backup. -
RDS → Automated backups or snapshots. - EC2 → AMIs, EBS snapshots, Auto
Scaling.

Use CloudTrail to identify the delete operation and IAM policies to
prevent recurrence.

### Typical interview answer

> I first confirm the deletion using CloudTrail, recover resources from
> backups or snapshots, validate application functionality, and
> strengthen IAM permissions and backup policies.

### Key takeaways

-   CloudTrail identifies the deletion.
-   Backups are critical.
-   Least privilege reduces accidental deletion.
