## AWS EFS Experience

### Question

Have you used AWS EFS? If yes, what issues did you run into?

### Short explanation of the question

Tests practical experience with shared file storage.

### Answer

Yes. Common issues include high latency for small-file workloads,
incorrect mount targets, security group misconfiguration, throughput
limits, and NFS mount failures.

### Detailed explanation

Troubleshooting: - Verify mount targets in every AZ. - Check NFS port
2049. - Review throughput mode. - Monitor CloudWatch metrics.

### Typical interview answer

> I used EFS for shared storage across multiple EC2/EKS nodes. Issues
> included mount failures due to Security Groups and throughput
> bottlenecks, which were resolved by correcting networking and
> throughput configuration.

### Key takeaways

-   EFS is shared storage.
-   Verify networking and throughput.
