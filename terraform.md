# Workshop - Terraform <img src="images/terraform-logo.png" width="30px">

### Features

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
