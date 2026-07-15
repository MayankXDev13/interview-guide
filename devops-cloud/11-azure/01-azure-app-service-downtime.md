## Troubleshooting Random Downtime in Azure App Service

### Question

User reports random downtime in a Web App hosted on Azure App Services.
How will you troubleshoot?

### Short explanation of the question

This tests your production troubleshooting methodology for Azure App
Service.

### Answer

I verify Azure Service Health, inspect Application Insights and App
Service metrics, review deployment history, diagnose scaling issues,
check dependencies, and identify the root cause before applying a fix.

### Detailed explanation

Workflow: 1. Check Azure Service Health. 2. Review App Service Metrics
(CPU, Memory, Requests, HTTP 5xx). 3. Review Application Insights. 4.
Check deployment logs. 5. Verify autoscale rules. 6. Check backend
dependencies (SQL, Storage, APIs).

### Typical interview answer

> I start with Azure Monitor and Application Insights to identify
> whether downtime is caused by the application, platform, or
> dependencies. I then review deployments, scaling, and logs before
> implementing the appropriate fix.

### Key takeaways

-   Azure Monitor and Application Insights are primary tools.
-   Always validate dependencies and scaling.
