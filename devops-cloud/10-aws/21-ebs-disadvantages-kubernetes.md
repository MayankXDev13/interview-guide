## Disadvantages of Using EBS Volumes in Kubernetes

### Question

What are the disadvantages of using EBS volumes in Kubernetes?

### Short explanation of the question

This question evaluates your understanding of persistent storage in
Kubernetes on AWS.

### Answer

Amazon EBS provides high-performance block storage but has limitations
in Kubernetes because it is tied to a single Availability Zone and is
typically attached to only one node at a time.

### Detailed explanation

Common disadvantages: - AZ-specific storage. - Single-node attachment
for most volume types. - Pod rescheduling across AZs can fail. - Not
suitable for shared file access. - Snapshot restore takes time.

### Typical interview answer

> EBS is excellent for databases and single-node workloads, but it isn't
> ideal for shared storage or workloads that move across Availability
> Zones. For shared access, I prefer Amazon EFS.

### Key takeaways

-   Single-AZ.
-   Single-node attachment.
-   Use EFS for shared storage.
