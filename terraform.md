# Workshop - Terraform <img src="images/terraform-logo.png" width="40px">

### Features

  - Variables support

  ```
    variable "application_name" {
      description = "Nome da Aplicação"
      default     = "Example"
    }

    variable "azs" {
      description = "Availability Zones"
      type        = "list"
      default     = ["sa-east-1a", "sa-east-1c"]
    }

    variable "vpc_name" {
      description = "Nome da VPC"
      type        = "map"
      default     = { Name = "Example.com" }
    }
  ```

  ```
    resource "aws_instance" "ec2_generic_instance" {
      ami             = ${var.ami}

      tags {
        Environment = "${var.environment}"
        Application = "${var.application_name}"
      }
    }
  ```  
