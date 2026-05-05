#### 1. How Terraform decides execution order?
Terraform builds a dependency graph based on resource references and executes resources in the correct order automatically, not based on file order.
#### 2. What happens if Terraform state file is deleted?:
Terraform loses track of all managed resources, which can lead to resource duplication, inability to destroy infrastructure, and loss of infrastructure state.
#### 3. What is Terraform state backup file:
Terraform automatically creates a backup of the previous state file before making changes, stored as terraform.tfstate.backup, which helps in recovery if the current state file is corrupted or lost.
#### 4. What happens if you run Terraform apply multiple times?
Terraform is idempotent, so running terraform apply multiple times without any changes will not modify the infrastructure. It only applies changes when there is a difference between configuration and state.
