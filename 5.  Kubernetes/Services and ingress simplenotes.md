# Kubernetes Services and Ingress

Kubernetes Services and Ingress are networking components used to expose and manage communication between Pods and external users.

Services provide stable internal or external access to Pods.

Ingress manages HTTP and HTTPS traffic routing into Kubernetes clusters.

# Kubernetes Services

Kubernetes Service is a Kubernetes resource used to expose and provide stable network access to Pods.

Pods in Kubernetes are temporary and their IP addresses can change when Pods restart or recreate.

Services provide a stable IP address and DNS name for accessing Pods reliably.

Services help communication between applications, Pods, users, and external systems.

## Why Services are Needed

Pods are dynamic and short-lived.

Pod IP addresses change frequently during scaling or failures.

Direct communication with Pod IPs becomes unreliable.

Services solve this problem by providing stable networking endpoints.

Services also provide load balancing between Pods automatically.

## How Kubernetes Service Works

Service selects Pods using labels and selectors.

Service creates a stable virtual IP address called ClusterIP.

Traffic sent to Service gets forwarded to healthy Pods automatically.

Kube Proxy manages networking rules and traffic forwarding.

## Service Architecture

Client sends request to Service.

Service receives request using stable IP or DNS name.

Service forwards request to one of matching Pods.

Pod processes request and sends response back.

## Labels and Selectors

Services use labels and selectors to identify target Pods.

Example Pod label:

```yaml id="jlwm1a"
labels:
  app: nginx
```

Example Service selector:

```yaml id="’wini2b"
selector:
  app: nginx
```

Service routes traffic to Pods having matching labels.

# Types of Kubernetes Services

Kubernetes mainly provides ClusterIP, NodePort, LoadBalancer, ExternalName, and Headless Services.

---

# 1. ClusterIP Service

ClusterIP is the default Kubernetes Service type.

ClusterIP exposes application only inside the Kubernetes cluster.

External users cannot access ClusterIP directly.

ClusterIP is mainly used for internal microservice communication.

## ClusterIP Workflow

Service gets internal virtual IP.

Pods inside cluster communicate using Service DNS or ClusterIP.

Traffic is load balanced across matching Pods.

## ClusterIP Example

```yaml id="’wini3c"
apiVersion: v1
kind: Service

metadata:
  name: nginx-service

spec:
  selector:
    app: nginx

  ports:
    - port: 80
      targetPort: 80

  type: ClusterIP
```

## Access ClusterIP Service

Inside cluster:

```bash id="’wini4d"
curl http://nginx-service
```

---

# 2. NodePort Service

NodePort exposes application externally using worker node IP and static port.

Kubernetes opens same port on all worker nodes.

External users access application using:

```text id="’wini5e"
NodeIP:NodePort
```

Default NodePort range:

```text id="’wini6f"
30000 - 32767
```

## NodePort Workflow

Client sends request to worker node IP and NodePort.

Node forwards traffic to Service.

Service forwards traffic to Pods.

## NodePort Example

```yaml id="’wini7g"
apiVersion: v1
kind: Service

metadata:
  name: nginx-service

spec:
  selector:
    app: nginx

  ports:
    - port: 80
      targetPort: 80
      nodePort: 30080

  type: NodePort
```

Access application:

```text id="’wini8h"
http://NodeIP:30080
```

---

# 3. LoadBalancer Service

LoadBalancer exposes application externally using cloud provider Load Balancer.

Cloud providers automatically create external Load Balancers.

LoadBalancer Service is mainly used in AWS, Azure, and Google Cloud environments.

## LoadBalancer Workflow

Client sends request to external Load Balancer IP.

Load Balancer forwards request to NodePort Service internally.

Service routes traffic to Pods.

## LoadBalancer Example

```yaml id="’wini9i"
apiVersion: v1
kind: Service

metadata:
  name: nginx-service

spec:
  selector:
    app: nginx

  ports:
    - port: 80
      targetPort: 80

  type: LoadBalancer
```

Check external IP:

```bash id="’wini0j"
kubectl get svc
```

---

# 4. ExternalName Service

ExternalName maps Kubernetes Service to external DNS name.

No proxying or load balancing happens.

Kubernetes returns external DNS name directly.

## ExternalName Example

```yaml id="’wini1k"
apiVersion: v1
kind: Service

metadata:
  name: external-service

spec:
  type: ExternalName
  externalName: google.com
```

Pods access external service using internal Kubernetes DNS.

---

# 5. Headless Service

Headless Service does not create ClusterIP.

Headless Service directly exposes Pod IP addresses.

Headless Services are commonly used with StatefulSets.

## Headless Service Example

```yaml id="’wini2l"
apiVersion: v1
kind: Service

metadata:
  name: mysql

spec:
  clusterIP: None

  selector:
    app: mysql

  ports:
    - port: 3306
```

## Why Headless Service is Used

Provides direct Pod-to-Pod communication.

Provides stable DNS records for StatefulSet Pods.

Used in databases and distributed systems.

---

# Service Discovery

Kubernetes automatically creates DNS entries for Services.

Pods communicate using Service names instead of IP addresses.

Example:

```text id="’wini3m"
http://nginx-service
```

DNS resolution is managed by CoreDNS inside Kubernetes.

---

# Service Ports

### port

Port exposed by Service.

### targetPort

Port inside Pod container.

### nodePort

External port opened on worker node for NodePort Service.

## Example

```yaml id="’wini4n"
ports:
  - port: 80
    targetPort: 8080
    nodePort: 30080
```

---

# Kube Proxy

Kube Proxy manages Service networking rules.

Kube Proxy forwards traffic from Services to Pods.

Kube Proxy uses iptables or IPVS internally.

---

# Service Load Balancing

Services automatically distribute traffic across multiple Pods.

Load balancing improves scalability and high availability.

Traffic routing works transparently for clients.

---

# Service Commands

Create Service:

```bash id="’wini5o"
kubectl apply -f service.yaml
```

List Services:

```bash id="’wini6p"
kubectl get svc
```

Describe Service:

```bash id="’wini7q"
kubectl describe svc nginx-service
```

Delete Service:

```bash id="’wini8r"
kubectl delete svc nginx-service
```

---

# Expose Deployment as Service

Automatically expose Deployment:

```bash id="’wini9s"
kubectl expose deployment nginx-deployment \
--type=NodePort \
--port=80
```

---

# Service Communication Example

Frontend Pod sends request to Backend Service.

Backend Service forwards traffic to Backend Pods.

Pods communicate using stable DNS names.

Scaling Pods does not affect Service access.

---

# Services in Microservices

Each microservice commonly gets its own Kubernetes Service.

Services provide communication between frontend, backend, databases, and APIs.

Services help decouple applications from changing Pod IPs.

---

# Advantages of Kubernetes Services

Provides stable networking for Pods.

Supports internal and external application access.

Provides automatic load balancing.

Supports DNS-based service discovery.

Improves scalability and reliability.

---

# Limitations of Kubernetes Services

NodePort exposes limited port ranges.

LoadBalancer depends on cloud provider support.

Large-scale networking may require advanced Ingress and Service Mesh solutions.

Complex traffic routing may require Ingress Controllers.
# Ingress in Kubernetes

Kubernetes Ingress is a Kubernetes resource used to manage external HTTP and HTTPS access to applications running inside a Kubernetes cluster.

Ingress provides routing rules for incoming traffic and forwards requests to Kubernetes Services.

Ingress helps expose multiple applications using a single external IP address.

Ingress commonly provides load balancing, SSL/TLS termination, domain-based routing, and path-based routing.

Ingress is mainly used for web applications, APIs, and microservices architectures.

## Why Ingress is Needed

Without Ingress, each application may require separate LoadBalancer or NodePort Services.

Managing multiple external IPs becomes expensive and complex.

Ingress centralizes external traffic management.

Ingress reduces cloud costs by sharing one Load Balancer across multiple services.

Ingress improves routing, security, and SSL management.

## How Ingress Works

Client sends HTTP or HTTPS request.

Ingress Controller receives incoming traffic.

Ingress resource contains routing rules.

Ingress Controller checks hostnames and URL paths.

Traffic is forwarded to correct Kubernetes Service.

Service forwards traffic to application Pods.

## Ingress Architecture

Main components are Client, Ingress Controller, Ingress Resource, Services, and Pods.

## Ingress Resource

Ingress Resource contains routing rules and configurations.

Ingress itself does not process traffic directly.

Ingress only defines routing instructions.

## Ingress Controller

Ingress Controller is the actual component handling external traffic.

Ingress Controller reads Ingress rules and configures reverse proxy behavior automatically.

Ingress Controller commonly works as reverse proxy and load balancer.

Common Ingress Controllers are:

NGINX Ingress Controller

Traefik

HAProxy Ingress

## Ingress Workflow

Client accesses domain like:

```text id="jlwm1a"
https://example.com
```

DNS points domain to Ingress Controller external IP.

Ingress Controller receives request.

Ingress rules determine target Service.

Service forwards request to application Pods.

Application response returns to client through Ingress Controller.

---

# Types of Ingress Routing

## Host-Based Routing

Routes traffic based on domain name.

Example:

```text id="’wini2b"
app1.example.com -> app1-service
app2.example.com -> app2-service
```

## Path-Based Routing

Routes traffic based on URL path.

Example:

```text id="’wini3c"
/api -> api-service
/web -> web-service
```

---

# Ingress YAML Example

## Basic Ingress Example

```yaml id="’wini4d"
apiVersion: networking.k8s.io/v1
kind: Ingress

metadata:
  name: my-ingress

spec:
  rules:
  - host: example.com

    http:
      paths:
      - path: /
        pathType: Prefix

        backend:
          service:
            name: nginx-service

            port:
              number: 80
```

## Explanation

`host` defines domain name.

`path` defines URL path rule.

`backend` defines target Kubernetes Service.

`service.name` defines Service name.

`port.number` defines Service port.

---

# Path-Based Routing Example

```yaml id="’wini5e"
apiVersion: networking.k8s.io/v1
kind: Ingress

metadata:
  name: app-ingress

spec:
  rules:
  - host: example.com

    http:
      paths:
      - path: /api
        pathType: Prefix

        backend:
          service:
            name: api-service

            port:
              number: 80

      - path: /web
        pathType: Prefix

        backend:
          service:
            name: web-service

            port:
              number: 80
```

## Routing Result

```text id="’wini6f"
example.com/api -> api-service
example.com/web -> web-service
```

---

# Host-Based Routing Example

```yaml id="’wini7g"
apiVersion: networking.k8s.io/v1
kind: Ingress

metadata:
  name: multi-host-ingress

spec:
  rules:
  - host: api.example.com

    http:
      paths:
      - path: /
        pathType: Prefix

        backend:
          service:
            name: api-service

            port:
              number: 80

  - host: web.example.com

    http:
      paths:
      - path: /
        pathType: Prefix

        backend:
          service:
            name: web-service

            port:
              number: 80
```

---

# Install NGINX Ingress Controller

Install Controller:

```bash id="’wini8h"
kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/main/deploy/static/provider/cloud/deploy.yaml
```

Check Controller Pods:

```bash id="’wini9i"
kubectl get pods -n ingress-nginx
```

Check Ingress Controller Service:

```bash id="’wini0j"
kubectl get svc -n ingress-nginx
```

---

# Create Ingress

Apply YAML:

```bash id="’wini1k"
kubectl apply -f ingress.yaml
```

View Ingress resources:

```bash id="’wini2l"
kubectl get ingress
```

Describe Ingress:

```bash id="’wini3m"
kubectl describe ingress my-ingress
```

---

# SSL/TLS in Ingress

Ingress supports HTTPS using SSL/TLS certificates.

TLS secures communication between client and Ingress Controller.

## TLS Example

```yaml id="’wini4n"
spec:
  tls:
  - hosts:
    - example.com

    secretName: tls-secret
```

## Create TLS Secret

```bash id="’wini5o"
kubectl create secret tls tls-secret \
--cert=cert.pem \
--key=key.pem
```

---

# Default Backend

Ingress can use default backend for unmatched requests.

If no rules match, traffic goes to default backend service.

---

# Ingress vs Service

Service exposes Pods inside cluster or externally.

Ingress manages HTTP and HTTPS routing rules.

Service works at Layer 4 mainly.

Ingress works at Layer 7 using HTTP and HTTPS.

Ingress routes traffic to multiple Services intelligently.

---

# Ingress vs LoadBalancer

LoadBalancer exposes single Service externally.

Ingress manages multiple Services using one external Load Balancer.

Ingress is more cost-efficient in cloud environments.

Ingress supports domain and path-based routing.

---

# Ingress in Microservices

Ingress acts as entry point for microservices applications.

Ingress routes traffic to frontend, backend, APIs, and other services.

Ingress simplifies external traffic management for large applications.

---

# Advantages of Ingress

Centralized traffic management.

Supports SSL/TLS termination.

Supports path-based and host-based routing.

Reduces cloud LoadBalancer costs.

Provides reverse proxy and load balancing features.

Improves scalability and external access management.

---

# Limitations of Ingress

Ingress mainly supports HTTP and HTTPS traffic.

Complex routing may require advanced configurations.

Ingress requires Ingress Controller installation.

Different Ingress Controllers support different features.

---

# Ingress Workflow Example

Client opens `https://example.com/api`.

DNS points request to Ingress Controller.

Ingress Controller receives HTTPS request.

TLS certificate secures communication.

Ingress rules match `/api` path.

Traffic forwards to `api-service`.

Service routes traffic to healthy Pods.

Application response returns to client securely.
