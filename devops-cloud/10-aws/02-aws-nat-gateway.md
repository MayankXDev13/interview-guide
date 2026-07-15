## AWS NAT Gateway and When It Is Used

### Question

What is AWS NAT and when is it used?

### Short explanation of the question

This question tests your understanding of how instances in private
subnets securely access the internet without becoming publicly
accessible.

### Answer

AWS **NAT (Network Address Translation) Gateway** enables resources in a
**private subnet** to initiate outbound internet connections while
preventing inbound internet connections.

### Detailed explanation of the answer for readers' understanding

Typical architecture:

``` text
Internet
    │
Internet Gateway
    │
Public Subnet
    │
NAT Gateway
    │
Private Subnet
    │
EC2 / ECS / EKS
```

When an EC2 instance in a private subnet needs to: - Download OS
updates - Pull Docker images - Access AWS APIs - Call external APIs

its traffic is routed to the NAT Gateway, which sends requests to the
internet and returns the responses.

### NAT Gateway vs NAT Instance

  Feature             NAT Gateway   NAT Instance
  ------------------- ------------- --------------
  Managed by AWS      Yes           No
  High Availability   Yes           Manual
  Scaling             Automatic     Manual
  Maintenance         None          Required

### Typical interview answer

> A NAT Gateway allows resources in a private subnet to access the
> internet for outbound traffic while blocking inbound internet access.
> It is commonly used by application servers in private subnets that
> need software updates or external API access.

### Best practices

-   Deploy one NAT Gateway per Availability Zone.
-   Place it in a public subnet.
-   Route private subnet traffic (0.0.0.0/0) to the NAT Gateway.

### Key takeaways

-   NAT Gateway provides outbound internet access.
-   It does not allow inbound internet traffic.
-   It is used by resources in private subnets.
