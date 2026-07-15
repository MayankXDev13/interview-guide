## Using NSG and ASG in Real Time

### Question

Explain how you used NSG and ASG in real time.

### Short explanation

Tests practical Azure networking.

### Answer

NSGs control inbound/outbound traffic while ASGs logically group VMs so
common NSG rules can be applied.

### Typical interview answer

> We grouped web and application VMs into separate ASGs and applied NSG
> rules between them instead of managing individual IP addresses.

### Key takeaways

-   NSG controls traffic.
-   ASG simplifies rule management.
