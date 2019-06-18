# Workshop - Terraform <img src="images/terraform-logo.png" width="30px">

### What is Terraform?

  _"Terraform is a tool for building, changing and versioning infrastructure safely and efficiently."_

### Features

  - **Manages the infrastructure, period.**

    - It is not a configuration management tool

  - **Popular infrastructure providers**

    - AWS

    - DigitalOcean

    - GCE

    - Azure

  - **Enable Multiple Providers**

  - **Infrastructure as Code**

    - Configurations files (.tf)

  - **Execution Plans**

    - What Terraform will do

  - **Resource Graph**

    - Parallelizes the creation and modification of any non-dependent resources    

  - **Variables support**

    - Example:

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
#

  - **Conditional Support**

    - Example:

    ```
      resource "aws_eip" "instance_eip" {
        count                     = "${var.attach_eip ? 1 : 0}"
        vpc                       = true
        instance                  = "${element(aws_instance.ec2_generic_instance.*.id,count.index)}"
        associate_with_private_ip = "${element(aws_instance.ec2_generic_instance.*.private_ip,count.index)}"
      }
    ```
#

  - **Many Built-in Functions**

    - [Interpolation Syntax](https://www.terraform.io/docs/configuration-0-11/interpolation.html)

    - Example:

    ```
      resource "aws_subnet" "public_subnet" {
        vpc_id                  = "${aws_vpc.vpc.id}"
        count                   = "${var.subnet_count}"
        cidr_block              = "${cidrsubnet(var.cidr_vpc, var.cidr_network_bits, (count.index + length(split(",", lookup(var.azs, var.region)))))}"
        availability_zone       = "${element(data.aws_availability_zones.all.names, count.index)}"
        map_public_ip_on_launch = true

        tags {
          Name = "public-${element(data.aws_availability_zones.all.names, count.index)}-subnet"
        }
      }
    ```
#

  - **External Datasources Support**

    - Example:

    ```
      data "terraform_remote_state" "shared" {
        backend = "s3"
        config {
          bucket = "globo-tf"
          key    = "network/vpc"
          region = "us-east-1"
        }
      }

      resource "aws_instance" "ec2_instance" {
        vpc_id                  = "${data.terraform_remote_state.shared.vpc_id}"
        key_pair                = "${data.terraform_remote_state.shared.key_name}"
        subnet_id               = "${data.terraform_remote_state.shared.public_subnets, 0}"
      }
    ```

#

### Workflow

  - **Step 1 - Create Configuration**

    `$ vim main.tf`

  - **Step 2 - Check the execution plan**

    `$ terraform plan`

  - **Step 3 - Build the Infrastructure**

    `$ terraform apply`

  - **Step X - Deploy the Infrastructure**

    `$ terraform plan --destroy`
    `$ terraform destroy # It will ask you, unless --force`

#

### Examples

  - **1. A simple infrastructure**

    - _1.1 Build a simple infrastructure:_

      ```
        resource "aws_instance" "example" {
          ami             = "ami-6edd3078"
          instance_type   = "t2.micro"

          tags {
              Name = "Test Machine"
          }
        }
      ```

    - _1.2. Improve It:_

      ```
        resource "aws_security_group" "ssh" {
          name = "allow_ssh"
          description = "Allow SSH connections"

          ingress {
            from_port = 22
            to_port = 22
            protocol = "tcp"
            cidr_blocks = ["0.0.0.0/0"]
          }
        }

        resource "aws_instance" "example" {
          ...
          vpc_security_group_ids = ["${aws_security_group.ssh.id}"]
        }
      ```

  - **2.1. Isolating Parts**

    - When invoking any command that loads the Terraform configuration, Terraform loads all configuration files within the directory specified in alphabetical order.

      ```
        - main.tf
        |
        - security_group.tf
      ```    

    - security_group.tf:

      ```
        resource "aws_security_group" "ssh" {
          name = "allow_ssh"
          description = "Allow SSH connections"

          ingress {
            from_port = 22
            to_port = 22
            protocol = "tcp"
            cidr_blocks = ["0.0.0.0/0"]
          }
        }
      ```

    - main.tf:

      ```
        resource "aws_instance" "example" {
          ...
          vpc_security_group_ids = ["${aws_security_group.ssh.id}"]
        }
      ```  

  - **3.1. Isolating components (A.K.A Modules)**

    ```
      - main.tf
      |
      - security_group
        |
        - main.tf
        |
        - outputs.tf
    ```      
