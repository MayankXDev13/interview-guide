## Scheduling a Script to Run Every Day on Azure

### Question

How can you schedule a script to run every day on Azure?

### Short explanation of the question

This tests your knowledge of Azure automation services.

### Answer

Common options include Azure Automation Runbooks, Azure Functions with
Timer Trigger, Logic Apps, or scheduled pipelines.

### Detailed explanation

Recommended approach: - Create an Azure Automation Account. - Upload a
PowerShell or Python Runbook. - Create a daily schedule. - Link the
schedule to the Runbook.

Alternative: Azure Function with a CRON timer trigger.

### Typical interview answer

> For administrative automation I generally use Azure Automation
> Runbooks. For application workflows I use Azure Functions with Timer
> Triggers.

### Key takeaways

-   Automation Runbooks for operations.
-   Timer-triggered Functions for serverless tasks.
