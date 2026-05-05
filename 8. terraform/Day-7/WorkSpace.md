# Workspace
Used to manage multiple environments (dev, test, prod) using same Terraform code 
#### Key Points
-	Purpose → Separate environments without changing code 
-	Default workspace → default 
-	Each workspace → Has its own state file 
-	Use case → dev, staging, production environments 
#### Commands
-	terraform workspace list → Show all workspaces 
-	terraform workspace new dev → Create new workspace named dev 
-	terraform workspace select dev → Switch to dev workspace 
-	terraform workspace show → Show current workspace 
-	terraform workspace delete dev → Delete workspace 
#### Example
```resource "aws_instance" "example" {   # Create EC2 instance

  instance_type = terraform.workspace == "prod" ? "t2.large" : "t2.micro"   # Use bigger instance for prod, small for others

}
```
- Simple Flow: Create workspace → Switch workspace → Apply same code → Different environments created 
#### Why we use Workspace:
Avoid duplicating code, Manage environments easily, Keep separate state files and Easy testing and deployment
#### Why not use only one environment?
-	If you use only one (prod) → Any mistake can break live application 
-	No testing → Bugs go directly to users 
-	Risk is very high → Downtime, data loss, customer impact 
#### Why we need 3 environments
- Dev (Development): Used to write and test code freely, Developers can make mistakes safely  and No impact on real users 
- Test (Testing / Staging): Used to verify application before release, QA checks bugs, performance, behavior, Acts like a simulation of production 
- Prod (Production): Used by real users, Should be stable and error-free, Only tested code is deployed here 
- Simple Flow: Dev → Write code, Test → Check code, Prod → Release code 

-	Without environments → You change code → Website crashes 
-	With environments → Dev → Fix & test, Test → Verify, Prod → Safe release 
- Key Point: Environments reduce risk, improve quality, and ensure stability 
•	One environment = High risk 
•	Three environments = Safe, tested, reliable system
