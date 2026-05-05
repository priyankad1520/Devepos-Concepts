# Multiple Providers
Using multiple providers or multiple configurations of the same provider in one Terraform project
#### Types of Multi Provider
1. Different Providers: Use multiple clouds in one project (AWS + Azure + GCP) 
> Example: AWS → Create EC2, Azure → Create VM 
2. Same Provider (Multiple Regions / Accounts): Use same provider with different configurations 
> Example: AWS us-east-1 → Create EC2, AWS us-west-2 → Create EC2
#### Key Points
-	alias → Used to create multiple provider configurations 
-	provider = aws.west → Tells resource which provider to use 
-	Helps in multi-region, multi-account, multi-cloud setup
- Why We Use Multi Provider: Deploy app in multiple regions, Disaster recovery setup, Multi-cloud architecture, Separate dev, test, prod environments
#### Simple Flow: Define multiple providers → Assign provider → Create resources in different environments
 
You can use multiple providers in one single terraform project. For example,


1. Create a providers.tf file in the root directory of your Terraform project.
2. In the providers.tf file, define the AWS and Azure providers. For example:


```
provider "aws" {   # Configure AWS provider
  region = "us-east-1"   # Set AWS region where resources will be created
}

provider "azurerm" {   # Configure Azure provider
  subscription_id = "your-azure-subscription-id"   # Identify Azure subscription
  client_id = "your-azure-client-id"   # Authenticate using Azure application ID
  client_secret = "your-azure-client-secret"   # Secure password for authentication
  tenant_id = "your-azure-tenant-id"   # Specify Azure Active Directory tenant
}
```

3. In your other Terraform configuration files, you can then use the aws and azurerm providers to create resources in AWS and Azure, respectively,

```
resource "aws_instance" "example" {   # Create EC2 instance in AWS
  ami = "ami-0123456789abcdef0"   # Define OS image for AWS instance
  instance_type = "t2.micro"   # Define instance size (CPU & RAM)
}
resource "azurerm_virtual_machine" "example" {   # Create Virtual Machine in Azure
  name = "example-vm"   # Set name for Azure VM
  location = "eastus"   # Define Azure region
  size = "Standard_A1"   # Define VM size in Azure
}
```
#### Simple Understanding
-	Define multiple providers → AWS + Azure 
-	Use AWS provider → Create EC2 
-	Use Azure provider → Create VM 
-	One Terraform project → Manage multi-cloud


