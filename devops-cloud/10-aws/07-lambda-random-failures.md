## Lambda Function Fails Randomly

### Question

Lambda Function fails randomly. How will you fix the issue?

### Short explanation of the question

This question tests your troubleshooting approach for intermittent
Lambda failures.

### Answer

I begin by identifying whether failures are caused by application logic,
configuration, permissions, dependencies, or service limits.

### Detailed explanation

Investigation steps:

1.  Review CloudWatch Logs.
2.  Check CloudWatch Metrics:
    -   Errors
    -   Duration
    -   Throttles
    -   Invocations
3.  Verify timeout configuration.
4.  Check memory allocation.
5.  Verify IAM permissions.
6.  Check downstream services (RDS, DynamoDB, S3, APIs).
7.  Review concurrency limits.

Typical causes:

-   Timeout
-   Out of memory
-   Throttling
-   Permission denied
-   Dependency failures
-   Cold starts

### Typical interview answer

> I first inspect CloudWatch Logs and Lambda metrics, then verify
> timeout, memory, IAM permissions, downstream dependencies, and
> concurrency settings. After identifying the root cause, I adjust the
> configuration or application code and monitor the function after
> deployment.

### Key takeaways

-   CloudWatch Logs are the first place to investigate.
-   Timeout, memory, and concurrency are common causes.
-   Always verify downstream service health.
