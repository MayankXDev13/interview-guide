## Difference Between Resource and Data Source in Terraform

### Question

What is the difference between Resource and Data Source in Terraform?

### Short explanation of the question

This question tests your understanding of two fundamental Terraform
concepts. A **Resource** is used to create or manage infrastructure,
while a **Data Source** is used to read information about infrastructure
that already exists.

### Answer

-   A **Resource** creates, updates, or deletes infrastructure managed
    by Terraform.
-   A **Data Source** only reads information from existing
    infrastructure and does not create or modify resources.

### Detailed explanation of the answer for readers' understanding

  -----------------------------------------------------------------------
  Aspect             Resource               Data Source
  ------------------ ---------------------- -----------------------------
  **Purpose**        Creates and manages    Reads existing infrastructure
                     infrastructure         

  **Creates          Yes                    No
  resources**                               

  **Updates          Yes                    No
  resources**                               

  **Deletes          Yes                    No
  resources**                               

  **Managed by       Yes                    No (read-only)
  Terraform**                               

  **Keyword**        `resource`             `data`
  -----------------------------------------------------------------------

------------------------------------------------------------------------

## Example 1 --- Resource

The following configuration creates a new Amazon S3 bucket.

``` hcl
provider "aws" {
  region = "ap-south-1"
}

resource "aws_s3_bucket" "logs" {
  bucket = "my-company-logs-12345"

  tags = {
    Name = "Logs Bucket"
  }
}
```

Terraform creates and manages this bucket throughout its lifecycle.

------------------------------------------------------------------------

## Example 2 --- Data Source

Suppose an Ubuntu AMI already exists in AWS. Instead of creating one,
Terraform can retrieve its details.

``` hcl
data "aws_ami" "ubuntu" {
  most_recent = true

  owners = ["099720109477"]

  filter {
    name   = "name"
    values = ["ubuntu/images/hvm-ssd/ubuntu-jammy-22.04-amd64-server-*"]
  }
}
```

The data source searches AWS and returns the latest matching AMI.

It can then be used in a resource:

``` hcl
resource "aws_instance" "web" {
  ami           = data.aws_ami.ubuntu.id
  instance_type = "t2.micro"
}
```

Here:

-   `data.aws_ami.ubuntu.id` retrieves the existing AMI ID.
-   Terraform creates only the EC2 instance.
-   The AMI itself is not managed by Terraform.

------------------------------------------------------------------------

## When should you use each?

### Use a Resource when:

-   Creating a new EC2 instance
-   Creating an S3 bucket
-   Creating a VPC
-   Creating an RDS database
-   Managing infrastructure lifecycle

### Use a Data Source when:

-   Looking up an existing AMI
-   Reading an existing VPC
-   Fetching an existing subnet
-   Using an existing Security Group
-   Referencing infrastructure created outside Terraform

------------------------------------------------------------------------

### Best practices

-   Use **Resources** for infrastructure Terraform should own and
    manage.
-   Use **Data Sources** to reference existing infrastructure.
-   Avoid recreating infrastructure that already exists when a data
    source can be used.

### Key takeaways

-   **Resource** → Creates and manages infrastructure.
-   **Data Source** → Reads existing infrastructure without modifying
    it.
-   Resources use the `resource` block, while Data Sources use the
    `data` block.
-   Data Sources are commonly used to integrate Terraform with existing
    cloud environments.