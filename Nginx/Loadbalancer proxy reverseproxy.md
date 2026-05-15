1. Server: A server is a computer or software that provides services, data, or resources to other computers called clients.

2. Backend Server: A backend server handles the main business logic, database operations, authentication, and application processing behind the scenes.

3. Internet Server: An internet server is a server connected to the internet and accessible publicly by users worldwide.

# Load Balancer

"A load balancer distributes incoming traffic across multiple servers, EC2 instances, Kubernetes nodes, or pods to improve availability, scalability, and performance."

Load Balancer is a networking component that distributes incoming traffic across multiple servers or applications.

Load Balancer improves performance, scalability, reliability, and availability of applications.

Load Balancer prevents one server from becoming overloaded with too much traffic.

If one server fails, Load Balancer redirects traffic to healthy servers automatically.

Load Balancer is widely used in cloud computing, Kubernetes, web applications, and microservices environments.

## How Load Balancer Works

Client sends request to Load Balancer.

Load Balancer receives incoming traffic.

Load Balancer selects one backend server based on balancing algorithm.

Request is forwarded to selected server.

Server processes request and sends response back through Load Balancer.

Client receives response without knowing which server handled the request.

## Load Balancing Algorithms

### Round Robin

Requests are distributed sequentially across servers.

Example:

```text id="jlwm1a"
Request 1 -> Server 1
Request 2 -> Server 2
Request 3 -> Server 3
```

### Least Connections

Traffic is sent to server with the fewest active connections.

### IP Hash

Requests from same client IP always go to same server.

## Types of Load Balancers

### Layer 4 Load Balancer

Works at Transport Layer using TCP and UDP traffic.

Uses IP addresses and ports for traffic distribution.

### Layer 7 Load Balancer

Works at Application Layer using HTTP and HTTPS traffic.

Can route traffic based on URL, hostname, headers, and cookies.

## Common Load Balancers

NGINX, HAProxy, AWS ELB, and Traefik are commonly used Load Balancers.

## Example Nginx Load Balancer

```nginx id="’wini2b"
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

---

# Proxy Server

Proxy Server acts as an intermediary between client and server.

Proxy receives requests from clients and forwards them to destination servers.

Proxy hides client identity from destination servers.

Proxy improves security, filtering, caching, and access control.

## How Proxy Works

Client sends request to Proxy Server.

Proxy Server forwards request to internet or destination server.

Destination server responds to Proxy Server.

Proxy Server sends response back to client.

Destination server sees Proxy IP instead of client IP.

## Uses of Proxy

Proxy hides user IP addresses.

Proxy filters websites and internet access.

Proxy improves caching and performance.

Proxy monitors network traffic.

## Forward Proxy

Forward Proxy sits between clients and internet servers.

Clients use Forward Proxy to access external resources.

Example use case is company internet filtering.

---

# Reverse Proxy

Reverse Proxy sits between clients and backend servers.

Clients communicate with Reverse Proxy instead of directly accessing backend servers.

Reverse Proxy forwards requests to backend applications internally.

Reverse Proxy improves security, scalability, load balancing, SSL termination, and caching.

## How Reverse Proxy Works

Client sends request to Reverse Proxy.

Reverse Proxy receives request.

Reverse Proxy forwards request to backend server.

Backend server processes request.

Response returns through Reverse Proxy to client.

Client never directly communicates with backend servers.

## Reverse Proxy Features

Reverse Proxy hides backend server details.

Reverse Proxy performs load balancing.

Reverse Proxy handles SSL/TLS encryption.

Reverse Proxy caches responses for performance improvement.

Reverse Proxy protects backend applications from direct exposure.

## Common Reverse Proxy Servers

NGINX and Apache are commonly used Reverse Proxy servers.

## Reverse Proxy Example

```nginx id="’wini3c"
server {
    listen 80;

    location / {
        proxy_pass http://localhost:3000;
    }
}
```

Requests are forwarded to application running on port `3000`.

## Proxy vs Reverse Proxy

Forward Proxy protects and represents clients.

Reverse Proxy protects and represents backend servers.

Forward Proxy hides client identity.

Reverse Proxy hides backend server identity.

Forward Proxy is used mainly by clients.

Reverse Proxy is used mainly by servers and applications.

---

# SSL and TLS

SSL stands for Secure Sockets Layer.

TLS stands for Transport Layer Security.

SSL and TLS are security protocols used to encrypt communication between client and server.

TLS is the modern and secure replacement for older SSL versions.

HTTPS uses SSL/TLS for secure communication.

## Why SSL/TLS is Used

SSL/TLS protects sensitive data during network communication.

SSL/TLS prevents attackers from reading or modifying transmitted data.

SSL/TLS provides encryption, authentication, and data integrity.

SSL/TLS is widely used in websites, APIs, banking applications, cloud services, and Kubernetes Ingress.

## How SSL/TLS Works

Client sends HTTPS request to server.

Server sends SSL/TLS certificate to client.

Client verifies server certificate.

Client and server establish encrypted session keys.

Encrypted communication begins securely.

All transmitted data becomes unreadable to attackers.

## SSL/TLS Certificate

Certificate verifies server identity.

Certificates are issued by Certificate Authorities called CA.

Example certificate providers are Let’s Encrypt and DigiCert.

## HTTPS

HTTPS stands for HyperText Transfer Protocol Secure.

HTTPS uses SSL/TLS encryption for secure web communication.

HTTPS commonly uses port `443`.

HTTP without encryption uses port `80`.

## SSL/TLS Features

### Encryption

Data becomes unreadable during transmission.

### Authentication

Verifies server identity using certificates.

### Data Integrity

Ensures transmitted data is not modified during communication.

## TLS Handshake

TLS Handshake establishes secure encrypted communication.

Client and server exchange certificates and encryption keys.

Secure session is created before data transmission starts.

## SSL/TLS Example in Nginx

```nginx id="’wini4d"
server {
    listen 443 ssl;

    ssl_certificate /etc/nginx/cert.pem;
    ssl_certificate_key /etc/nginx/key.pem;
}
```

## HTTP vs HTTPS

HTTP transfers data without encryption.

HTTPS transfers encrypted data securely using SSL/TLS.

HTTP is less secure.

HTTPS protects sensitive information like passwords and payment details.

## Real-Time Example

When opening banking website using HTTPS, browser verifies SSL/TLS certificate.

Secure encrypted communication starts between browser and banking server.

Passwords and payment data travel securely over the internet.

## Relationship Between Load Balancer, Reverse Proxy, and SSL/TLS

Load Balancer distributes traffic across multiple servers.

Reverse Proxy forwards requests to backend applications securely.

SSL/TLS encrypts communication between clients and servers.

Load Balancers and Reverse Proxies commonly handle SSL/TLS termination.

NGINX can act as Load Balancer, Reverse Proxy, and SSL/TLS termination server together.
