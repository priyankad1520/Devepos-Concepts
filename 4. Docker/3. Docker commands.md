# Docker Commands

Some of the most commonly used docker commands are 

1. docker images: Lists docker images on the host machine.

2. docker build: Builds image from Dockerfile.

3. docker run: Runs a Docker container. 

There are many arguments which you can pass to this command for example,

`docker run -d` -> Run container in background and print container ID
`docker run -p` -> Port mapping

use `docker run --help` to look into more arguments.

4. docker ps: Lists running containers on the host machine.

5. docker stop: Stops running container.

6. docker start: Starts a stopped container.

7. docker rm: Removes a stopped container.

8. docker rmi: Removes an image from the host machine.

9. docker pull: Downloads an image from the configured registry.

10. docker push: Uploads an image to the configured registry.

11. docker exec: Run a command in a running container.

12. docker network: Manage Docker networks such as creating and removing networks, and connecting containers to networks.
Here are **commonly used Docker commands in one-line format** (simple and interview-friendly):

---

##  Real-Time Docker Commands (DevOps Use Cases)

####  1. Run Application Container with Port Mapping
Runs Nginx in background and maps container port 80 to server port 80
```bash
docker run -d -p 80:80 nginx
```
---
####  2. Run Container with Custom Name
Assigns a readable name instead of container ID
```bash
docker run -d --name myapp nginx
```
---
####  3. Restart Policy (Important in Production)
Container auto-restarts if it crashes or server reboots
```bash
docker run -d --restart=always nginx
```
---
####  4. Mount Volume (Persistent Storage)
Data will not be lost even if container stops
```bash
docker run -d -v /host/data:/container/data nginx
```
---
####  5. Pass Environment Variables
Used for configuration like DB credentials
```bash
docker run -d -e ENV=prod nginx
```
---
###  6. Check Logs for Debugging
Real-time logs (very important in troubleshooting)
```bash
docker logs -f <container_id>
```
---
####  7. Execute Command Inside Container
Access running container (like SSH)
```bash
docker exec -it <container_id> /bin/bash
```
---
####  8. Clean Up Unused Resources
Removes unused images, containers, networks
```bash
docker system prune -a
```
---
####  9. Build Image from Dockerfile
Used in CI/CD pipelines
```bash
docker build -t myapp:v1 .
```
---
####  10. Push Image to Docker Hub
Share image with team or deployment
```bash
docker push myrepo/myapp:v1
```
---
####  11. Pull Image from Registry
Used in deployment servers
```bash
docker pull myrepo/myapp:v1
```
---
####  12. Create Custom Network
Allows container-to-container communication
```bash
docker network create mynetwork
```
---
####  13. Run Container in Custom Network
```bash
docker run -d --network=mynetwork nginx
```
---
####  14. Check Resource Usage
CPU, memory usage (monitoring)
```bash
docker stats
```
---
####  15. Inspect Container Details
Full JSON details (IP, config, mounts)
```bash
docker inspect <container_id>
```
---

👉 *"How do you debug a failed container?"*

You can answer:

1. `docker ps -a`
2. `docker logs <id>`
3. `docker inspect <id>`
4. `docker exec -it <id> /bin/bash`

# Complete Docker and Kubernetes Commands Guide

---

## **DOCKER COMMANDS**

### **1. Basic Docker Commands**

| Command | Purpose | Example |
|---------|---------|---------|
| `docker version` | Check Docker version | `docker version` |
| `docker info` | Display system info | `docker info` |
| `docker help` | Get help | `docker help` |
| `docker login` | Login to registry | `docker login` |
| `docker logout` | Logout from registry | `docker logout` |

---

### **2. Docker Image Commands**

| Command | Purpose | Example |
|---------|---------|---------|
| `docker image ls` | List all images | `docker image ls` |
| `docker images` | List images (short) | `docker images` |
| `docker pull` | Download image | `docker pull ubuntu:latest` |
| `docker push` | Upload image | `docker push myrepo/myimage:1.0` |
| `docker build` | Build image from Dockerfile | `docker build -t myapp:1.0 .` |
| `docker tag` | Tag an image | `docker tag myapp:1.0 myrepo/myapp:1.0` |
| `docker inspect` | Image details | `docker inspect nginx` |
| `docker history` | Image layers | `docker history ubuntu:latest` |
| `docker image rm` | Remove image | `docker image rm nginx` |
| `docker rmi` | Remove image (short) | `docker rmi myapp:1.0` |
| `docker image prune` | Remove unused images | `docker image prune -a` |

---

### **3. Docker Container Commands**

| Command | Purpose | Example |
|---------|---------|---------|
| `docker run` | Create and start container | `docker run -d -p 8080:80 nginx` |
| `docker create` | Create container (no start) | `docker create --name my-app myimage` |
| `docker start` | Start stopped container | `docker start my-container` |
| `docker stop` | Stop running container | `docker stop my-container` |
| `docker restart` | Restart container | `docker restart my-container` |
| `docker kill` | Force stop container | `docker kill my-container` |
| `docker pause` | Pause container | `docker pause my-container` |
| `docker unpause` | Resume container | `docker unpause my-container` |
| `docker rm` | Remove container | `docker rm my-container` |
| `docker ls` | List containers (short) | `docker ls` |
| `docker container ls` | List running containers | `docker container ls` |
| `docker container ls -a` | List all containers | `docker container ls -a` |
| `docker ps` | List running (legacy) | `docker ps` |
| `docker ps -a` | List all (legacy) | `docker ps -a` |
| `docker rename` | Rename container | `docker rename old-name new-name` |

### **docker run Examples**

```bash
# Basic run
docker run ubuntu echo "Hello World"

# Run in background (detached)
docker run -d --name my-nginx -p 8080:80 nginx

# Run with environment variables
docker run -d -e DB_HOST=localhost -e DB_USER=admin postgres

# Run with volume mount
docker run -d -v /host/path:/container/path nginx

# Run with multiple ports
docker run -d -p 8080:80 -p 8443:443 nginx

# Run with memory/CPU limits
docker run -d --memory="512m" --cpus="1" nginx

# Run with custom name
docker run -d --name web-server nginx

# Run in interactive mode
docker run -it ubuntu /bin/bash

# Run with restart policy
docker run -d --restart always nginx
```

---

### **4. Docker Inspection & Debugging**

| Command | Purpose | Example |
|---------|---------|---------|
| `docker inspect` | View detailed container info | `docker inspect my-container` |
| `docker container inspect` | Container details | `docker container inspect my-container` |
| `docker logs` | View container logs | `docker logs my-container` |
| `docker logs -f` | Follow logs (real-time) | `docker logs -f my-container` |
| `docker logs --tail` | Last N lines | `docker logs --tail 50 my-container` |
| `docker exec` | Run/Execute command in container | `docker exec -it my-container bash` |
| `docker attach` | Connect to container | `docker attach my-container` |
| `docker top` | Check Running processes | `docker top my-container` |
| `docker stats` | View Container resource usage | `docker stats` |
| `docker events` | Check container events/ Real-time events | `docker events` or `docker events --filter container=my-container`|

---

### **5. Docker File & Data Management**

| Command | Purpose | Example |
|---------|---------|---------|
| `docker cp` | Copy files | `docker cp container:/path/file ./local/` |
| `docker volume ls` | List volumes | `docker volume ls` |
| `docker volume create` | Create volume | `docker volume create my-volume` |
| `docker volume inspect` | Volume details | `docker volume inspect my-volume` |
| `docker volume rm` | Remove volume | `docker volume rm my-volume` |
| `docker volume prune` | Remove unused volumes | `docker volume prune` |

---

### **6. Docker Compose Commands**

| Command | Purpose | Example |
|---------|---------|---------|
| `docker-compose up` | Start services | `docker-compose up -d` |
| `docker-compose down` | Stop services | `docker-compose down` |
| `docker-compose ps` | List services | `docker-compose ps` |
| `docker-compose logs` | View logs | `docker-compose logs -f` |
| `docker-compose exec` | Run command | `docker-compose exec service-name bash` |
| `docker-compose restart` | Restart services | `docker-compose restart` |
| `docker-compose build` | Build images | `docker-compose build` |
| `docker-compose pull` | Pull images | `docker-compose pull` |

---

## **DOCKER NETWORK COMMANDS**

### **1. Docker Network Management**

| Command | Purpose | Example |
|---------|---------|---------|
| `docker network ls` | List all networks | `docker network ls` |
| `docker network create` | Create network | `docker network create my-network` |
| `docker network inspect` | Network details | `docker network inspect my-network` |
| `docker network connect` | Connect container to network | `docker network connect my-network my-container` |
| `docker network disconnect` | Disconnect container from network | `docker network disconnect my-network my-container` |
| `docker network rm` | Remove network | `docker network rm my-network` |
| `docker network prune` | Remove unused networks | `docker network prune` |

### **Docker Network Types**

```bash
# Bridge Network (default, isolated)
docker network create --driver bridge my-bridge-network

# Host Network (uses host's network)
docker run --network host nginx

# Overlay Network (multi-host, for Swarm/K8s)
docker network create --driver overlay my-overlay-network

# None Network (no networking)
docker run --network none ubuntu

Example:
# Run container on specific network
docker run -d --name app1 --network my-app-network myimage

# Run container with static IP
docker run -d --network my-custom-network --ip 172.20.0.2 nginx
```

### **Container-to-Container Communication**

```bash
# Create network
docker network create backend

# Run containers on the same network
docker run -d --name db --network backend postgres
docker run -d --name app --network backend myapp

# They can now communicate using container names as hostnames
# From app: ping db (works!)
docker exec app ping db
```

---



## **Quick Reference Cheat Sheet**

### **Docker Quick Commands**

```bash
# Images
docker pull ubuntu
docker build -t myapp:1.0 .
docker images
docker rmi myapp:1.0

# Containers
docker run -d -p 8080:80 --name web nginx
docker ps -a
docker logs -f web
docker exec -it web bash
docker stop web
docker rm web

# Networks
docker network create my-net
docker network ls
docker network connect my-net container-name
docker network inspect my-net

# Compose
docker-compose up -d
docker-compose ps
docker-compose logs -f
docker-compose down
```

### **Kubernetes Quick Commands**

```bash
# Pods
kubectl get pods
kubectl describe pod my-pod
kubectl logs -f my-pod
kubectl exec -it my-pod -- bash
kubectl delete pod my-pod

# Deployments
kubectl get deploy
kubectl scale deploy my-app --replicas=5
kubectl set image deploy/my-app app=myimg:2.0
kubectl rollout undo deploy/my-app

# Services
kubectl get svc
kubectl expose deploy my-app --port=80
kubectl port-forward svc/my-service 8080:80

# Networking
kubectl get netpol
kubectl apply -f network-policy.yaml
kubectl get ingress
kubectl exec -it my-pod -- nslookup my-service
```
