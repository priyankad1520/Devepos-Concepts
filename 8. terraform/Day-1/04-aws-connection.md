# Setup Terraform for AWS
#### Terraform Installation Steps
First, configure AWS if needed, then go to the Terraform documentation, download and install Terraform, run the commands on your machine, and finally verify the installation using terraform --version.
1. Step 1: Go to Terraform Official Website
2. Step 2: Choose Your Operating System: Select Windows / Linux / Mac based on your system 
3. Step 3: Download Terraform: Download the Terraform zip file  Extract the file 
4. Step 4: Set Environment Variable (PATH)
-	Copy the Terraform folder path  Add it to System Environment Variables (PATH) 
- This step is important so you can run Terraform from anywhere
5. Step 5: Verify Installation: terraform –version: If installed correctly → it shows Terraform version 
- Download → Extract → Set PATH → Verify using terraform –version
- Basic AWS Configuration (Local System)
- Install AWS CLI → Tool to interact with AWS from terminal 
-	Run aws configure → Start setup process 
-	Enter Access Key → From AWS IAM user 
-	Enter Secret Key → Secure key for authentication 
-	Set Region → Example: ap-south-1 
-	Set Output Format → json (recommended)

To configure AWS credentials and set up Terraform to work with AWS, you'll need to follow these steps:

1. **Install AWS CLI (Command Line Interface)**:

Make sure you have the AWS CLI installed on your machine. You can download and install it from the [AWS CLI download page](https://aws.amazon.com/cli/).

2. **Create an AWS IAM User**:

To interact with AWS programmatically, you should create an IAM (Identity and Access Management) user with appropriate permissions. Here's how to create one:

a. Log in to the AWS Management Console with an account that has administrative privileges.

b. Navigate to the IAM service.

c. Click on "Users" in the left navigation pane and then click "Add user."

- Choose a username, select "Programmatic access" as the access type, and click "Next: Permissions."

- Attach policies to this user based on your requirements. At a minimum, you should attach the "AmazonEC2FullAccess" policy for basic EC2 operations. If you need access to other AWS services, attach the relevant policies accordingly.

- Review the user's configuration and create the user. Be sure to save the Access Key ID and Secret Access Key that are displayed after user creation; you'll need these for Terraform.

3. **Configure AWS CLI Credentials**:

Use the AWS CLI to configure your credentials. Open a terminal and run:

```
aws configure
```

It will prompt you to enter your AWS Access Key ID, Secret Access Key, default region, and default output format. Enter the credentials you obtained in the previous step.
