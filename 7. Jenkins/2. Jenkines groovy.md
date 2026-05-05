## Groovy
Groovy is a dynamic scripting language used in Jenkins pipelines. Its structure includes variables, lists, maps, conditions, loops, and functions. In DevOps, it is mainly used to define pipeline stages and automate build, test, and deployment processes.
- Key Points: Groovy is dynamic (no strict types). Used in Jenkins pipelines. Supports lists, maps, functions. Closures are important. Syntax is simple like scripting 
- Key Rule: Indentation = readability only. Curly braces {} = actual structure

indentation does not affect execution because Groovy uses curly braces for structure. However, proper indentation is recommended for readability and maintainability.

Why: Hard to read, Confusing for team members, Difficult to debug, Not industry standard { } 
- curly braces to define blocks, Not spaces like YAML
- Yes indentation does not important but when Team collaboration, Code reviews and Avoiding mistakes indentation used to understand the proper structure. 

**In a real DevOps pipeline**, Jenkins pulls code from GitHub, builds a Docker image, pushes it to a container registry like Docker Hub, and then deploys it to Kubernetes using kubectl commands. This process is defined using a Jenkinsfile written in Groovy.

- **Jenkins:** Jenkins is an open-source automation tool used for CI/CD. It helps automate build, test, and deployment processes.

- **Jenkins Pipeline:** A Jenkins pipeline is a set of automated steps written in Groovy that define the CI/CD workflow.

- **Jenkinsfile:** Jenkinsfile is a file written in Groovy that defines the pipeline structure (build, test, deploy stages).

## Types of Pipelines: 
Declarative Pipeline (easy, structured) and Scripted Pipeline (flexible, complex) 
### Declarative pipeline
Declarative pipeline uses a structured and simple syntax with predefined blocks like pipeline, stages, and steps, making it easy to read and maintain. Scripted pipeline uses pure Groovy code, providing more flexibility and control but is more complex. In most real-world scenarios, declarative pipelines are preferred unless advanced logic is required.

When to Use What?
- **Use Declarative:** Standard CI/CD pipelines, Easy maintenance and Team collaboration 
- **Use Scripted:** Complex conditions, Dynamic behavior  and Advanced logic

- **pipeline {}:** It is the main block that defines the entire Jenkins pipeline.
- **Agent:** Defines where the pipeline runs (like any node, docker, etc.) ex: agent any
- **Stages:** Stages divide pipeline into phases like Build, Test, Deploy.
- **Steps:** Steps contain actual commands executed in each stage.
- **Echo:** Used to print messages in Jenkins console.
- **Groovy in Jenkins:** Jenkins pipelines are written in Groovy language to automate tasks.
- **closure in Groovy:** A closure is a block of code that can be passed and executed.
``` def greet = { println "Hello" } ```
- **environment in Jenkins:** Used to define environment variables in pipeline.
```
environment {
  APP_ENV = "prod"
}
```
- **params:** Used to pass input parameters to pipeline.
- **post block:** Defines actions after pipeline execution (success, failure)
```
post {
  success {
    echo "Success"
  }
}
```

**How Jenkins connects with GitHub:** Using webhook or polling, Jenkins triggers pipeline when code is pushed.

**Webhook:** A webhook automatically triggers Jenkins when changes happen in GitHub.

How do you build Docker image in Jenkins?
```
stage('Build') {
  steps {
    sh 'docker build -t myapp .'
  }
}
How do you push Docker image: sh 'docker push myapp'
```
common pipeline stages: Build --> Test --> Deploy 

Focus on: Pipeline structure, Declarative vs Scripted, GitHub + Webhook, Docker integration 

Jenkins + Groovy = "Automating complete software lifecycle"

```
pipeline {
    agent any

    environment {
        APP_NAME = "my-java-app"
        DOCKER_IMAGE = "myrepo/my-java-app:latest"
    }

    tools {
        maven 'Maven3'
    }

    stages {
        stage('Clone Code') {
            steps {
                git 'https://github.com/user/java-project.git'
            }
        }

        stage('Build (Maven)') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('SonarQube Analysis') {
            steps {
                sh 'mvn sonar:sonar \
                -Dsonar.projectKey=myapp \
                -Dsonar.host.url=http://sonarqube:9000 \
                -Dsonar.login=SONAR_TOKEN'
            }
        }

        stage('Quality Gate') {
            steps {
                waitForQualityGate abortPipeline: true
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t $DOCKER_IMAGE .'
            }
        }

        stage('Trivy Scan') {
            steps {
                sh 'trivy image $DOCKER_IMAGE'
            }
        }

        stage('Push Docker Image') {
            steps {
                sh 'docker push $DOCKER_IMAGE'
            }
        }

        stage('Deploy to Kubernetes') {
            steps {
                sh 'kubectl apply -f deployment.yaml'
            }
        }
    }

    post {
        success {
            echo 'Pipeline Success '
        }
        failure {
            echo 'Pipeline Failed '
        }
    }
}
```
### Logging
Logging is the process of recording events, messages, and errors generated by an application or system. It is used for monitoring, debugging, and troubleshooting issues.
- **Logging** = recording events/messages about what is happening in a system or application
- **Logging means:** Writing information (messages) to a file or console to track system behavior
- **Why we use Logging:** Debug issues. Monitor application. Track errors. Understand flow 
- **Real Example:** When your app runs, it writes messages like: 

Application started --> Connecting to database --> Error: Connection failedThese messages = logs

### Types of Logs
1. Info Logs: Normal messages Server started successfully
2. Debug Logs: Detailed information (for developers) User ID: 123 logged in
3. Warning Logs: Something might go wrong Disk space is low
4. Error Logs: Something failedDatabase connection failed
5. Critical Logs: Serious issue Server crashed

Logging in Jenkins. Example:
```
echo "Build started"
sh "docker build -t myapp ."
Output in Jenkins console:
Build started
Step 1/5 : FROM python:3.9
...
This is logging
```
Logging in Real DevOps: Logs come from: Applications, Docker containers, Kubernetes pods, Servers 

Example Commands
- `docker logs container_id`
- `kubectl logs pod_name`

Where logs are stored: Files (/var/log/) --> Console output --> Logging tools 

Popular Logging Tools: ELK Stack (Elasticsearch, Logstash, Kibana), Grafana + Loki, CloudWatch (AWS) 

Without logs: You don’t know what happened, Hard to debug. With logs: Easy to find issues 

Docker logs and Kubernetes logs are used to monitor application runtime behavior, Git logs track code changes, Jenkins logs help debug CI/CD pipelines, and log files store system or application events. Each log type serves a different purpose in the DevOps lifecycle.

**1. Application Logs:** Logs generated by your app. `Example: User login success and Payment failed`

**2. Server Logs:** Web servers (Nginx, Apache)--> GET /index.html 200 OK

**3. System Logs:** OS-level logs --> /var/log/syslog

**4. Audit Logs:** Security-related logs  ✔ Who accessed system ✔ What action performed

**5. CI/CD Logs:** Jenkins, GitHub Actions logs

**6. Monitoring Logs From tools like:** Prometheus and CloudWatch 

**7. Security Logs:** Unauthorized access attempts

Real DevOps Flow. Example:
1.	App fails in Kubernetes 
2.	Check: `kubectl logs` or `Docker logs` 
3.	Check Jenkins logs (deployment issue) 
4.	Check Git logs (recent change) 
