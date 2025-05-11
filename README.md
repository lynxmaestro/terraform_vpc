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

If you need to download terraform (Manually), then click here 
