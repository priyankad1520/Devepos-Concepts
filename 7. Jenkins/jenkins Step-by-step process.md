# Jenkins Commands Step-by-Step Process for DevOps Engineer

Jenkins is a CI/CD tool used for:

* Build automation
* Continuous Integration (CI)
* Continuous Deployment (CD)
* Running pipelines
* Automating testing and deployments

---

# 1. Check Java Version

Jenkins requires Java.

```bash
java -version
```

### Why We Use This

Checks whether Java is installed.

---

# 2. Install Java (Ubuntu)

```bash
sudo apt update
sudo apt install openjdk-17-jdk -y
```

---

# 3. Install Jenkins

## Add Jenkins Repository Key

```bash
curl -fsSL https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key | sudo tee \
  /usr/share/keyrings/jenkins-keyring.asc > /dev/null
```

---

## Add Jenkins Repository

```bash
echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] \
  https://pkg.jenkins.io/debian-stable binary/ | sudo tee \
  /etc/apt/sources.list.d/jenkins.list > /dev/null
```

---

## Install Jenkins

```bash
sudo apt update
sudo apt install jenkins -y
```

---

# 4. Start Jenkins Service

```bash
sudo systemctl start jenkins
```

### Why We Use This

Starts Jenkins server.

---

# 5. Enable Jenkins at Boot

```bash
sudo systemctl enable jenkins
```

### Why We Use This

Automatically starts Jenkins after reboot.

---

# 6. Check Jenkins Status

```bash
sudo systemctl status jenkins
```

### What You See

* active (running)
* failed
* stopped

---

# 7. Restart Jenkins

```bash
sudo systemctl restart jenkins
```

### Why We Use This

Used after:

* Plugin installation
* Configuration changes
* Jenkinsfile updates

---

# 8. Stop Jenkins

```bash
sudo systemctl stop jenkins
```

---

# 9. Jenkins Default Port

```bash
8080
```

### Access Jenkins

```text
http://server-ip:8080
```

---

# 10. Get Jenkins Initial Password

```bash
sudo cat /var/lib/jenkins/secrets/initialAdminPassword
```

### Why We Use This

Unlock Jenkins first time.

---

# 11. Jenkins Home Directory

```bash
/var/lib/jenkins
```

### Important Jenkins Files

| Path                 | Purpose        |
| -------------------- | -------------- |
| /var/lib/jenkins     | Jenkins home   |
| /etc/default/jenkins | Jenkins config |
| /var/log/jenkins     | Jenkins logs   |

---

# 12. View Jenkins Logs

## Real-Time Logs

```bash
sudo journalctl -u jenkins -f
```

## Jenkins Log File

```bash
sudo tail -f /var/log/jenkins/jenkins.log
```

### Why We Use This

Troubleshooting Jenkins issues.

---

# 13. Check Jenkins Port

```bash
netstat -tulnp | grep 8080
```

OR

```bash
ss -tulnp | grep 8080
```

---

# 14. Open Firewall Port

```bash
sudo ufw allow 8080
```

---

# 15. Jenkins CLI Commands

## Download Jenkins CLI

```bash
wget http://server-ip:8080/jnlpJars/jenkins-cli.jar
```

---

## Check Jenkins Version

```bash
java -jar jenkins-cli.jar -s http://server-ip:8080/ version
```

---

# 16. Create Jenkins Job Using CLI

```bash
java -jar jenkins-cli.jar -s http://server-ip:8080/ create-job myjob < config.xml
```

---

# 17. Build Jenkins Job

```bash
java -jar jenkins-cli.jar -s http://server-ip:8080/ build myjob
```

---

# 18. Get Jenkins Job List

```bash
java -jar jenkins-cli.jar -s http://server-ip:8080/ list-jobs
```

---

# 19. Install Plugins from CLI

```bash
java -jar jenkins-cli.jar -s http://server-ip:8080/ install-plugin git
```

---

# 20. Safe Restart Jenkins

```bash
java -jar jenkins-cli.jar -s http://server-ip:8080/ safe-restart
```

### Why We Use This

Waits for running jobs to finish before restart.

---

# 21. Backup Jenkins

## Backup Jenkins Home

```bash
sudo tar -czvf jenkins-backup.tar.gz /var/lib/jenkins
```

### Why We Use This

Backup:

* Jobs
* Plugins
* Configurations
* Credentials

---

# 22. Restore Jenkins

```bash
sudo tar -xzvf jenkins-backup.tar.gz -C /
```

---

# 23. Change Jenkins Port

## Edit Configuration

```bash
sudo nano /etc/default/jenkins
```

Change:

```text
HTTP_PORT=8080
```

Example:

```text
HTTP_PORT=9090
```

---

## Restart Jenkins

```bash
sudo systemctl restart jenkins
```

---

# 24. Jenkins Agent Commands

## Connect Agent

```bash
java -jar agent.jar -jnlpUrl http://server-ip:8080/computer/agent/slave-agent.jnlp -secret XXXXX -workDir "/home/jenkins"
```

### Why We Use Agents

Run builds on multiple servers.

---

# 25. Jenkins Plugin Management

## List Plugins

```bash
ls /var/lib/jenkins/plugins
```

---

# 26. Jenkins Pipeline Commands

## Validate Jenkinsfile

Usually done inside pipeline execution.

---

## Run Pipeline

```groovy
pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                sh 'echo Hello Jenkins'
            }
        }
    }
}
```

---

# 27. Jenkinsfile Basic Commands

## Print Current Directory

```groovy
sh 'pwd'
```

---

## List Files

```groovy
sh 'ls -l'
```

---

## Run Docker Command

```groovy
sh 'docker ps'
```

---

## Run Kubernetes Command

```groovy
sh 'kubectl get pods'
```

---

# 28. Jenkins Environment Variables

## Print Variables

```groovy
sh 'env'
```

---

## Common Variables

| Variable     | Purpose           |
| ------------ | ----------------- |
| BUILD_NUMBER | Build ID          |
| JOB_NAME     | Jenkins job name  |
| WORKSPACE    | Jenkins workspace |
| BUILD_URL    | Build URL         |

---

# 29. Jenkins Workspace

## Workspace Location

```bash
/var/lib/jenkins/workspace
```

---

# 30. Clean Workspace

```groovy
cleanWs()
```

### Why We Use This

Removes old build files.

---

# 31. Jenkins with GitHub

## Clone Repository in Pipeline

```groovy
git 'https://github.com/user/project.git'
```

---

# 32. Jenkins with Docker

## Build Docker Image

```groovy
sh 'docker build -t myapp .'
```

## Run Container

```groovy
sh 'docker run -d -p 80:80 myapp'
```

---

# 33. Jenkins with Kubernetes

## Deploy Application

```groovy
sh 'kubectl apply -f deployment.yaml'
```

---

# 34. Jenkins with Terraform

## Terraform Init

```groovy
sh 'terraform init'
```

## Terraform Plan

```groovy
sh 'terraform plan'
```

## Terraform Apply

```groovy
sh 'terraform apply -auto-approve'
```

---

# 35. Jenkins with Maven

## Build Java Application

```groovy
sh 'mvn clean install'
```

---

# 36. Jenkins with SonarQube

## Code Scan

```groovy
sh 'sonar-scanner'
```

---

# 37. Jenkins with Trivy

## Scan Docker Image

```groovy
sh 'trivy image nginx'
```

---

# 38. Jenkins Common Troubleshooting Commands

## Check Disk Space

```bash
df -h
```

---

## Check Memory Usage

```bash
free -m
```

---

## Check CPU Usage

```bash
top
```

---

## Check Running Processes

```bash
ps -ef | grep jenkins
```

---

# 39. Common Jenkins Errors and Solutions

| Error                     | Solution             |
| ------------------------- | -------------------- |
| Jenkins not starting      | Check Java           |
| Port 8080 busy            | Change port          |
| Build failed              | Check logs           |
| Permission denied         | Fix file permissions |
| Git authentication failed | Add credentials      |
| Disk full                 | Clean workspace      |

---

# 40. Real-Time Jenkins Workflow in Company

# Step 1: Developer Pushes Code

```bash
git push origin main
```

↓

# Step 2: GitHub Webhook Triggers Jenkins

↓

# Step 3: Jenkins Pulls Code

```groovy
git 'repo-url'
```

↓

# Step 4: Build Application

```groovy
sh 'mvn clean install'
```

↓

# Step 5: Build Docker Image

```groovy
sh 'docker build -t app .'
```

↓

# Step 6: Push Docker Image

```groovy
sh 'docker push app'
```

↓

# Step 7: Deploy to Kubernetes

```groovy
sh 'kubectl apply -f deployment.yaml'
```

↓

# Step 8: Monitor Application

Using:

* Prometheus
* Grafana

---

# Important Jenkins Commands Used Daily

| Command                  | Purpose         |
| ------------------------ | --------------- |
| systemctl start jenkins  | Start Jenkins   |
| systemctl status jenkins | Check status    |
| journalctl -u jenkins -f | View logs       |
| restart jenkins          | Restart service |
| docker build             | Build image     |
| kubectl apply            | Deploy app      |
| terraform apply          | Create infra    |
| mvn clean install        | Build Java app  |

---

# Jenkins Architecture Simple Analogy

```text
Developer → GitHub → Jenkins → Docker → Kubernetes → Users
```

---

# Jenkins Interview Important Topics

| Topic                       | Importance     |
| --------------------------- | -------------- |
| Jenkins Pipeline            | Very Important |
| Declarative Pipeline        | Important      |
| Jenkinsfile                 | Important      |
| CI/CD                       | Very Important |
| Plugins                     | Important      |
| Agents/Nodes                | Important      |
| Webhooks                    | Important      |
| Integration with Docker/K8s | Very Important |
