## Cannot SSH or RDP to an Azure VM

### Question

Cannot SSH or RDP to an Azure VM. How will you fix it?

### Short explanation of the question

This evaluates VM connectivity troubleshooting skills.

### Answer

Check VM status, NSGs, Public IP, Azure Bastion, firewall rules, route
tables, credentials, and boot diagnostics.

### Detailed explanation

Checklist: 1. Verify VM is running. 2. Confirm Public IP/Bastion. 3.
Check NSG allows TCP 22 or 3389. 4. Verify guest firewall. 5. Review
Boot Diagnostics. 6. Use Serial Console if needed.

### Typical interview answer

> I first verify the VM is running, then check NSG rules, public
> connectivity, guest firewall, boot diagnostics, and credentials before
> using Azure Bastion or the Serial Console for recovery.

### Key takeaways

-   NSGs are a common cause.
-   Boot Diagnostics help identify startup failures.
