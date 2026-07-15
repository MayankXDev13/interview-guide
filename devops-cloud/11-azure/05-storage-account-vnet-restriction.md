## Restrict Azure Storage Account Access to a Specific VNet

### Question

How will you restrict access to a Storage Account so only VMs in a
specific VNet can access it?

### Short explanation of the question

This tests Azure networking and storage security.

### Answer

Use Storage Account Networking settings with Selected Networks, Service
Endpoints or Private Endpoints, and allow only the required subnet.

### Detailed explanation

Implementation: 1. Disable public access if appropriate. 2. Enable
Selected Networks. 3. Add the required VNet/Subnet. 4. Prefer Private
Endpoint for private connectivity. 5. Validate NSG and DNS
configuration.

Architecture:

``` text
VM
 │
VNet/Subnet
 │
Private Endpoint
 │
Storage Account
```

### Typical interview answer

> I secure the Storage Account using Private Endpoints or Service
> Endpoints, restrict access to the required subnet, and disable
> unnecessary public access.

### Key takeaways

-   Prefer Private Endpoints.
-   Restrict storage networking to trusted VNets.
