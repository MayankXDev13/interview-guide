## East US VM Slow for Europe Users

### Question

A VM-based application in East US is slow for users in Europe. What do
you do?

### Short explanation

Tests latency optimization.

### Answer

Deploy the application closer to users, use Front Door/Traffic Manager,
CDN and database replication.

### Typical interview answer

> I deploy a European instance and route users through Azure Front Door
> to reduce latency.

### Key takeaways

-   Deploy near users.
-   Use global routing.
