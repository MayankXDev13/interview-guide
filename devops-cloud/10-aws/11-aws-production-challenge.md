## AWS Production Challenge

### Question

Explain a recent challenge that you faced with AWS and how you solved
it.

### Short explanation of the question

Interviewers expect a real production troubleshooting example.

### Answer

One common example is an application becoming unavailable because EC2
instances failed health checks behind an Application Load Balancer.

### Detailed explanation

Investigation: 1. Checked CloudWatch metrics. 2. Reviewed ALB Target
Group health. 3. Verified Security Groups. 4. Examined application logs.
5. Restarted unhealthy instances. 6. Fixed application configuration. 7.
Verified Auto Scaling replaced unhealthy instances.

### Typical interview answer

> We observed failing ALB health checks. I used CloudWatch and Target
> Group health status to identify unhealthy instances, corrected the
> application configuration, verified the health checks passed, and
> monitored the environment until it stabilized.

### Key takeaways

-   Use CloudWatch and ALB health checks.
-   Verify Security Groups and application logs.
-   Validate recovery after the fix.
