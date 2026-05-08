In Kubernetes, NGINX is used in many places because it is lightweight, fast, and handles HTTP traffic very efficiently.

NGINX is mainly used as a web server, reverse proxy, load balancer, ingress controller, and API gateway inside the Kubernetes cluster.

---

## 1. NGINX as a Web Server

Sometimes applications like React, Angular, or static websites are packaged inside an NGINX container and deployed as a Pod.

Example:

```bash id="isjlwm"
docker run nginx
```

In Kubernetes:

```yaml id="g5u6g8"
containers:
  - name: nginx
    image: nginx
```

Here NGINX serves:

* HTML files
* CSS
* JavaScript
* Static content

---

## 2. NGINX as Reverse Proxy

In microservices architecture, users should not directly access backend services.

NGINX sits in front of applications and forwards requests to correct services.

Flow:

```text id="qqhrrv"
User Request → NGINX → Backend Application
```

Example:

```text id="5mmb8g"
User → NGINX → Python App
               → NodeJS App
               → Java App
```

NGINX hides backend services and manages traffic routing.

---

## 3. NGINX as Load Balancer

If multiple Pods of same application exist, NGINX distributes traffic among them.

Example:

```text id="h34p4l"
User Request
      ↓
    NGINX
   ↙  ↓  ↘
Pod1 Pod2 Pod3
```

Benefits:

* Prevents one Pod from overload
* Improves availability
* Improves scalability

---

## 4. NGINX Ingress Controller (Very Important in Kubernetes)

This is the most common use of NGINX in Kubernetes.

Kubernetes Service exposes applications internally, but external traffic needs routing rules.

Ingress + NGINX Controller manages external HTTP/HTTPS traffic.

Flow:

```text id="pr11xn"
Internet → NGINX Ingress Controller → Kubernetes Services → Pods
```

Example:

```text id="a6b4i0"
example.com/api  → API Service
example.com/app  → Frontend Service
```

NGINX Ingress Controller handles:

* URL routing
* SSL/TLS
* HTTPS termination
* Load balancing
* Path-based routing
* Host-based routing

---

## 5. NGINX for SSL/TLS Termination

NGINX decrypts HTTPS traffic before sending it to backend Pods.

Flow:

```text id="7ql6m7"
HTTPS Request → NGINX → HTTP → Backend Pods
```

Benefits:

* Backend apps become simpler
* Centralized SSL management

---

## 6. NGINX as API Gateway

Sometimes NGINX acts as entry point for APIs.

It can provide:

* Authentication
* Rate limiting
* Security headers
* Request filtering
* API routing

---

# Real Kubernetes Architecture Example

```text id="t0vw0n"
Internet User
      ↓
Load Balancer
      ↓
NGINX Ingress Controller
      ↓
Kubernetes Service
      ↓
Application Pods
```

---

# Why Companies Use NGINX in Kubernetes

Because it is:

* Fast
* Lightweight
* Stable
* Easy to configure
* Open source
* Supports high traffic
* Works well with microservices

---

# Common NGINX Kubernetes Components

| Component                | Purpose                    |
| ------------------------ | -------------------------- |
| NGINX Pod                | Runs web server            |
| NGINX Deployment         | Manages replicas           |
| NGINX Service            | Exposes NGINX internally   |
| NGINX Ingress Controller | Manages external traffic   |
| ConfigMap                | Stores NGINX configuration |

---

# Common Commands

### Deploy NGINX Pod

```bash id="97yd9o"
kubectl create deployment nginx --image=nginx
```

---

### Expose NGINX Service

```bash id="lj87v7"
kubectl expose deployment nginx --port=80 --type=NodePort
```

---

### Check NGINX Pods

```bash id="i6ayh9"
kubectl get pods
```

---

### Check NGINX Service

```bash id="rbrb81"
kubectl get svc
```

---

# Interview One-Line Answer

“In Kubernetes, NGINX is mainly used as a reverse proxy, load balancer, web server, and Ingress Controller to manage external traffic and route requests to applications running inside the cluster.”
# Nginx Full Concepts

Nginx is an open-source web server, reverse proxy server, load balancer, and HTTP cache server.

Nginx is widely used for hosting websites, handling web traffic, reverse proxying applications, load balancing, SSL termination, and API gateway functionality.

Nginx is known for high performance, scalability, low memory usage, and handling large numbers of concurrent connections efficiently.

Nginx is commonly used in DevOps, cloud computing, Kubernetes, microservices, and production web environments.

## Why Nginx is Used

Nginx serves static and dynamic web content efficiently.

Nginx acts as a reverse proxy for backend applications.

Nginx distributes traffic using load balancing.

Nginx handles SSL/TLS encryption for HTTPS communication.

Nginx improves performance using caching and compression.

Nginx manages high traffic efficiently with low resource usage.

## Nginx Architecture

Nginx follows an event-driven asynchronous architecture.

Nginx uses a Master Process and multiple Worker Processes.

### Master Process

The Master Process manages configuration files, worker processes, and system signals.

The Master Process starts and controls worker processes.

### Worker Process

Worker Processes handle client requests and responses.

Worker processes efficiently handle thousands of simultaneous connections.

Nginx uses non-blocking I/O for high performance.

## How Nginx Works

Client sends HTTP or HTTPS request to Nginx server.

Nginx receives the request using configured ports like `80` or `443`.

Nginx processes the request based on configuration rules.

Nginx either serves static files directly or forwards requests to backend applications.

Nginx sends response back to the client efficiently.

## Nginx Installation

Install Nginx on Ubuntu:

```bash id="jlwm1a"
sudo apt update
sudo apt install nginx -y
```

Start Nginx service:

```bash id="’wini2b"
sudo systemctl start nginx
```

Enable Nginx during boot:

```bash id="’wini3c"
sudo systemctl enable nginx
```

Check Nginx service status:

```bash id="’wini4d"
systemctl status nginx
```

Check Nginx version:

```bash id="’wini5e"
nginx -v
```

## Nginx Default Ports

Port `80` is used for HTTP communication.

Port `443` is used for HTTPS communication.

## Nginx Configuration Files

Main configuration file:

```text id="’wini6f"
/etc/nginx/nginx.conf
```

Site configuration directory:

```text id="’wini7g"
/etc/nginx/sites-available/
```

Enabled site configurations:

```text id="’wini8h"
/etc/nginx/sites-enabled/
```

## Nginx Basic Configuration

Example server block:

```nginx id="’wini9i"
server {
    listen 80;

    server_name example.com;

    location / {
        root /var/www/html;
        index index.html;
    }
}
```

`listen` defines the port number.

`server_name` defines domain name.

`location` defines URL path handling rules.

`root` defines website file location.

`index` defines default webpage file.

## Test Nginx Configuration

Check configuration syntax:

```bash id="’wini0j"
nginx -t
```

Reload Nginx configuration:

```bash id="’wini1k"
sudo systemctl reload nginx
```

Restart Nginx service:

```bash id="’wini2l"
sudo systemctl restart nginx
```

## Web Server

Nginx serves static files like HTML, CSS, JavaScript, images, and videos.

Nginx can host websites directly from server directories.

Example website directory:

```text id="’wini3m"
/var/www/html
```

## Reverse Proxy

Reverse Proxy forwards client requests to backend applications.

Clients interact with Nginx instead of directly accessing backend servers.

Nginx improves security and performance for backend services.

Example reverse proxy configuration:

```nginx id="’wini4n"
server {
    listen 80;

    location / {
        proxy_pass http://localhost:3000;
    }
}
```

Nginx forwards requests to application running on port `3000`.

## Load Balancing

Load Balancing distributes traffic across multiple backend servers.

Load balancing improves availability, scalability, and fault tolerance.

Example load balancer configuration:

```nginx id="’wini5o"
upstream backend {
    server 192.168.1.10;
    server 192.168.1.11;
}

server {
    listen 80;

    location / {
        proxy_pass http://backend;
    }
}
```

## Load Balancing Methods

Round Robin distributes requests sequentially across servers.

Least Connections sends traffic to server with least active connections.

IP Hash sends requests from same client IP to same backend server.

## SSL/TLS Configuration

Nginx supports HTTPS using SSL/TLS certificates.

SSL/TLS encrypts communication between client and server securely.

Example HTTPS configuration:

```nginx id="’wini6p"
server {
    listen 443 ssl;

    ssl_certificate /etc/nginx/cert.pem;
    ssl_certificate_key /etc/nginx/key.pem;
}
```

## Redirect HTTP to HTTPS

Example redirect configuration:

```nginx id="’wini7q"
server {
    listen 80;
    return 301 https://$host$request_uri;
}
```

## Nginx Caching

Nginx supports caching to improve performance and reduce backend load.

Caching stores frequently accessed responses temporarily.

Nginx can cache static files, APIs, and proxy responses.

## Compression

Nginx supports Gzip compression for reducing response size.

Compression improves website loading speed and bandwidth usage.

Enable Gzip:

```nginx id="’wini8r"
gzip on;
```

## Nginx Logs

Access logs store successful client requests.

Error logs store failures and server issues.

Access log location:

```text id="’wini9s"
/var/log/nginx/access.log
```

Error log location:

```text id="’wini0t"
/var/log/nginx/error.log
```

View logs:

```bash id="’wini1u"
tail -f /var/log/nginx/access.log
```

## Nginx Security

Use HTTPS for encrypted communication.

Disable unnecessary modules and ports.

Restrict access using firewall rules.

Use rate limiting to prevent DDoS attacks.

Hide server version information for security.

Example:

```nginx id="’wini2v"
server_tokens off;
```

## Rate Limiting

Rate limiting controls request frequency from clients.

Rate limiting helps prevent abuse and attacks.

Example:

```nginx id="’wini3w"
limit_req_zone $binary_remote_addr zone=mylimit:10m rate=5r/s;
```

## Nginx in Docker

Nginx commonly runs inside Docker containers.

Run Nginx container:

```bash id="’wini4x"
docker run -d -p 80:80 nginx
```

## Nginx in Kubernetes

Nginx is widely used as Kubernetes Ingress Controller.

NGINX Ingress Controller manages HTTP and HTTPS routing inside Kubernetes clusters.

Ingress routes traffic to Kubernetes Services.

## Nginx Commands

Start Nginx:

```bash id="’wini5y"
sudo systemctl start nginx
```

Stop Nginx:

```bash id="’wini6z"
sudo systemctl stop nginx
```

Restart Nginx:

```bash id="’wini7a"
sudo systemctl restart nginx
```

Reload Nginx:

```bash id="’wini8b"
sudo systemctl reload nginx
```

Check status:

```bash id="’wini9c"
systemctl status nginx
```

## Nginx Advantages

Nginx provides high performance and scalability.

Nginx handles large traffic efficiently.

Nginx uses low CPU and memory resources.

Nginx supports reverse proxy and load balancing.

Nginx supports SSL/TLS and caching features.

Nginx integrates with Docker, Kubernetes, and cloud environments easily.

## Nginx Limitations

Complex configurations may become difficult for beginners.

Dynamic content processing usually requires external application servers like PHP-FPM.

Advanced debugging may require deeper networking knowledge.

## Nginx Workflow

Client sends HTTP or HTTPS request.

Nginx receives request on configured port.

Nginx checks configuration rules.

Nginx serves static files or forwards requests to backend servers.

Load balancing distributes traffic if multiple backend servers exist.

SSL/TLS secures communication if HTTPS is enabled.

Nginx sends optimized response back to the client efficiently.# 🚀 NGINX Zero to Hero

**Beginner-Friendly Guide for DevOps and Cloud Engineers**

---

## 🎯 What You'll Learn

| Section | Topic                                      | Description                                                        |
|---------|--------------------------------------------|--------------------------------------------------------------------|
| 1️⃣      | [Introduction to NGINX](./01-getting-started.md)    | What is NGINX, why DevOps use it, and how to install it            |
| 2️⃣      | [NGINX as a Web Server](./02-nginx-as-web-server.md)    | Serve static websites and understand root vs alias                 |
| 3️⃣      | [NGINX as a Reverse Proxy](./03-nginx-as-reverse-proxy.md) | Forward traffic to backend apps with a production-style setup      |
| 4️⃣      | [Load Balancing](./04-nginx-as-load-balancer.md)           | Distribute requests to multiple backends (round-robin, IP hash)    |
| 5️⃣      | [SSL/TLS with Self-Signed Certs](./05-nginx-with-ssl-or-tls.md) | Add HTTPS for local/test environments using OpenSSL                |

---

## 🧰 Prerequisites

- Basic Linux CLI skills

---

## 🧪 How to Use This Repo

Each section comes with:
- ✅ Markdown notes
- ✅ Real commands
- ✅ Configuration snippets
- ✅ Demos you can run on your local machine

You can go through each section sequentially or jump to the one you need.

---

## 🙌 Contribute or Ask

Feel free to:
- Open an issue for feedback
- Suggest improvements
- Request additional sections

---

## 📜 License

This course and repo are released under the [Apache License](./LICENSE).

---
