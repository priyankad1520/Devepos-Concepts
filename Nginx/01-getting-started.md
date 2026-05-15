# 📘 Section 1: Introduction to NGINX

## ✅ What is NGINX?

**NGINX** is an open-source, high-performance web server that also functions as:
- A reverse proxy
- Load balancer
- HTTP cache
- Mail proxy

It is designed for high concurrency, performance, and low memory usage — making it ideal for modern DevOps and cloud environments.

---

## Reverse Proxy

<img width="1536" height="1024" alt="nginx-reverse-proxy" src="https://github.com/user-attachments/assets/1c9fbec8-b7b6-4385-bf96-dd6598842b81" />

---

### 1. Web Server
A web server handles: HTML, CSS, JavaScript, Images, Static files

Example: Nginx, Apache HTTP Server

```text id="tf2q3f"
Example: Browser requests: www.flipkart.com

Web server sends: HTML page, CSS, Images
```
### 2. API

API allows applications/services to communicate and exchange data.
```text id="cv7xjz"
Example: Mobile App → Request Product Data

API returns:
{
  "name": "Laptop",
  "price": 50000
}

# Example APIs
GET /products
POST /payment
GET /orders
```
### 3. API Gateway

API Gateway acts as a single entry point for multiple APIs/microservices.

It: Receives requests, Routes traffic, Handles authentication, Rate limiting, Security

```text id="nqjlwm"
Example
User Request
      ↓
API Gateway
      ↓
 ┌───────────────┐
 │ User Service  │
 │ Payment API   │
 │ Product API   │
 └───────────────┘
```
# Main Difference

| Web Server | API | API Gateway |
|---|---|
| Serves webpages/files | Exchanges data | Manages APIs |
| Mostly frontend content | Backend communication | Traffic controller |
| Returns HTML | Returns JSON/XML | Routes requests |
| Restaurant waiter serving food | Communication between kitchen and waiter| Reception manager controlling all requests |
---
### Important DevOps Understanding
```text id="j40uvq"
In microservices:

Users
   ↓
Load Balancer
   ↓
Web Server / API Gateway
   ↓
Microservices APIs
```

## 📊 NGINX vs Apache (Why DevOps Prefer NGINX)

| Feature         | NGINX                          | Apache                      |
|-----------------|--------------------------------|-----------------------------|
| Architecture    | Event-driven (asynchronous)    | Process/thread-based        |
| Performance     | High concurrency, fast         | Slower with many connections|
| Memory usage    | Low                            | High                        |
| Static content  | Extremely fast                 | Good                        |
| Config format   | Simple, declarative            | More flexible but complex   |
| Use cases       | Web server, reverse proxy, LB  | Traditional web server      |

💡 **DevOps Engineers** often choose NGINX for its:
- Lightweight footprint
- Ease of automation
- Docker/Kubernetes friendliness

---

## 🧰 Common DevOps Use Cases for NGINX

| Use Case                              | Example                                                                 |
|--------------------------------------|-------------------------------------------------------------------------|
| Web server                           | Serving static React/Angular apps                                      |
| Reverse proxy                        | Forwarding requests to backend apps (Node.js, Python, Java)            |
| Load balancer                        | Distributing load between multiple backend servers                     |
| SSL termination                      | Handling HTTPS at the edge                                             |
| Caching                              | Reducing load on upstream services                                     |
| Ingress controller (Kubernetes)      | Managing traffic inside Kubernetes clusters                            |
| Rate limiting & security enforcement | Protecting APIs from abuse or bots                                     |

---

## 🛠️ Installing NGINX

### 🐧 On Ubuntu/Debian
```bash
sudo apt update
sudo apt install nginx -y
```

### 📦 On RHEL/CentOS
```bash
sudo yum install epel-release -y
sudo yum install nginx -y
```

### 🐳 Using Docker (Recommended for DevOps)
```bash
docker run --name nginx -p 8080:80 -d nginx
```

Visit: `http://localhost:8080`

---

## 📁 NGINX File Structure (Linux)

| File/Directory        | Purpose                                      |
|-----------------------|----------------------------------------------|
| `/etc/nginx/nginx.conf` | Main configuration file                     |
| `/etc/nginx/sites-available/` | Stores virtual host (server block) configs |
| `/etc/nginx/sites-enabled/`   | Symlinks to active site configs         |
| `/var/www/html`       | Default web root directory                   |
| `/var/log/nginx/`     | Contains access and error logs               |

---

## 🧪 Demo: Run NGINX Using Docker

### Step 1: Run container
```bash
docker run --name nginx-demo -p 8080:80 -d nginx
```

### Step 2: Test in browser
Visit: `http://localhost:8080`  
You should see the **Welcome to NGINX** page.

### Step 3: View Logs
```bash
docker logs nginx-demo
```

### Step 4: Clean up
```bash
docker stop nginx-demo
docker rm nginx-demo
```

---

## 🎯 Summary

- NGINX is a lightweight, high-performance web server and reverse proxy.
- Widely used in DevOps for load balancing, SSL termination, and as a reverse proxy.
- Easy to install via Linux package managers or Docker.
- Supports modular configuration — great for automation and CI/CD.
