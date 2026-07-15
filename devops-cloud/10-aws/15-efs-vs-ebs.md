## When to Use EFS Instead of EBS

### Question

When will you use EFS over EBS in real time?

### Short explanation of the question

This evaluates storage selection.

### Answer

Use EFS when multiple EC2 instances or Kubernetes pods require shared,
concurrent file access. Use EBS when storage is attached to a single
instance and low latency is required.

### Detailed explanation

  EFS        EBS
  ---------- -----------------
  Shared     Single instance
  NFS        Block storage
  Multi-AZ   AZ specific
  Scalable   Fixed volume

### Typical interview answer

> I choose EFS for shared storage and EBS for high-performance block
> storage attached to one instance.

### Key takeaways

-   Shared storage → EFS.
-   Single-instance block storage → EBS.
