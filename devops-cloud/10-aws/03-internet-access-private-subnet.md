## Enable Internet Access for an Application in a Private Subnet

### Question

How do you enable Internet access to an application deployed in a
private subnet?

### Short explanation of the question

Applications in private subnets cannot directly access the internet
because they have no route to an Internet Gateway. This question checks
whether you understand the correct networking design.

### Answer

Deploy a **NAT Gateway** in a **public subnet**, attach an **Internet
Gateway** to the VPC, and configure the private subnet's route table to
send outbound traffic through the NAT Gateway.

### Detailed explanation of the answer for readers' understanding

Architecture:

``` text
Internet
    │
Internet Gateway
    │
Public Subnet
    │
NAT Gateway
    │
Private Route Table
    │
Private Subnet
    │
Application (EC2/ECS/EKS)
```

Configuration steps:

1.  Attach an Internet Gateway to the VPC.
2.  Create a public subnet.
3.  Deploy a NAT Gateway with an Elastic IP in the public subnet.
4.  Update the private subnet route table:

``` text
Destination: 0.0.0.0/0
Target: NAT Gateway
```

5.  Ensure the application remains in the private subnet without a
    public IP.

### Typical interview answer

> I keep the application in a private subnet for security. To provide
> outbound internet access, I deploy a NAT Gateway in a public subnet,
> attach an Internet Gateway to the VPC, and configure the private
> subnet route table to send internet-bound traffic through the NAT
> Gateway.

### Best practices

-   Never assign public IPs to application servers in private subnets.
-   Use one NAT Gateway per AZ for high availability.
-   Restrict inbound access with Security Groups.

### Key takeaways

-   Private subnets cannot access the internet directly.
-   NAT Gateway enables secure outbound connectivity.
-   Internet Gateway is attached only to the VPC and used by the NAT
    Gateway.
