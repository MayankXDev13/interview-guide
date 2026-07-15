## Write Terraform Code to Create an AWS Resource

### Question

Write Terraform code to create any resource on AWS.

### Short explanation of the question

This question evaluates your understanding of Terraform syntax and your
ability to define AWS infrastructure using Infrastructure as Code (IaC).
Interviewers typically expect you to write a basic resource such as an
EC2 instance, an S3 bucket, or a VPC.

### Answer

Terraform creates AWS resources using the `resource` block. Before
defining resources, you configure the AWS provider, then declare the
resource with the required arguments.

### Detailed explanation of the answer for readers' understanding

A Terraform configuration generally consists of:

1.  Provider configuration
2.  Resource definition
3.  Variables (optional)
4.  Outputs (optional)

------------------------------------------------------------------------

## Example --- Create an EC2 Instance

``` hcl
terraform {
  required_providers {
    aws = {
      source  = "hashicorp/aws"
      version = "~> 6.0"
    }
  }
}

provider "aws" {
  region = "ap-south-1"
}

resource "aws_instance" "web_server" {
  ami           = "ami-0123456789abcdef0"
  instance_type = "t2.micro"

  tags = {
    Name = "Interview-EC2"
    Environment = "Dev"
  }
}
```

------------------------------------------------------------------------

### Understanding the code

  Block                       Purpose
  --------------------------- ----------------------------------------------
  `terraform`                 Specifies the required provider and version.
  `provider "aws"`            Configures the AWS region.
  `resource "aws_instance"`   Creates an EC2 instance.
  `ami`                       Specifies the Amazon Machine Image.
  `instance_type`             Defines the EC2 instance size.
  `tags`                      Assigns metadata to the resource.

------------------------------------------------------------------------

### Terraform workflow

After writing the configuration, run:

``` bash
terraform init
```

Initializes the working directory and downloads the AWS provider.

``` bash
terraform plan
```

Shows what Terraform will create or modify.

``` bash
terraform apply
```

Creates the EC2 instance after confirmation.

``` bash
terraform destroy
```

Deletes the resources managed by Terraform.

------------------------------------------------------------------------

## Example --- Create an S3 Bucket

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

This configuration creates an Amazon S3 bucket.

------------------------------------------------------------------------

### Best practices

-   Use variables instead of hardcoding values such as regions and AMI
    IDs.
-   Store sensitive information outside the Terraform code.
-   Use remote state for production deployments.
-   Organize reusable infrastructure using modules.
-   Apply tags consistently to all resources.

### Key takeaways

-   Terraform creates AWS resources using the `resource` block.
-   Every configuration begins with a provider configuration.
-   Common commands are `terraform init`, `terraform plan`,
    `terraform apply`, and `terraform destroy`.
-   Writing reusable, parameterized configurations is considered a best
    practice.