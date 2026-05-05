#  Terraform Commands (Step-by-Step )

**1. Install Terraform:** Download from → Terraform official site. Verify installation: Confirms Terraform is installed
```bash
terraform -version
```
**2. Create Project Folder:** Keep all Terraform files in one directory
```bash
mkdir terraform-project
cd terraform-project
```
**3. Create Configuration File:** Create a file:
```bash
touch main.tf
```
`main.tf` → Main configuration file
**4. Write Basic Configuration:** Example (AWS EC2):
```hcl
# Provider (AWS)
provider "aws" {                  
  region = "us-east-1"
}
# Resource (EC2 instance)
resource "aws_instance" "my_ec2" {
  ami           = "ami-12345678"
  instance_type = "t2.micro"
}
```
**5. Initialize Terraform:** Downloads provider plugins, Creates `.terraform/` folder, Prepares environment/working directory
```bash
terraform init    # Must run first time
```
**6. Validate Configuration:** Checks syntax errors, Ensures configuration is correct. Example: Missing brackets → error and Wrong config → error
```bash
terraform validate
```
**7. Format Code (Optional but Good Practice):** Makes code clean and readable/ Cleans and formats your .tf files
```bash
terraform fmt
```
**8. Plan Execution:** What Terraform will create/update/delete, No actual changes yet or “Plan is a dry run”. What resources will be created. What will be changed or destroyed. 
```bash
terraform plan
```
**9. Apply Changes (Create Resources):** Creates infrastructure/ This actually Creates resources in cloud (VM, network, etc.),  Will ask for confirmation → type `yes`.  
```bash
terraform apply
```
**10. Auto Approve (Used in CI/CD):** Skips manual confirmation
```bash
terraform apply -auto-approve
```
**11. Check State:** Shows managed resources/ Shows created resources. 
```bash
terraform state list
```
**12. Show Resource Details:** Displays current infrastructure state/ Track infrastructure in .tfstate file
```bash
terraform show
```
**13. Destroy Resources:** Deletes all created resources created by terraform and it's Saves cost
```bash
terraform destroy
```
**14. Auto Destroy (CI/CD):** 

```bash
terraform destroy -auto-approve
```
**15. Output Values:** Shows outputs like: Public IP, DNS name
```
terraform output
```
---

#### Easy Way to Remember

* **init** → Start
* **validate** → Check
* **plan** → Preview
* **apply** → Create
* **destroy** → Delete
*  “In Terraform, I start with terraform init to initialize, then validate and plan to check changes, and finally apply to create infrastructure. I also use destroy to clean up resources.”
---
### Terraform Key Terminology 

1. Provider: A plugin that connects Terraform to a cloud platform. “Provider = connection to cloud” Example → AWS, Azure, GCP. Use → Without provider, Terraform cannot create resources 
2. Resource: Actual infrastructure you create. “Resource = what you create” 
Examples → EC2, S3, VPC. Important → Every resource has type + configuration 
3. Module: Reusable Terraform code block. “Module = reusable template” 
Use → Write once, use many times 
Example → Create same EC2 setup for dev & prod 
4. Configuration File (.tf): File where you write Terraform code. “.tf file = where you define everything”. Example files → main.tf, variables.tf, outputs.tf 
5. Variable: Input values for your code. “Variable = dynamic input” 
Example → instance_type = t2.micro. Use → Makes code flexible & reusable 
6. Output: Result shown after execution. “Output = result you see”. Example → EC2 public IP 
7. State File (.tfstate): Stores current infrastructure status. “State = memory of Terraform” 
Why important → Tracks what is created & updated 
8. Plan: Preview of changes. “Plan = what will happen” 
Command → terraform plan. Use → Avoid mistakes before applying 
9. Apply: Executes the changes. “Apply = do the work” 
Command → terraform apply. Result → Resources are created/updated 
10. Workspace: Separate environments. “Workspace = different environments” 
Examples → dev, test, prod. Use → Same code, different environments 
11. Remote Backend: Store state file in remote location. “Remote backend = shared storage” 
Examples → S3, Terraform Cloud. Why needed → Team collaboration + security 
Terraform Lifecycle
•	Write (.tf files) → Define infrastructure in code 
•	terraform init → Initialize project & download providers 
•	terraform validate → Check code syntax 
•	terraform plan → Preview what will be created/changed 
•	terraform apply → Create/update infrastructure 
•	terraform state → Track infrastructure in .tfstate file 
•	terraform destroy → Delete all resources
---
### Does terraform care about file name
Terraform does NOT care about file names. Terraform will read ALL .tf files together. It only cares about .tf extension. BUT there is ONE EXCEPTION: terraform.tfvars → Name matters

This file must be: terraform.tfvars. Only this name is auto-loaded
If you rename: myvars.tfvars.  Then Terraform won’t read it unless you do:
1. CLI arguments: terraform apply -var="instance_type=t2.micro"
2. Custom tfvars file: terraform apply -var-file="custom.tfvars" or “myvars.tfvars”
3. Auto-loaded files: Any file ending with:  *.auto.tfvars  Terraform automatically loads
> Example: dev.auto.tfvars or prod.auto.tfvars
- If multiple .auto.tfvars exist: Terraform loads ALL of them. If same variable → last one wins
- Never push to git this 2 files: terraform.tfstate and terraform.tfvars
- Best Practice Folder Structure
  
- For DEV environment: terraform apply -var-file="dev.tfvars"
- For PROD: terraform apply -var-file="prod.tfvars"
4. Default values in variables.tf 
```
variable "instance_type" {
  default = "t2.micro"
}
```
- Arguments = Input (what you give)
- Attributes = Output (what Terraform gives back)

Concept	Meaning	Example
- Runtime Environment	place where your application runs. It provides everything needed to execute your code	Python, Node, Docker
- Environment Variables	Dynamic values. key-value settings. Used to control app behavior without changing code	PORT=3000
- Infrastructure	physical or cloud resources. Where your app is deployed and runs	EC2, K8s, Server
- Configuration	Behavior settings. settings that define how your system behaves	YAML, JSON

