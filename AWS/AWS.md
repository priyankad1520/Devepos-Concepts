 
### Basic AWS Commands
-	aws configure → Set AWS access key, secret key, region
-	aws help → Get help for AWS CLI commands 
- aws --version → Check AWS CLI version 
### EC2 Commands
- aws ec2 describe-instances → View EC2 instances 
-	aws ec2 run-instances → Launch new EC2 instance 
-	aws ec2 stop-instances --instance-ids ID → Stop instance 
-	aws ec2 start-instances --instance-ids ID → Start instance 
-	aws ec2 terminate-instances --instance-ids ID → Delete instance 
### S3 Commands
- aws s3 ls → List all S3 buckets
- aws s3 mb s3://bucket-name → Create bucket 
-	aws s3 cp file.txt s3://bucket-name/ → Upload file 
-	aws s3 sync . s3://bucket-name/ → Upload folder 
-	aws s3 rm s3://bucket-name/file.txt → Delete file 
### IAM Commands
-	aws iam list-users → List IAM users 
-	aws iam create-user --user-name name → Create user 
-	aws iam delete-user --user-name name → Delete user 
### VPC Commands
-	aws ec2 describe-vpcs → List VPCs 
-	aws ec2 create-vpc --cidr-block 10.0.0.0/16 → Create VPC 
### CloudWatch Commands
-	aws cloudwatch list-metrics → View metrics 
-	aws logs describe-log-groups → View logs

**Cloud Computing:** Cloud computing means using servers, storage, and services over the internet instead of local systems. It helps reduce cost, improve scalability, and avoid hardware management.

**EC2 (Elastic Compute Cloud):** EC2 is a virtual server in AWS. It is used to run applications without physical hardware. You can start, stop, and terminate instances anytime. You pay only when it is running.

**VPC (Virtual Private Cloud):** VPC is a private network in AWS. It is used to securely run resources. It has subnets (public and private), route tables, and gateways. It provides full control over networking.

**S3 (Simple Storage Service):** S3 is object storage used to store files. Data is stored in buckets as objects. It provides high durability and unlimited storage. Used for backup, static websites, and file storage.

**IAM (Identity and Access Management):** IAM controls access in AWS. It defines who can access what. It includes users, groups, roles, and policies. It improves security using least privilege.

**CloudWatch:** CloudWatch is a monitoring service. It tracks metrics like CPU, memory, and network. It stores logs and creates alarms. It helps detect and fix issues quickly.

**EC2 Lifecycle:** Launch → create instance, Running → working state, Stop → paused (no compute cost), Start → resume, Terminate → delete permanently

**Instance Family:** General purpose → balanced usage, Compute optimized → high CPU, Memory, optimized → high RAM, Storage optimized → high disk, Accelerated → GPU workloads

**Cloud Types:** Public cloud → shared and cost-effective, Private cloud → secure and dedicated, Hybrid cloud → mix of both

EC2 = virtual server, VPC = private network, S3 = storage, IAM = access control, CloudWatch = monitoring

## Cloud Computing 
Cloud Computing: Using servers, storage, databases, networking, and software over the internet instead of your local computer. Instead of saving files on your laptop → you save them in Google Drive / AWS / Azure

**Why Cloud is Used?**
- Before cloud: Companies had to buy physical servers, Costly, Hard to maintain 
- Now with cloud: No need to buy hardware, Pay only for what you use, Access from anywhere, hight availability, easy scaling when traffic increases
Infrastructure (Basic Building Blocks)
- Cloud provides: Compute → Virtual Machines (EC2 in AWS), Storage → S3 (files), EBS (disks), Networking → VPC, Subnets, IP 
- Think like: Cloud = Data center on internet

**Types of cloud service provider**

**IaaS (Infrastructure as a Service):** Infrastructure is like getting a raw computer.
- What is: IaaS is a cloud service model where the provider gives infrastructure like virtual machines, storage, and networking over the internet. You get a virtual server and you can install OS and software as you need.
- Why we use: We use IaaS to avoid buying physical hardware and to get full control over the system configuration. It allows flexible resource usage and quick setup.
- What kind of problem it solves: It solves problems like high hardware cost, limited capacity, and time-consuming server setup. It also removes the need for maintaining physical data centers.
- Example: Using EC2 in Amazon Web Services

**PaaS (Platform as a Service):** Platform is like getting a ready system to build apps
- What is: PaaS is a cloud service model where the provider gives a platform with OS, runtime, and development tools so you can directly build and deploy applications without worrying about infrastructure.
- Why we use: We use PaaS to focus only on application development without managing servers, OS, or updates. It speeds up development and deployment.
- What kind of problem it solves: It solves problems like environment setup, dependency management, and infrastructure maintenance. Developers don’t need to configure servers or worry about scaling.
- Example: Using App Service in Microsoft Azure

**SaaS (Software as a Service):** Software is like getting a finished app to use directly.
- What is: SaaS is a cloud service model where software applications are delivered over the internet and you can use them directly without installing anything.
- Why we use: We use SaaS for easy access to applications from anywhere without installation or maintenance. It is user-friendly and ready to use.
- What kind of problem it solves: It solves problems like software installation, updates, maintenance, and compatibility issues. Everything is managed by the provider.
- Example: Using Google Docs or Gmail

**Interview Answer:** Cloud service models include IaaS, PaaS, and SaaS. IaaS provides infrastructure like servers and networking, PaaS provides a platform for application development, and SaaS provides ready-to-use software over the internet. These models help reduce cost, simplify management, and improve scalability.
Infrastructure is the basic hardware resources, platform is an environment to develop and run applications, and software is a ready-to-use application for end users.

## Types of cloud 
**Public Cloud** is a cloud environment where resources like servers, storage, and applications are provided over the internet and shared among multiple users.
- The infrastructure is owned and managed by companies like Amazon Web Services, Microsoft Azure, and Google Cloud.
- You can access services from anywhere, and you only pay for what you use.
- It is best for general applications, startups, and projects that need scalability and low cost.

**Private Cloud** is a cloud environment dedicated to a single organization.
- The infrastructure is not shared with others and can be hosted in a company’s own data center or by a cloud provider.
- It offers higher security, control, and customization.
- It is mainly used by banks, government organizations, and companies that handle sensitive data.

**Hybrid Cloud** is a combination of both public cloud and private cloud.
- In this setup, some applications or data run on private cloud, while others run on public cloud.
- It allows companies to keep critical data secure in private cloud and use public cloud for less sensitive tasks.
- It provides flexibility, cost efficiency, and better control over workloads.

## IAM
AWS IAM (Identity and Access Management) is a service provided by Amazon Web Services (AWS) that helps you manage access to your AWS resources. It's like a security system for your AWS account.
- IAM allows you to create and manage users, groups, and roles. With IAM, you can control and define permissions through policies. 
- IAM follows the principle of least privilege, meaning users and entities are given only the necessary permissions required for their tasks, minimizing potential security risks. IAM also provides features like multi-factor authentication (MFA) for added security and an audit trail to track user activity and changes to permissions.
- By using AWS IAM, you can effectively manage and secure access to your AWS resources, ensuring that only authorized individuals have appropriate permissions and actions are logged for accountability and compliance purposes.

**Why do we use IAM?**
- IAM is used to provide secure access to AWS resources.
- It ensures that only authorized users can access services like EC2, S3, or databases.
- It helps in controlling permissions so that users can perform only specific actions.
- It improves security by avoiding sharing of root account credentials.

**What problem does IAM solve?**
- Without IAM, everyone would need to use the root account, which is risky and insecure.
- There would be no proper control over who can access what.
- IAM solves this by giving fine-grained access control and improving security.

**Components of IAM**
- **Users:** IAM users represent individual people or entities (such as applications or services) that interact with your AWS resources. Each user has a unique name and security credentials (password or access keys) used for authentication and access control.
- **Groups:** IAM groups are collections of users with similar access requirements. Instead of managing permissions for each user individually, you can assign permissions to groups, making it easier to manage access control. Users can be added or removed from groups as needed.
- **Roles:** IAM roles are used to grant temporary access to AWS resources. Roles are typically used by applications or services that need to access AWS resources on behalf of users or other services. Roles have associated policies that define the permissions and actions allowed for the role.
- **Policies:** With IAM, you can control and define permissions through policies. Policies are written in JSON format and specify what actions are allowed or denied on specific AWS resources. These policies can be attached to IAM entities (users, groups, or roles) to grant or restrict access to AWS services and resources.

## EC2
EC2 is a cloud service provided by AWS that allows users to create virtual servers on demand. It eliminates the need for physical hardware, provides scalability, and follows a pay-as-you-go model, making it efficient for hosting applications.
- EC2 (Elastic Compute Cloud) is a service provided by Amazon Web Services (AWS) that gives you a virtual server in the cloud. It allows you to create and run a computer (instance) without buying physical hardware.
- In simple words, EC2 is like renting a computer on the internet where you can install software, run applications, and host websites.
- Why do we use EC2: We use EC2 to avoid buying and maintaining physical servers. It helps in quickly launching applications because you can create a server in minutes. It allows scaling, meaning you can increase or decrease resources like CPU and RAM based on your need. It is cost-efficient because you pay only for the time your server is running.
- What problem does EC2 solve: Before EC2, companies had to buy expensive servers, wait for setup, and handle maintenance. If traffic increased suddenly, servers would crash because scaling was difficult. With EC2, you can instantly create servers, handle traffic using scaling, and avoid hardware costs.
- What is an EC2 Instance: An EC2 instance is a virtual server. It behaves like a real computer where you can install Linux or Windows and run your applications. Each instance has CPU, RAM, storage, and network configuration.

**Key Components of EC2**
- **AMI (Amazon Machine Image)** is a template used to launch an instance, and it contains OS and pre-installed software.
- **Instance Type** defines the power of the server like CPU, RAM, and performance.
- **Key Pair** is used to securely connect login to the instance using SSH.
- **Security Group** acts like a firewall and controls incoming and outgoing traffic.
- **EBS (Elastic Block Store)** is storage attached to the instance.
- **Elastic IP** is a static public IP address used to access the instance.
- **How EC2 Works:** You choose an AMI like Ubuntu or Windows. You select instance type based on your requirement. You configure storage and network settings. You create a key pair and security group. You launch the instance and connect using SSH or RDP. You install software and deploy your application.
- **Types of EC2 Instances:** General purpose instances are used for normal applications. Compute optimized instances are used for CPU-heavy tasks. Memory optimized instances are used for large data processing. Storage optimized instances are used for high disk usage
- **Pricing Models:** On-Demand means you pay per usage with no commitment. Reserved Instances give discount if you commit for 1 or 3 years. Spot Instances are very cheap but can be stopped anytime by AWS.
- **Auto Scaling & Load Balancer:** Auto Scaling automatically increases or decreases the number of instances based on traffic. Load Balancer distributes traffic across multiple instances to avoid overload.
- **Security in EC2:** Security Groups control traffic like firewall rules. Key pairs provide secure login. IAM roles help manage permissions securely.
- **Example:** If you want to host a website, you launch an EC2 instance, install a web server like Nginx, and deploy your application. When users visit your website, they are actually accessing your EC2 server.

**EC2 Lifecycle**
- Launch Instance (create server) is the first step where you create a virtual server using an AMI, instance type, storage, and security settings. At this stage, AWS prepares the instance and allocates resources for it.
- Running (server is working) means the instance is active and working.
- In this state, your application is running, and you are charged for compute (CPU, RAM) and storage.
- You can connect to the instance using SSH (Linux) or RDP (Windows).
- Stop (server is paused) means the instance is shut down but not deleted.
- The data in attached storage like EBS is (safe), but the compute resources are released.
- You are not charged for compute when stopped, but you still pay for storage.
- Start (server is resumed) means restarting a stopped instance.
- When you start it again, AWS assigns compute resources and the instance becomes running again.
- Your application continues from where it was stopped.
- Terminate means permanently deleting the instance.
- All data in the instance (except separately saved storage) is lost. After termination, you cannot recover the instance.

## VPC (Virtual Private Cloud)
VPC is a virtual network in AWS that allows users to securely launch resources in an isolated environment. It provides control over IP addressing, subnets, routing, and security, ensuring safe communication between resources.

VPC (Virtual Private Cloud) is a service provided by Amazon Web Services (AWS) that allows you to create your own private network inside the cloud.

**In simple words,** VPC is like your own data center network in AWS where you can launch resources like EC2 securely.

**Why do we use VPC?:** We use VPC to isolate our resources from others in the cloud. It gives full control over networking, including IP address range, subnets, routing, and security. It improves security because only allowed traffic can enter or leave the network.

**What problem does VPC solve?:** Without VPC, all resources would be in a shared network, which is not secure. There would be no control over who can access your servers. VPC solves this by providing a private and secure network environment.

**Key Components of VPC**
- **Virtual private clouds (VPC):** A VPC is a virtual network that closely resembles a traditional network that you'd operate in your own data center. After you create a VPC, you can add subnets.
- **A Subnet** is a smaller network inside a VPC where you place your resources. A subnet is a range of IP addresses in your VPC. A subnet must reside in a single Availability Zone. After you add subnets, you can deploy AWS resources in your VPC.
- **IP addresses:** You can assign IP addresses, both IPv4 and IPv6, to your VPCs and subnets. You can also bring your public IPv4 and IPv6 GUA addresses to AWS and allocate them to resources in your VPC, such as EC2 instances, NAT gateways, and Network Load Balancers.
- **A Public Subnet** allows internet access, while a Private Subnet does not allow direct internet access.
- **An Internet Gateway (IGW)** allows communication between your VPC and the internet.
- **A Route Table** defines how traffic flows inside the VPC. Use route tables to determine where network traffic from your subnet or gateway is directed.
- **A NAT Gateway** allows private instances to access the internet without exposing them.
- **A Security Group** acts as a firewall at the instance level. A security group acts as a virtual firewall for instances (EC2 instances or other resources) within a VPC. It controls inbound and outbound traffic at the instance level. Security groups allow you to define rules that permit or restrict traffic based on protocols, ports, and IP addresses.  
- **A Network ACL (NACL)** acts as a firewall at the subnet level. A Network Access Control List is a stateless firewall that controls inbound and outbound traffic at the subnet level. It operates at the IP address level and can allow or deny traffic based on rules that you define. NACLs provide an additional layer of network security for your VPC.
- **Gateways and endpoints:** A gateway connects your VPC to another network. For example, use an internet gateway to connect your VPC to the internet. Use a VPC endpoint to connect to AWS services privately, without the use of an internet gateway or NAT device.
- **Peering connections:** Use a VPC peering connection to route traffic between the resources in two VPCs.
- **Traffic Mirroring:** Copy network traffic from network interfaces and send it to security and monitoring appliances for deep packet inspection.
- **Transit gateways:** Use a transit gateway, which acts as a central hub, to route traffic between your VPCs, VPN connections, and AWS Direct Connect connections.
- **VPC Flow Logs:** A flow log captures information about the IP traffic going to and from network interfaces in your VPC.
- **VPN connections:** Connect your VPCs to your on-premises networks using AWS Virtual Private Network (AWS VPN).
- **How VPC Works :** You create a VPC with an IP range. You create subnets inside the VPC. You attach an Internet Gateway for internet access. You configure route tables to control traffic. You launch EC2 instances inside subnets.
- **Real-Time Example:** If you are building an application, you place your web server in a public subnet so users can access it. You place your database in a private subnet so it is secure and not directly exposed to the internet.
- **Simple Understanding:** VPC is your private network. Subnets divide the network. IGW gives internet access. Route table controls traffic.

## S3 (Simple Storage Service) 
S3 is an object storage service provided by AWS that allows users to store and retrieve data at any scale. It offers high durability, scalability, and security, making it ideal for storing files, backups, and static content.

S3 (Simple Storage Service) is a storage service provided by Amazon Web Services (AWS) that allows you to store and retrieve data over the internet.

**In simple words,** S3 is like an online storage where you can keep files such as images, videos, documents, and backups.

**Why do we use S3?:** We use S3 to store large amounts of data without worrying about storage limits. It provides high durability, meaning your data is safely stored and rarely lost. It is accessible from anywhere using the internet.It is cost-effective because you pay only for the storage you use.

**What problem does S3 solve:** Before S3, storing large data required physical storage systems, which were expensive and hard to manage. There was also a risk of data loss due to hardware failure. S3 solves this by providing scalable, secure, and highly durable storage in the cloud.

**How S3 Works:** In S3, data is stored in buckets. A bucket is like a folder that holds your files. Each file stored in S3 is called an object. Each object has a unique name called a key.

**Key Features of S3:** S3 provides unlimited storage capacity. It offers high durability (99.999999999%). It supports versioning, which means you can keep multiple versions of a file. It provides security using IAM policies and bucket policies. It supports lifecycle rules to automatically move or delete data.

**Storage Classes:** Standard is used for frequently accessed data. Infrequent Access is used for data accessed less often. Glacier is used for long-term backup and archival.

**Security in S3:** Access is controlled using IAM policies and bucket policies. You can make data private or public based on your need. Encryption is available to protect data.

**Real-Time Example:** If you build a website, you can store images, videos, and static files in S3. When users access your website, files are served from S3 instead of your server. You can also use S3 for backups, logs, and data storage.

**Simple Understanding:** S3 is cloud storage. Bucket is a container. Object is a file. Key is file name.

## CloudWatch
CloudWatch is an AWS monitoring service used to track metrics, collect logs, and set alarms for AWS resources and applications, helping in performance monitoring and troubleshooting.

CloudWatch is a monitoring service. It is used to monitor your AWS resources and applications.

**In simple words,** CloudWatch helps you see what is happening in your system.

**Why do we use CloudWatch:** We use CloudWatch to track performance of services like EC2, S3, and applications. It helps us detect problems early and take action. It allows automatic alerts when something goes wrong. It helps in troubleshooting and improving system performance.

**What problem does CloudWatch solve:** Without monitoring, we don’t know if our server is slow, down, or overloaded. We cannot track errors or performance issues. CloudWatch solves this by providing real-time monitoring, logs, and alerts.

**Key Features of CloudWatch:** CloudWatch collects metrics like CPU usage, memory, and network activity. It stores logs from applications and servers. It allows you to create alarms to get notifications. It supports dashboards to visualize data.

**How It Works:** CloudWatch collects data from AWS resources. It monitors metrics like CPU usage of EC2. If CPU usage goes high, it triggers an alarm. You get a notification or automatic action is taken.

**Real-Time Example:** If your EC2 CPU usage goes above 80%, CloudWatch sends an alert. You can also configure it to automatically add more instances using Auto Scaling.

**Simple Understanding:** CloudWatch is like a health monitor for your system. It shows performance, logs, and alerts.

**CloudWatch – Key Points**
- CloudWatch is a monitoring service from Amazon Web Services.
- It is used to monitor AWS resources like EC2, S3, and applications.
- It collects data called metrics such as CPU usage, memory, and network.
- It stores logs from servers and applications.
- It helps you understand system performance.
- It allows you to create alarms when something goes wrong.
- It sends notifications when limits are crossed (like high CPU).
- It supports dashboards to visualize data.
- It helps in troubleshooting issues quickly.
- It can trigger automatic actions like Auto Scaling.

## Lambda
AWS Lambda is a serverless compute service that allows users to run code in response to events without managing servers, with automatic scaling and pay-per-use pricing.

AWS Lambda is a serverless computing service. It allows you to run code without managing servers.

**In simple words,** you just write code and AWS runs it for you.

**Why do we use Lambda:** We use Lambda to avoid managing servers like EC2. It automatically scales when requests increase. You pay only when your code runs. It is useful for event-based tasks.

**What problem does Lambda solve:** Before Lambda, we had to create and manage servers even for small tasks. Servers might be idle but still cost money. Lambda solves this by running code only when needed and removing server management.

**How Lambda Works:** You write a function (code). You upload it to Lambda. An event triggers the function. Lambda runs the code and returns the result.

**What is Event-Driven:** Lambda works on events.
- An event can be: Uploading a file to S3, HTTP request from API, Database change
- When event happens → Lambda runs automatically.

**Example:** When a file is uploaded to S3, Lambda automatically resizes the image. When a user submits a form, Lambda processes the data.

**Key Features:** No server management (serverless). Auto scaling. Pay per execution. Supports multiple languages like Python, Node.js, Java. Integrates with many AWS services.

**Simple Understanding:** Lambda = run code without server, Event = trigger, Execution = function runs

**How Lambda Functions Fit into the Serverless World**

At the heart of AWS Lambda are "Lambda functions." These are individual units of code that perform specific tasks. Think of them as small, single-purpose applications that run independently.

Here's how Lambda functions fit into the serverless world:

1.	Event-Driven Execution: Lambda functions are triggered by events. An event could be anything, like a new file being uploaded to Amazon S3, a request hitting an API, or a specific time on the clock. When an event occurs, Lambda executes the corresponding function.

2.	No Server Management: As a developer, you don't need to worry about managing servers. AWS handles everything behind the scenes. You just upload your code, configure the trigger, and Lambda takes care of the rest.

3.	Automatic Scaling: Whether you have one user or one million users, Lambda scales automatically. Each function instance runs independently, ensuring that your application can handle any level of incoming traffic without manual intervention.

4.	Pay-per-Use: One of the most attractive features of serverless computing is cost efficiency. With Lambda, you pay only for the compute time your code consumes. When your code isn't running, you're not charged.

5.	Supported Languages: Lambda supports multiple programming languages like Node.js, Python, Java, Go, and more. You can choose the language you are comfortable with or that best fits your application's needs.

**Real-World Use Cases** 
Now, let's explore some real-world use cases to better understand how AWS Lambda can be applied:

1.	Automated Image Processing: Imagine you have a photo-sharing app, and users upload images every day. You can use Lambda to automatically resize or compress these images as soon as they are uploaded to S3.

2.	Chatbots and Virtual Assistants: Build interactive chatbots or voice-controlled virtual assistants using Lambda. These assistants can perform tasks like answering questions, fetching data, or even controlling smart home devices.

3.	Scheduled Data Backups: Use Lambda to create scheduled tasks for backing up data from one storage location to another, ensuring data resilience and disaster recovery.

4.	Real-Time Analytics: Lambda can process streaming data from IoT devices, social media, or other sources, allowing you to perform real-time analytics and gain insights instantly.

5.	API Backends: Develop scalable API backends for web and mobile applications using Lambda. It automatically handles the incoming API requests and executes the corresponding functions.

AWS Lambda – Key Points
- AWS Lambda is a serverless service from Amazon Web Services.
- It runs your code without managing servers.
- You just write code and upload it as a function.
-	It works on event-based triggers.
-	It automatically scales when requests increase.
-	You pay only when your code runs.
-	It supports languages like Python, Node.js, Java.
-	It integrates with services like S3, API Gateway, and CloudWatch.
-	It is used for automation, backend tasks, and data processing.
-	No need to manage infrastructure.
-	Lambda = serverless compute, Event = trigger, Function = code, Pay = per execution

## ECS (Elastic Container Service)
ECS (Elastic Container Service) is a container management service. It is used to run, manage, and scale Docker containers in AWS.

ECS is a fully managed container orchestration service in AWS that allows users to run, manage, and scale Docker containers using EC2 or Fargate without handling complex infrastructure.

**In simple words,** ECS helps you run applications inside containers without managing everything manually.

**Why do we use ECS:** We use ECS to easily deploy and manage containerized applications. It removes the complexity of managing containers manually. It helps in scaling applications automatically. It integrates well with other AWS services.

**What problem does ECS solve:** Before ECS, managing containers manually was complex and time-consuming. Scaling containers and handling failures was difficult. ECS solves this by providing container orchestration and easy management.

**How ECS Works:** You create a Docker container for your application. You define a Task Definition (CPU, memory, container details). You run it as a Task or Service. ECS manages running, scaling, and monitoring containers.

**Key Components of ECS:** Cluster is a group of servers where containers run. Task Definition is a blueprint of your container. Task is a running container. Service ensures containers are always running and handles scaling.

**Launch Types:** EC2 Launch Type means containers run on EC2 instances that you manage.

**Fargate Launch Type** means AWS manages servers, and you just run containers.

**Example:** You build a web application using Docker. You push the image to a registry. ECS runs the container and ensures it is always available. If traffic increases, ECS scales containers automatically.

**Simple Understanding:** ECS = manage containers. Task = running container. Cluster = group of servers. Service = keep app running

**1. What is AWS ECR?**

AWS Elastic Container Registry (ECR) is a fully managed container image registry service provided by Amazon Web Services (AWS). It enables you to store, manage, and deploy container images (Docker images) securely, making it an essential component of your containerized application development workflow. ECR integrates seamlessly with other AWS services like Amazon Elastic Container Service (ECS) and Amazon Elastic Kubernetes Service (EKS).

**2. Key Benefits of ECR**
- Security: ECR offers encryption at rest, and images are stored in private repositories by default, ensuring the security of your container images. 
- Integration: ECR integrates smoothly with AWS services like ECS and EKS, simplifying the deployment process. 
- Scalability: As a managed service, ECR automatically scales to meet the demands of your container image storage. 
- Availability: ECR guarantees high availability, reducing the risk of image unavailability during critical times.

ECS (Elastic Container Service) is a container management service from Amazon Web Services.
-	It is used to run and manage Docker containers in AWS.
-	It helps deploy, manage, and scale containerized applications.
-	You don’t need to manage complex orchestration manually.
-	ECS supports two launch types: EC2 and Fargate.
-	EC2 launch type means you manage the servers.
-	Fargate launch type means serverless (no server management).
-	A Task Definition is like a blueprint of your container (image, CPU, memory).
-	A Task is a running container.
-	A Service keeps your containers running and handles scaling.
-	It integrates with load balancers for traffic distribution.
-	It is commonly used for microservices and container-based applications.

## EKS (Elastic k8s server):
EKS (Elastic k8s server): EKS is a managed Kubernetes service provided by AWS that allows users to run and manage containerized applications without handling Kubernetes infrastructure, offering scalability, automation, and high availability.

**Why do we use EKS:** We use EKS to run and manage containers using Kubernetes easily. It removes the complexity of installing and managing Kubernetes control plane. It helps in scaling, load balancing, and automation. It is useful for microservices and large applications.

**What problem does EKS solve:** Setting up Kubernetes manually is complex and time-consuming. Managing clusters, scaling, and updates is difficult. EKS solves this by providing a managed Kubernetes environment.

**How EKS Works:** You create an EKS cluster. AWS manages the control plane (master nodes). You add worker nodes (EC2 or Fargate). You deploy applications using pods and services. Kubernetes manages scaling, load balancing, and deployment.

**Key Components:** Cluster is a group of machines running Kubernetes. Node is a server (EC2) where containers run. Pod is the smallest unit that runs containers. Service exposes your application to users.

**Launch Types:** EKS with EC2 means you manage worker nodes. EKS with Fargate means serverless containers (no node management). 

**Key Points:** EKS = Kubernetes service, Used for container orchestration, AWS manages control plane, Supports EC2 and Fargate, Used for microservices

**Example:** If you have a microservices application with many containers, EKS helps manage, scale, and deploy all services easily using Kubernetes.

**Simple Understanding:** EKS = Kubernetes managed by AWS, Pod = container, Cluster = group of nodes

## ELB (Elastic loadBalancer)
ELB is an AWS service that distributes incoming application traffic across multiple targets such as EC2 instances to ensure high availability, scalability, and fault tolerance.
 
It is used to distribute incoming traffic across multiple servers (EC2 instances).

**In simple words,** ELB acts like a traffic controller.

**Why do we use ELB:** We use ELB to avoid overloading a single server. It improves availability and reliability of applications. It automatically distributes traffic to multiple instances. If one server fails, ELB sends traffic to healthy servers.

**What problem does ELB solve:** Without ELB, all users hit one server, which can crash under heavy load. There is no failover if the server goes down. ELB solves this by balancing traffic and ensuring high availability.

**How ELB Works:** User sends request to ELB. ELB distributes request to multiple EC2 instances. If one instance is unhealthy, ELB skips it. Application continues running without downtime.

**Types of Load Balancer:** Application Load Balancer (ALB) is used for HTTP/HTTPS traffic. Network Load Balancer (NLB) is used for high performance and TCP traffic. Classic Load Balancer (CLB) is the older version.

**Example:** If 1000 users open your website, ELB distributes traffic across multiple servers. This prevents server crash and improves performance.

**Simple Understanding:** ELB = traffic distributor, It sends requests to multiple servers, Prevents overload

**Very Short Key Points:** ELB = load balancer, Distributes traffic, Improves availability, Works with EC2, Handles failure

## KMS (Key Management Service)
KMS is an AWS service used to create and manage encryption keys, enabling secure encryption and decryption of data across AWS services with controlled access.

It is used to create and manage encryption keys.

**In simple words,** KMS helps you lock (encrypt) and unlock (decrypt) your data securely.

**Why do we use KMS:** We use KMS to protect sensitive data. It helps in encrypting data in services like S3, EBS, and databases. It provides secure key storage and management. It avoids manually handling encryption keys.

**What problem does KMS solve:** Without KMS, managing encryption keys is difficult and risky. Keys can be lost or misused. KMS solves this by securely storing and controlling access to keys.

**How KMS Works:** You create a key in KMS. You use the key to encrypt data. When needed, the same key is used to decrypt data. Access to keys is controlled using IAM policies.

**Key Features:** Centralized key management. Automatic key rotation (for security). Integration with AWS services like S3, EBS, RDS. Fine-grained access control using IAM. Secure and highly available.

**Example:** If you store files in S3, you can enable encryption using KMS. Only users with permission can access and decrypt the data.

**Simple Understanding:** KMS = key manager, Encrypt = lock data, Decrypt = unlock data

**Key Points:** KMS = encryption key service, Used for data security, Controls access to keys, Works with S3, EBS

## CloudTrail
CloudTrail is an AWS service that records all API calls and user activities in an AWS account, helping in monitoring, auditing, and security analysis.

It is used to track and record all activities in your AWS account.

**In simple words,** CloudTrail is like a history log of everything happening in AWS.

**Why do we use CloudTrail:** We use CloudTrail to know who did what in AWS. It helps in security, auditing, and troubleshooting. It records actions like creating EC2, deleting S3, or changing IAM policies.

**What problem does CloudTrail solve:** Without CloudTrail, you cannot track changes or user actions. If something goes wrong, you won’t know who made the change. CloudTrail solves this by recording all API activities.

**How CloudTrail Works:** Whenever a user or service performs an action, CloudTrail records it. It logs details like user, time, service, and action performed. Logs are stored in S3 for analysis.

**Key Features:** Tracks all API calls and user activity. Stores logs securely in S3. Helps in auditing and compliance. Integrates with CloudWatch for alerts. Provides event history.

**Example:** If someone deletes an EC2 instance, CloudTrail shows who deleted it and when. This helps  in debugging and security analysis.

**Simple Understanding:** CloudTrail = activity history, Tracks user actions, Helps in auditing

**Key Points:** CloudTrail = tracking service, Records all actions, Stores logs in S3, Used for auditing

## Cloud Build
Cloud Build is a fully managed CI/CD service from Google Cloud that automates building, testing, and deploying applications whenever code changes are made.

Cloud Build is a CI/CD (Continuous Integration and Continuous Deployment) service from Google Cloud. It is used to build, test, and deploy applications automatically.

**In simple words,** Cloud Build helps you automate the process of building and deploying code.

**Why do we use Cloud Build:** We use Cloud Build to automate software development tasks. It helps in building code whenever changes are made. It reduces manual work and saves time. It ensures consistent and error-free deployments.

**What problem does Cloud Build solve:** Without Cloud Build, developers have to build and deploy code manually. This can cause errors and slow down development. Cloud Build solves this by automating the entire process.

**How Cloud Build Works:** Developer pushes code to repository (like GitHub). Cloud Build triggers automatically. It builds the application and runs tests. If successful, it deploys the application.

**Key Features:** Fully managed CI/CD service. Supports Docker container builds. Integrates with GitHub and repositories. Automates build, test, and deployment. Scalable and fast.

**Example:** When a developer pushes code, Cloud Build automatically builds a Docker image and deploys it to production.

**Simple Understanding:** Cloud Build = CI/CD tool, Build = compile code, Deploy = release application

**Key Points:** Cloud Build = CI/CD, Automates build & deploy, Triggered by code changes, Used with Docker
## AWS Config
AWS Config is a service that records and tracks configuration changes of AWS resources, helping in auditing, compliance, and troubleshooting.
It is used to track and record configuration changes of AWS resources.

**In simple words,** AWS Config helps you know how your resources are set up and what changes happen over time.

**Why do we use AWS Config:** We use AWS Config to monitor configuration changes. It helps in security, compliance, and auditing. It shows the history of resource settings. It ensures resources follow rules and policies.

**What problem does AWS Config solve:** Without AWS Config, you cannot track configuration changes of resources. If something breaks, you don’t know what changed. AWS Config solves this by recording configuration history and changes.

**How AWS Config Works:** AWS Config records the configuration of resources. It tracks any changes made to resources. It stores this data for review. It checks rules to see if resources are compliant.

**Key Features:** Tracks configuration history. Shows resource relationships. Supports compliance rules (like security checks). Stores data for auditing.

**Integrates with CloudTrail and CloudWatch.**

**Example:** If someone changes a security group rule, AWS Config records the change. You can see what changed, when, and who made the change.

**Simple Understanding:** AWS Config = configuration tracker, Tracks settings, Shows history, Checks compliance

**Key Points:** AWS Config = configuration tracking, Records changes, Helps in compliance, Works with CloudTrail


Amazon Web Services CloudFront is a CDN service provided by AWS. and CDN means Content Delivery Network. CloudFront is mainly used to deliver website content, images, videos, APIs, CSS files, JavaScript files, and application data to users very fast from the nearest server location instead of sending everything from the main server every time.

Normally when a user opens a website, the request goes directly to the main application server. If the server is located very far from the user, the website becomes slow because the data needs to travel a long distance through the internet. CloudFront solves this problem by storing a cached copy of the content in multiple AWS edge locations across the world. Edge locations are small AWS servers located in different countries and cities.

For example, imagine your application server is running in Mumbai and a user opens the website from Bangalore. Without CloudFront, the request goes directly to Mumbai every time. With CloudFront, the content is already cached in the nearest edge location near Bangalore, so the user gets the data faster with low latency.

CloudFront works like a middle layer between users and backend servers. Users send requests to CloudFront first, then CloudFront checks whether the content is already available in cache. If the content is available, it sends the response immediately from the edge location. If the content is not available, CloudFront fetches it from the origin server, stores it in cache, and sends it to the user.

Origin server means the actual backend source where the original content exists. The origin can be an Amazon S3 bucket, EC2 instance, Load Balancer, Kubernetes application, or any external web server.

In real-world projects, CloudFront is commonly used when applications have users from different locations and the company wants fast performance. It is heavily used for e-commerce websites, OTT platforms like video streaming, gaming applications, banking applications, APIs, static websites, and large enterprise applications.

Suppose a company uploads product images in S3 and millions of users open the website daily. If every image request goes directly to S3, the response may become slow and expensive. So the company places CloudFront in front of S3. Now CloudFront caches the images in edge locations and users receive images faster while reducing load on S3.

CloudFront is also used for video streaming. When users watch videos, CloudFront delivers video chunks from nearby edge locations instead of downloading everything from the main server. This improves buffering speed and user experience.

In DevOps and microservice projects, CloudFront is often used together with Load Balancer, API Gateway, Kubernetes, and S3. A common architecture is Users → CloudFront → Load Balancer → Kubernetes Pods/Application Servers.

One important reason companies use CloudFront is security. CloudFront supports HTTPS, SSL certificates, AWS Shield for DDoS protection, and integration with AWS WAF to block malicious traffic. This helps protect applications from attacks.

CloudFront also reduces backend traffic because repeated requests are served from cache instead of reaching the application server every time. This reduces CPU usage, bandwidth usage, and infrastructure cost.

Another important concept in CloudFront is cache expiration. CloudFront stores data for a specific time called TTL (Time To Live). Until TTL expires, users receive cached data. After expiration, CloudFront fetches updated content from the origin again.

For example, if you update a website logo in S3, users may still see the old logo because CloudFront cached it earlier. To solve this, companies perform cache invalidation, which removes old cached content from edge locations.

Simple definition of CloudFront:

“CloudFront is an AWS CDN service used to deliver application content to users quickly, securely, and with low latency using globally distributed edge locations.”

Simple real-world understanding:

“CloudFront is like storing copies of your application content in many nearby locations around the world so users can access data faster without always contacting the main server.”




