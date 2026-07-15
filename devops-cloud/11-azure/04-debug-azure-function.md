## Debugging a Failed Azure Function

### Question

Azure Function failed to execute. How do you debug?

### Short explanation of the question

This tests your approach to diagnosing Azure Functions.

### Answer

Review Function logs, Application Insights, execution metrics, triggers,
configuration, permissions, and dependencies.

### Detailed explanation

Steps: 1. Check Function Monitor. 2. Review Application Insights. 3.
Validate trigger configuration. 4. Check environment variables. 5.
Verify Managed Identity or Service Principal permissions. 6. Test
locally if needed.

### Typical interview answer

> I use Function Monitor and Application Insights to identify failures,
> validate trigger configuration, permissions, timeout, and
> dependencies, then redeploy and monitor after fixing the issue.

### Key takeaways

-   Application Insights is essential.
-   Validate triggers and permissions.
