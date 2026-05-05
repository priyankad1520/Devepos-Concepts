# Python for DevOps Full Explanation

Python is one of the most widely used programming languages in DevOps because it is simple, powerful, and excellent for automation.

Python helps DevOps Engineers automate repetitive tasks, manage infrastructure, interact with APIs, monitor systems, handle cloud operations, and build CI/CD automation scripts.

Python is heavily used with Linux, Cloud Computing, Kubernetes, Docker, Terraform, Ansible, Jenkins, Monitoring Tools, and APIs.

## Why Python is Important for DevOps

Python is easy to learn and read.

Python supports automation very efficiently.

Python works well on Linux servers.

Python has huge libraries for cloud, networking, APIs, automation, and monitoring.

Python integrates with DevOps tools easily.

Python reduces manual operational work.

Python improves infrastructure management and scalability.

## Where Python is Used in DevOps

Infrastructure automation.

CI/CD pipeline automation.

Server management.

Cloud automation.

Log analysis.

Monitoring and alerting.

Kubernetes automation.

Docker automation.

API integration.

Configuration management.

File processing and reporting.

## Python Basics for DevOps

## Variables

Variables store data values.

Example:

```python id="jlwm1a"
server_name = "web-server"
cpu_usage = 75
```

## Data Types

### String

Stores text values.

```python id="’wini2b"
name = "Priyanka"
```

### Integer

Stores whole numbers.

```python id="’wini3c"
port = 8080
```

### Float

Stores decimal numbers.

```python id="’wini4d"
memory = 4.5
```

### Boolean

Stores True or False values.

```python id="’wini5e"
status = True
```

## Input and Output

Take user input:

```python id="’wini6f"
name = input("Enter name: ")
```

Display output:

```python id="’wini7g"
print(name)
```

## Conditional Statements

Used for decision-making automation.

Example:

```python id="’wini8h"
cpu = 85

if cpu > 80:
    print("High CPU Usage")
else:
    print("CPU Normal")
```

## Loops

Loops repeat tasks automatically.

### For Loop

```python id="’wini9i"
servers = ["web1", "web2", "web3"]

for server in servers:
    print(server)
```

### While Loop

```python id="’wini0j"
count = 1

while count <= 5:
    print(count)
    count += 1
```

## Functions

Functions organize reusable code blocks.

Example:

```python id="’wini1k"
def check_server():
    print("Server Running")

check_server()
```

## File Handling

Read file:

```python id="’wini2l"
file = open("log.txt", "r")
print(file.read())
```

Write file:

```python id="’wini3m"
file = open("output.txt", "w")
file.write("DevOps Automation")
```

## Exception Handling

Handles errors gracefully.

Example:

```python id="’wini4n"
try:
    print(10 / 0)

except:
    print("Error Occurred")
```

## Modules

Modules provide reusable functionality.

Import module:

```python id="’wini5o"
import os
```

## Important Python Modules for DevOps

## OS Module

Used for interacting with operating system.

Example:

```python id="’wini6p"
import os

os.system("df -h")
```

## Subprocess Module

Executes Linux commands from Python.

Example:

```python id="’wini7q"
import subprocess

subprocess.run(["ls", "-l"])
```

## Sys Module

Used for system-level operations.

Example:

```python id="’wini8r"
import sys

print(sys.version)
```

## JSON Module

Used for handling JSON API data.

Example:

```python id="’wini9s"
import json

data = {"name": "Priyanka"}

print(json.dumps(data))
```

## Requests Module

Used for API communication.

Install requests module:

```bash id="’wini0t"
pip install requests
```

Example API request:

```python id="’wini1u"
import requests

response = requests.get("https://api.github.com")

print(response.status_code)
```

## YAML Module

Used for Kubernetes and Ansible YAML processing.

Install YAML module:

```bash id="’wini2v"
pip install pyyaml
```

Example YAML read:

```python id="’wini3w"
import yaml

with open("config.yaml") as file:
    data = yaml.safe_load(file)

print(data)
```

## Automation in DevOps Using Python

Python automates repetitive DevOps tasks.

Examples:

Server health monitoring.

Disk cleanup automation.

Backup automation.

Log monitoring.

CI/CD automation.

Infrastructure deployment.

Cloud resource management.

## Python Script for Disk Usage Monitoring

```python id="’wini4x"
import shutil

total, used, free = shutil.disk_usage("/")

print("Free Space:", free)
```

## Python Script for Ping Check

```python id="’wini5y"
import os

response = os.system("ping -c 1 google.com")

if response == 0:
    print("Server Reachable")
else:
    print("Server Down")
```

## Python with Linux

Python works closely with Linux systems.

Python automates Linux administration tasks.

Python executes shell commands, monitors processes, and manages files.

## Python with Docker

Python automates Docker container management.

Install Docker SDK:

```bash id="’wini6z"
pip install docker
```

Example Docker container list:

```python id="’wini7a"
import docker

client = docker.from_env()

containers = client.containers.list()

for container in containers:
    print(container.name)
```

## Python with Kubernetes

Python interacts with Kubernetes clusters using Kubernetes Python Client.

Install Kubernetes client:

```bash id="’wini8b"
pip install kubernetes
```

Example Kubernetes Pod list:

```python id="’wini9c"
from kubernetes import client, config

config.load_kube_config()

v1 = client.CoreV1Api()

pods = v1.list_pod_for_all_namespaces()

for pod in pods.items:
    print(pod.metadata.name)
```

## Python with AWS Cloud

Python automates AWS services using Boto3 SDK.

Install Boto3:

```bash id="’wini0d"
pip install boto3
```

Example AWS S3 buckets list:

```python id="’wini1e"
import boto3

s3 = boto3.client('s3')

response = s3.list_buckets()

for bucket in response['Buckets']:
    print(bucket['Name'])
```

## Python with APIs

DevOps tools expose APIs for automation.

Python communicates with Jenkins, GitHub, Kubernetes, Docker, and cloud APIs.

## Python with Jenkins

Python triggers Jenkins jobs using APIs.

## Python with GitHub

Python automates repository management and CI/CD workflows.

## Python with Monitoring

Python collects system metrics and monitoring data.

Python integrates with Prometheus and monitoring systems.

## Python Virtual Environment

Virtual Environment isolates Python project dependencies.

Create virtual environment:

```bash id="’wini2f"
python3 -m venv venv
```

Activate environment:

```bash id="’wini3g"
source venv/bin/activate
```

## Pip

Pip installs Python packages.

Install package:

```bash id="’wini4h"
pip install requests
```

List installed packages:

```bash id="’wini5i"
pip list
```

## Logging in Python

Logging helps troubleshoot automation scripts.

Example logging:

```python id="’wini6j"
import logging

logging.basicConfig(level=logging.INFO)

logging.info("Server Started")
```

## Python Best Practices for DevOps

Write modular scripts.

Use functions and reusable code.

Handle exceptions properly.

Store secrets securely.

Use logging for troubleshooting.

Avoid hardcoded credentials.

Use version control with Git.

Test automation scripts before production use.

## Advantages of Python in DevOps

Simple and readable syntax.

Powerful automation capabilities.

Huge ecosystem of libraries.

Strong Linux and cloud support.

Easy API integration.

Works well with DevOps and cloud-native tools.

## Limitations of Python

Python may be slower than compiled languages.

Large automation systems may require better structure and optimization.

Dependency management can become complex in large projects.

## Python Workflow in DevOps

Developer writes Python automation script.

Script connects with Linux servers, APIs, or cloud platforms.

Python executes commands or API requests.

Automation tasks run automatically.

Logs and outputs are generated for monitoring and troubleshooting.

Infrastructure and applications are managed efficiently with reduced manual work.
