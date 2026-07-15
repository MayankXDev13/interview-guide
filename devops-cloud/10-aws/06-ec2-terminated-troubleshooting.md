## EC2 Instance Terminated Unexpectedly

### Question

EC2 Instance terminated unexpectedly. How will you troubleshoot?

### Short explanation of the question

This question evaluates your ability to investigate unexpected EC2
termination.

### Answer

I investigate in a structured order: 1. Check EC2 State Transition
Reason. 2. Review CloudTrail events. 3. Check Auto Scaling activity. 4.
Review AWS Health Dashboard. 5. Check CloudWatch metrics and logs. 6.
Verify Spot Instance interruption or lifecycle policies.

### Detailed explanation

Useful commands and services:

``` bash
aws ec2 describe-instances
```

Check: - CloudTrail (TerminateInstances API) - Auto Scaling Activity
History - Spot interruption events - IAM permissions - CloudWatch
alarms - AWS Health events

### Typical interview answer

> I first determine whether the instance was manually terminated,
> terminated by Auto Scaling, Spot interruption, or AWS. I use
> CloudTrail, Auto Scaling activity, CloudWatch, and EC2 events to
> identify the root cause before restoring the workload.

### Key takeaways

-   CloudTrail identifies who terminated the instance.
-   Auto Scaling may intentionally replace unhealthy instances.
-   CloudWatch and AWS Health provide supporting evidence.
