# DevOps
DevOps is a methodology that combines development and operations to deliver applications faster, safely, and efficiently through automation, collaboration, and continuous delivery.

Word	Meaning: Development:	Building application, Operations:	Managing infrastructure/deployment, DevOps:	Working together with automation

### Main Goals of DevOps

- Faster Delivery:	Quick deployments
- Automation:	Reduce manual work
- Collaboration:	Dev + Ops work together
- Reliability:	Stable applications
- Continuous Delivery:	Frequent releases

## DevOps lifecycle
DevOps lifecycle is the complete process used to develop, build, test, deploy, monitor, and maintain an application continuously and efficiently. The main goal of DevOps is to improve collaboration between development and operations teams so software can be delivered faster, more reliably, and with fewer errors.

The DevOps lifecycle normally works in a continuous loop because applications are continuously updated, monitored, and improved.

Planning phase is the first stage where teams gather requirements, discuss features, create tasks, and plan releases. Tools like Jira are commonly used for tracking work.

Development phase is where developers write application code using programming languages and store the code in repositories like [GitHub](https://github.com?utm_source=chatgpt.com) or [GitLab](https://gitlab.com?utm_source=chatgpt.com). Version control using Git helps teams track changes and collaborate safely.

Build phase starts after developers push code. CI/CD tools automatically compile code, install dependencies, package the application, and create artifacts like Docker images. Tools commonly used are Jenkins, GitHub Actions, or GitLab CI/CD.

Testing phase validates whether the application works correctly. Automated tests like unit testing, integration testing, security testing, and performance testing are executed to reduce manual effort and catch bugs early.

Release phase prepares the application for deployment. The release is approved, versioned, and made ready for production environments.

Deployment phase deploys the application into servers, cloud platforms, containers, or Kubernetes clusters. DevOps engineers ensure deployment happens smoothly with minimal downtime. Deployment strategies like rolling updates, blue-green deployment, and canary deployment are commonly used.

Operations phase focuses on maintaining the infrastructure, servers, networking, scaling, security, backups, and application availability. DevOps engineers continuously ensure systems are stable and healthy.

Monitoring phase continuously tracks application health, server resources, logs, user traffic, and errors using monitoring tools like Prometheus and Grafana. If issues occur, alerts are generated.

Feedback phase collects feedback from monitoring systems, users, customers, and teams. Based on this feedback, improvements and fixes are planned again, and the lifecycle continues.

Simple DevOps lifecycle flow:

Plan → Develop → Build → Test → Release → Deploy → Operate → Monitor → Feedback → Repeat

Real-world example:

A developer fixes a bug and pushes code to GitHub. CI/CD pipeline automatically builds the application, runs tests, creates a Docker image, and deploys it into Kubernetes. Monitoring tools then check whether the application is healthy. If errors are detected, alerts are sent to the DevOps team for troubleshooting.

Simple definition:

DevOps lifecycle is a continuous process of planning, developing, testing, deploying, monitoring, and improving applications using automation and collaboration between development and operations teams.


## What DevOps Engineers Store in Git
| DevOps File        | Purpose                |
| ------------------ | ---------------------- |
| Dockerfile         | Container build        |
| Jenkinsfile        | CI/CD pipeline         |
| Kubernetes YAML    | Deployment             |
| Terraform code     | Infrastructure         |
| Ansible playbooks  | Automation             |
| Helm charts        | K8s package management |
| Monitoring configs | Prometheus/Grafana     |
| Shell scripts      | Automation             |

## Why DevOps Engineers Must Know Git
Modern DevOps is based on: Infrastructure as Code + Automation + CI/CD + Collaboration. All these things are stored in Git repositories.
| Reason                  | Explanation                               |
| ----------------------- | ----------------------------------------- |
| CI/CD pipelines use Git | Jenkins/GitHub Actions pull code from Git |
| Infrastructure tracking | Terraform/K8s configs version controlled  |
| Rollback changes        | Restore old infrastructure configs        |
| Collaboration           | Multiple DevOps engineers work together   |
| GitOps                  | ArgoCD deploys directly from Git          |
| Automation              | Changes trigger deployments automatically |
| Audit tracking          | Know who changed infrastructure           |

Example Without Git: Suppose DevOps engineer changes: Kubernetes deployment, Terraform infrastructure

Without Git: No history, No rollback, No collaboration, No tracking. This becomes risky in production.
