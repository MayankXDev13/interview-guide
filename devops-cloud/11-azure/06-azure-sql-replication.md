## Azure SQL Replication to Staging

### Question

Your team wants to replicate a production SQL database to staging daily.
What's your approach?

### Short explanation of the question

This tests Azure SQL backup and restore strategies.

### Answer

Use Azure SQL automated backups with point-in-time restore, Azure Data
Factory, or database copy depending on the requirement.

### Detailed explanation

A common approach is an Azure Automation Runbook or Azure Data Factory
pipeline that restores the latest backup into the staging database every
day.

### Typical interview answer

> I automate a daily restore of the production backup into the staging
> database using Azure Automation or Azure Data Factory while masking
> sensitive data if required.

### Key takeaways

-   Automate restores.
-   Protect production data.
