# Docker Commands Step-by-Step Process for a DevOps Engineer

Docker is used by DevOps engineers for:

* Containerization
* Application deployment
* CI/CD pipelines
* Microservices
* Environment consistency
* Faster deployments

---

## 1. Install Docker
- Update Packages: `sudo apt update`
- Install Docker: `sudo apt install docker.io -y`
- Start Docker Service: `sudo systemctl start docker`
- Enable Docker at Boot: `sudo systemctl enable docker`
- Check Docker Version: `docker --version`

## 2. Verify Docker Installation
- Check Docker Service Status: `sudo systemctl status docker`
- Run Test Container: `docker run hello-world`
- What Happens?: Docker downloads and runs a test container.

## 3. Basic Docker Information Commands
- Check Docker System Information: `docker info`
- Check Docker Version: `docker version`

## 4. Docker Images Commands
- View Images: `docker images` OR `docker image ls`
-  Why We Use This: Shows downloaded Docker images.

## 5. Pull Image from Docker Hub
- Download Ubuntu Image: `docker pull ubuntu`
- Download Nginx Image:  `docker pull nginx`
- What Happens?: Downloads image from Docker Hub.

## 6. Run a Container
- Run Ubuntu Container: `docker run ubuntu`
- Run Interactive Container: `docker run -it ubuntu bash`

##### Options Explanation

| Option | Meaning          |
| ------ | ---------------- |
| -i     | Interactive mode |
| -t     | Terminal         |
| bash   | Open bash shell  |

## 7. View Running Containers
```bash
docker ps
```
- Why We Use This: Shows active/running containers.

## 8. View All Containers
```bash
docker ps -a
```
- Why We Use This. Shows: Running containers, Stopped containers

## 9. Stop Container
- Stop Using Container ID: `docker stop container_id`
- Example: `docker stop a1b2c3d4`

## 10. Start Container
```bash
docker start container_id
```

## 11. Restart Container
```bash
docker restart container_id
```
## 12. Remove Container
- Delete Stopped Container: `docker rm container_id`
- Force Remove Running Container: `docker rm -f container_id`

## 13. Remove Docker Image

```bash
docker rmi image_id

# Example:
docker rmi ubuntu
```
## 14. Run Container in Background

```bash
docker run -d nginx
```

#### Option Explanation

| Option | Meaning                  |
| ------ | ------------------------ |
| -d     | Detached mode/background |

## 15. Port Mapping
- Run Nginx on Port 80: docker run -d -p 80:80 nginx

#### Port Explanation

| Port      | Meaning           |
| --------- | ----------------- |
| First 80  | Host machine port |
| Second 80 | Container port    |

## 16. Name a Container

```bash
docker run -d --name mynginx nginx
```
Why We Use This: Easy container identification.

## 17. Execute Commands Inside Container
- Access Container Terminal: `docker exec -it mynginx bash` OR `docker exec -it container_id bash`

## 18. View Container Logs

```bash
docker logs container_id
```
- Live Logs: `docker logs -f container_id`
- Why DevOps Engineers Use This: Troubleshooting applications.

## 19. Inspect Container Details

```bash
docker inspect container_id
```
Shows: IP address, Network, Volumes, Configuration

## 20. Monitor Resource Usage
```bash
docker stats
```
Shows: CPU usage, Memory usage, Network usage

## 21. Copy Files Between Host and Container
- Host to Container: `docker cp file.txt container_id:/tmp`
- Container to Host: `docker cp container_id:/tmp/file.txt .`

## 22. Docker Volumes
- Create Volume: `docker volume create myvolume`
- View Volumes: `docker volume ls`
-  Use Volume: `docker run -d -v myvolume:/app nginx`
-   Why We Use Volumes: Persistent storage.

## 23. Docker Networks
- View Networks: `docker network ls`
- Create Network: `docker network create mynetwork`
- Run Container in Network: `docker run -d --network=mynetwork nginx`

# 24. Dockerfile Commands
- Create Dockerfile: `touch Dockerfile`

## 25. Common Dockerfile Instructions
Example Dockerfile

```dockerfile
FROM ubuntu

RUN apt update

RUN apt install nginx -y

COPY . /app

WORKDIR /app

EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]
```

# Dockerfile Instructions Explanation

| Instruction | Purpose               |
| ----------- | --------------------- |
| FROM        | Base image            |
| RUN         | Execute command       |
| COPY        | Copy files            |
| WORKDIR     | Set working directory |
| EXPOSE      | Open port             |
| CMD         | Start application     |

## 26. Build Docker Image

```bash
docker build -t myapp .
```
Options Explanation

| Option | Meaning           |
| ------ | ----------------- |
| -t     | Tag/name image    |
| .      | Current directory |

## 27. Run Custom Image

```bash
docker run -d -p 8080:80 myapp
```
## 28. Tag Docker Image

```bash
docker tag myapp username/myapp:v1
```

## 29. Login to Docker Hub

```bash
docker login
```
## 30. Push Image to Docker Hub

```bash
docker push username/myapp:v1
```

## 31. Docker Compose
- Create docker-compose.yml: `touch docker-compose.yml`
- Example Docker Compose File
```yaml
version: '3'

services:
  web:
    image: nginx
    ports:
      - "80:80"

  database:
    image: mysql
    environment:
      MYSQL_ROOT_PASSWORD: root
```

## 32. Start Docker Compose

```bash
docker-compose up -d
```
## 33. Stop Docker Compose

```bash
docker-compose down
```
## 34. View Docker Compose Containers

```bash
docker-compose ps
```

## 35. Clean Unused Docker Resources
- Remove Unused Containers: `docker container prune`
- Remove Unused Images: `docker image prune`
- Remove Everything Unused: `docker system prune -a`

## Real-Time Docker Workflow in DevOps

#### Step 1: Developer Pushes Code to GitHub

```bash
git push origin main
```
#### Step 2: Jenkins Pulls Code

#### Step 3: Build Docker Image

```bash
docker build -t ecommerce-app .
```
#### Step 4: Run Container

```bash
docker run -d -p 8080:80 ecommerce-app
```

#### Step 5: Push Image to Docker Hub

```bash
docker push company/ecommerce-app:v1
```
#### Step 6: Kubernetes Pulls Docker Image
Used in: Kubernetes, EKS, AKS, GKE

## Important Docker Commands Used Daily

| Command       | Purpose          |
| ------------- | ---------------- |
| docker pull   | Download image   |
| docker build  | Build image      |
| docker run    | Run container    |
| docker ps     | Check containers |
| docker logs   | View logs        |
| docker exec   | Access container |
| docker stop   | Stop container   |
| docker rm     | Remove container |
| docker images | View images      |
| docker push   | Upload image     |

---

## Common Docker Errors and Solutions

#### 1. Port Already in Use
- **Error:** `Bind for 0.0.0.0:80 failed`

#### Solution
```bash
# Check process using port:
sudo netstat -tulnp
# OR
sudo lsof -i :80
```

#### 2. Permission Denied

#### Solution
```bash
# Add user to docker group:
sudo usermod -aG docker $USER
```

#### 3. Container Exits Immediately
```bash
# Check Logs
docker logs container_id
```

#### 4. No Space Left on Device

#### Solution
```bash
# Clean unused resources:
docker system prune -a
```

#### 5. Image Not Found
#### Solution
```bash
# Pull image again:
docker pull nginx
```
### Docker Architecture

```text
User
 ↓
Docker CLI
 ↓
Docker Daemon
 ↓
Docker Engine
 ↓
Containers
```
### Docker vs Virtual Machine

| Docker           | Virtual Machine |
| ---------------- | --------------- |
| Lightweight      | Heavy           |
| Fast startup     | Slow startup    |
| Shares OS kernel | Separate OS     |
| Less memory      | More memory     |


## Simple Docker Workflow Diagram

```text
Developer Writes Code
        ↓
Create Dockerfile
        ↓
docker build
        ↓
Docker Image Created
        ↓
docker run
        ↓
Container Running
        ↓
Push Image to Docker Hub
        ↓
Deploy Using Kubernetes
```
