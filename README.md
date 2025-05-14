# Create a VPC Through Terraform 

## Description

Terraform is a tool for building infrastructure with various technologies including Amazon AWS, Microsoft Azure, Google Cloud, and vSphere.

Here is a simple document on how to use Terraform to build an AWS VPC along with private/public Subnet and Network Gateway's for the VPC. We will be making 1 VPC with 4 Subnets: 2 Private and 2 Public, 1 NAT Gateways, 1 Internet Gateway, and 2 Route Tables all the creation was automated with appending to your values.

## Features
- Fully Automated (included terraform installation)
- Easy to customise and use as the Terraform modules are created using variables,allowing the module to be customized without altering the module's own source code, and allowing modules to be shared between different configurations.
- Each subnet CIDR block created automatically using cidrsubnet Function (Automated)
- Project name is appended to the resources that are creating which will make easier to identify the resources.

## Prerequisites for this project
- Need a IAM user access with attached policies for the creation of VPC.
- Knowledge to the working principles of each AWS services especially VPC, EC2 and IP Subnetting.

## Used Languages
- Bash (scripting)
- Terraform (iaac)

## Terraform Installation and VPC creation code and explanation :

If you need to download terraform (Manually), then click here [Terraform](https://developer.hashicorp.com/terraform/tutorials/aws-get-started/install-cli?in=terraform%2Faws-get-started)

### Prerequisites
- Create an IAM user on your AWS console that have access to create the required resources.
- Create a dedicated directory where you can create terraform configuration files.

~~~
sample installation steps
~~~

~~~
wget https://releases.hashicorp.com/terraform/0.15.3/terraform_0.15.3_linux_amd64.zip
unzip terraform_0.15.3_linux_amd64.zip 
ls -l
-rwxr-xr-x 1 root root 79991413 May  6 18:03 terraform  <<=======
-rw-r--r-- 1 root root 32743141 May  6 18:50 terraform_0.15.3_linux_amd64.zip
mv terraform /usr/bin/
which terraform 
/usr/bin/terraform
~~~

### Create provider.tf file

First we need to install the aws provider by creating a file provider.tf, because terraform will only look for .tf extensions in the project directory.
~~~
provider "aws" {
  region     = var.region
  access_key = access_key
  secret_key = secret_access_key
}
~~~

![image](https://github.com/user-attachments/assets/feef8b11-98bd-42c6-96b4-6123ef16dd30)

~~~
terraform init command is used to install the corresponding provider on the project directory.
~~~
![image](https://github.com/user-attachments/assets/4c7784c3-9460-4d01-8125-0f5be6652fa7)

### Create a variables.tf file

![image](https://github.com/user-attachments/assets/7428dbaa-563e-414c-b863-2fa6bd60f740)
![image](https://github.com/user-attachments/assets/96bf03c4-117f-4091-a24d-fd71ff1f62e9)

### Lets start creating main.tf file with the details below.

> To create VPC.
~~~
resource "aws_vpc" "main" {
  cidr_block           = var.pro_cidr
  instance_tenancy     = "default"
  enable_dns_hostnames = true

  tags = {
    Name    = "${var.pro_name}-${var.pro_env}-vpc"
    Project = var.pro_name
    Env     = var.pro_env
  }
}
~~~

> To Gather all availability zone names and output the details 
~~~
data "aws_availability_zones" "available" {
  state = "available"
}

output "azs" {
  value = data.aws_availability_zones.available
}
~~~

> To create Internet Gateway for VPC
~~~
resource "aws_internet_gateway" "igw" {
  vpc_id = aws_vpc.main.id                                                                                                                                                                                                                                                                                                tags = {
    Name    = "${var.pro_name}-${var.pro_env}-igw"
    Project = var.pro_name
    Env     = var.pro_env                                                                                                                                     }
}     
~~~
