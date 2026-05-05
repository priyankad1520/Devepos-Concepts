# Provider Configuration
1. required_providers → Defines which provider + version Terraform should download. Install provider (what + version). required_providers is used to define provider source and version 

2. provider block → Defines how to use/configure the provider. Open app and set language/login. provider block is used to configure provider settings like region, credentials

- The required_providers block in Terraform is used to declare and specify the required provider configurations for your Terraform module or configuration. It allows you to specify the provider name, source, and version constraints.
#### Provider Configuration
```
terraform {   # Define global Terraform configuration block
  required_providers {   # Declare all required providers for this project
   
 aws = {   # Configure AWS provider
      source  = "hashicorp/aws"   # Download AWS provider from HashiCorp registry
      version = "~> 3.0"   # Use version >=3.0 and <4.0 (compatible versions)
    }

    azurerm = {   # Configure Azure provider
      source  = "hashicorp/azurerm"   # Download Azure provider from HashiCorp registry
      version = ">= 2.0, < 3.0"   # Use version between 2.0 and less than 3.0
    }
  }
}
```
#### Quick Understanding 
-	terraform → Main configuration block 
-	required_providers → List of providers Terraform must install 
-	aws / azurerm → Provider names 
-	source → Where Terraform downloads provider 
-	version → Controls which versions are allowed 
#### --> Why we use this: Avoid version conflicts, Ensure same setup in all environments, Control provider updates and Support multi-cloud (AWS + Azure)
-	Infrastructure → Basic resources (server, network, storage) needed to run applications. Infrastructure is the base resources. EC2, VPC, S3
-	Install → Put software into a system (download + install). Install means adding software. Install Nginx
-	Setup → Prepare system/software to start using. Setup means preparing it to run. Start Nginx service
-	Configure → Customize settings to control how it works. Configure means customizing settings. Change port to 8080. Change config file (port, domain)
#### Real-life Example
-	Buy house → Infrastructure, Bring furniture → Install, Arrange furniture → Setup, Decorate rooms → Configure

#### Configure
Set or adjust settings to make a system/application work properly. Configure means setting parameters so a system works as required. “tell the system how to behave”
#### Examples
-	Set region in AWS → Provider configuration 
-	Set IP address → Network configuration 
-	Set username/password → Application configuration 
-	Set port number (80/443) → Server configuration 

#### In Terraform
-	Configure provider → Tell Terraform which region, credentials to use 
-	 Example: provider "aws" → region = "us-east-1" → Configure AWS to work in that region 
#### Real-life example
-	Buy phone → Infrastructure 
-	Install apps → Setup 
-	“Change settings (WiFi, language) → Configuration “
