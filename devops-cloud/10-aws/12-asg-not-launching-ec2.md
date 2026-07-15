## Auto Scaling Group Not Launching EC2

### Question

Auto Scaling Group is not launching EC2 instances. What can be the
issue?

### Short explanation of the question

This question tests your troubleshooting approach for Auto Scaling
failures.

### Answer

Possible causes include: - Invalid Launch Template - Capacity shortage -
IAM permission issues - Incorrect subnet configuration - Instance quota
exceeded - AMI no longer available - Security Group or networking issues

### Detailed explanation

Check: 1. Auto Scaling Activity History. 2. Launch Template. 3. EC2
service quotas. 4. Target subnets. 5. IAM role. 6. CloudTrail. 7.
CloudWatch Events.

### Typical interview answer

> I first review Auto Scaling Activity History because it usually
> explains why instances failed to launch. Then I verify the Launch
> Template, IAM role, subnet capacity, quotas, and AMI before testing
> again.

### Key takeaways

-   Activity History is the best starting point.
-   Launch Template errors are common.
-   Verify quotas and networking.
