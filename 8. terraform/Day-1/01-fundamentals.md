# Infrastructure as Code (IaC)
Before IaC, managing infrastructure was manual and slow process
#### Problems in Traditional Method
-	Manual Configuration → Servers were set up manually → leads to errors and inconsistency
-	No Version Control → Difficult to track changes or rollback
-	Documentation Heavy → Need to write steps manually → becomes outdated quickly
-	Less Automation → Only basic scripting → not flexible
-	Slow Provisioning → Creating new resources takes more time
#### How IaC Solves These Problems
-	Automation → Infrastructure created automatically using code
-	Consistency → Same setup every time (no errors)
-	Version Control → Track changes using Git
-	Faster Deployment → Create resources quickly
-	Easy Management → Modify infrastructure easily

- Popular IaC Tools: Terraform, AWS CloudFormation, Azure Resource Manager (ARM)
#### Key Advantages
-	Multi-Cloud Support → Works with AWS, Azure, GCP, and on-premises
-	Large Ecosystem → Many ready-made modules and providers available
-	Declarative Syntax → Define what you want, not how to do it
-	State Management → Keeps track of current infrastructure using state file
-	Plan & Apply → Preview changes before applying → avoids mistakes
-	Strong Community → Easy to get help, tutorials, and solutions
-	Integration → Works with Docker, Kubernetes, Jenkins, Ansible
-	HCL Language → Easy to read and write configuration language
#### In Simple Words
-	IaC → Write code to create infrastructure
-	Terraform → Tool to automate and manage that code easily
# Terraform
Terraform is a tool used to create and manage infrastructure using code. It is called Infrastructure as Code (IaC). You write code instead of manually creating servers, networks, etc. 
- Terraform = “Write code → Infrastructure is created automatically”
- Infrastructure → All the basic resources (servers, network, storage, software) needed to run an application
- Ex: Instead of creating an EC2 manually in AWS console, you write code and Terraform creates it
#### Why we use Terraform?
To automate infrastructure setup, save time and effort, avoid manual mistakes, maintain same setup everywhere (dev, test, prod) and manage infrastructure easily using code 
#### What kind of problems it solves?
-	Manual work → Takes time  Terraform automates everything 
-	Human errors → Wrong configuration  Terraform ensures consistent setup 
-	Difficult to manage large infrastructure Terraform manages everything in one place 
-	No tracking of changes Terraform tracks changes using state file 
Without Terraform: Login to AWS  Click EC2 → Launch instance → Select AMI, instance type → key pair → Configure network →Launch * Time consuming + manual errors possible
# Infrastructure as Code(IaC)

Before the advent of IaC, infrastructure management was typically a manual and time-consuming process. System administrators and operations teams had to:

1. Manually Configure Servers: Servers and other infrastructure components were often set up and configured manually, which could lead to inconsistencies and errors.

2. Lack of Version Control: Infrastructure configurations were not typically version-controlled, making it difficult to track changes or revert to previous states.

3. Documentation Heavy: Organizations relied heavily on documentation to record the steps and configurations required for different infrastructure setups. This documentation could become outdated quickly.

4. Limited Automation: Automation was limited to basic scripting, often lacking the robustness and flexibility offered by modern IaC tools.

5. Slow Provisioning: Provisioning new resources or environments was a time-consuming process that involved multiple manual steps, leading to delays in project delivery.

IaC addresses these challenges by providing a systematic, automated, and code-driven approach to infrastructure management. Popular IaC tools include Terraform, AWS CloudFormation, Azure Resource Manager templates others. 

These tools enable organizations to define, deploy, and manage their infrastructure efficiently and consistently, making it easier to adapt to the dynamic needs of modern applications and services.

# Why Terraform ?

There are multiple reasons why Terraform is used over the other IaC tools but below are the main reasons.

1. **Multi-Cloud Support**: Terraform is known for its multi-cloud support. It allows you to define infrastructure in a cloud-agnostic way, meaning you can use the same configuration code to provision resources on various cloud providers (AWS, Azure, Google Cloud, etc.) and even on-premises infrastructure. This flexibility can be beneficial if your organization uses multiple cloud providers or plans to migrate between them.

2. **Large Ecosystem**: Terraform has a vast ecosystem of providers and modules contributed by both HashiCorp (the company behind Terraform) and the community. This means you can find pre-built modules and configurations for a wide range of services and infrastructure components, saving you time and effort in writing custom configurations.

3. **Declarative Syntax**: Terraform uses a declarative syntax, allowing you to specify the desired end-state of your infrastructure. This makes it easier to understand and maintain your code compared to imperative scripting languages.

4. **State Management**: Terraform maintains a state file that tracks the current state of your infrastructure. This state file helps Terraform understand the differences between the desired and actual states of your infrastructure, enabling it to make informed decisions when you apply changes.

5. **Plan and Apply**: Terraform's "plan" and "apply" workflow allows you to preview changes before applying them. This helps prevent unexpected modifications to your infrastructure and provides an opportunity to review and approve changes before they are implemented.

6. **Community Support**: Terraform has a large and active user community, which means you can find answers to common questions, troubleshooting tips, and a wealth of documentation and tutorials online.

7. **Integration with Other Tools**: Terraform can be integrated with other DevOps and automation tools, such as Docker, Kubernetes, Ansible, and Jenkins, allowing you to create comprehensive automation pipelines.

8. **HCL Language**: Terraform uses HashiCorp Configuration Language (HCL), which is designed specifically for defining infrastructure. It's human-readable and expressive, making it easier for both developers and operators to work with.
