## AWS RDS Storage is Full

### Question

What will you do when AWS RDS Storage is Full?

### Short explanation of the question

This tests your ability to troubleshoot database storage issues while
minimizing downtime.

### Answer

Check CloudWatch storage metrics, identify what's consuming space,
increase storage if needed, clean unnecessary data, enable storage
autoscaling, and monitor recovery.

### Detailed explanation

Steps: 1. Check `FreeStorageSpace` in CloudWatch. 2. Identify large
tables, logs, or temporary files. 3. Delete/archive unnecessary data. 4.
Increase allocated storage (online for most engines). 5. Enable Storage
Autoscaling. 6. Monitor performance after the change.

### Typical interview answer

> I first verify CloudWatch storage metrics, identify the storage
> consumer, clean unnecessary data if possible, then increase RDS
> storage or rely on Storage Autoscaling. Finally, I monitor database
> performance and configure alerts.

### Key takeaways

-   Monitor `FreeStorageSpace`.
-   Enable Storage Autoscaling.
-   Configure CloudWatch alarms.
