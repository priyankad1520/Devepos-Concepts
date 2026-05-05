# Basic Networking Concepts for DevOps Engineers
#### 1. What is Networking?

Networking means connecting computers/devices so they can communicate and share data. / A network is a group of devices connected to communicate with each other.

Example: Internet, Office LAN, Wifi at home, Cloud Networking(AWS VPC)

* Laptop communicates with server
* Browser communicates with website
* Kubernetes pods communicate with each other
* Jenkins communicates with GitHub
---
#### 2. IP Address = Unique address of a device in a network.
Types: 1. IPv4 → `192.168.1.10` and 2. IPv6 → `2001:db8::1`

##### Types of IP

| Type       | Example     | Usage                  |
| ---------- | ----------- | ---------------------- |
| Private IP | 192.168.x.x | Internal communication |
| Public IP  | 8.8.8.8     | Internet communication |

#### Important Private IP Ranges

| Range                         | Purpose         |
| ----------------------------- | --------------- |
| 10.0.0.0 – 10.255.255.255     | Large networks  |
| 172.16.0.0 – 172.31.255.255   | Medium networks |
| 192.168.0.0 – 192.168.255.255 | Home/office     |

#### Commands

```bash
ip addr
ifconfig
hostname -I
```
---
#### 3. ISP: Internet service provider is a company that gives you access to the internet

#### MAC Address = Physical hardware address of NIC card.
```bash
Example: 00:1A:2B:3C:4D:5E  # Used inside local network communication.
```
```bash
Command: ip link
```
---

#### 4. DNS (Domain Name System): DNS converts domain names into IP addresses.
- Example: google.com → 142.250.183.14
- Without DNS: We must remember IP addresses.
- DNS Flow: Browser → DNS Server → IP Address → Website Opens
##### Commands
```bash
nslookup google.com
dig google.com
host google.com
```
---
#### 5. Port Numbers: Ports identify specific application / services running on a system / Device.
```text
Example: IP = House Address
Port = Room Number
```

### Common Ports
| Port Number | Protocol | Service Name Full Form                            | Usage                        |
| ----------- | -------- | ------------------------------------------------- | ---------------------------- |
| 20 and 21   | TCP      | FTP (File Transfer Protocol) Data and FTP Control | File transfer data and control       |
| 22 and 23   | TCP      | **SSH (Secure Shell)** and Telnet                 | Remote server login and Remote login (not secure)        |
| 25 and 465  | TCP      | **SMTP (Simple Mail Transfer Protocol) and SMTPS (Secure SMTP)**| Sending emails and Secure email sending              |
| 53          | TCP/UDP  | **DNS (Domain Name System)**                      | Domain name resolution       |
| 67 and 68   | UDP      | DHCP (Dynamic Host Configuration Protocol) Server and DHCP Client | Assign IP addresses and Receive IP address           |
| 69          | UDP      | TFTP (Trivial File Transfer Protocol)             | Simple file transfer         |
| 80          | TCP      | **HTTP (HyperText Transfer Protocol)**            | Website traffic              |
| 443         | TCP      | **HTTPS (HyperText Transfer Protocol Secure)**    | Secure websites              |
| 4433        | TCP      | Alternative HTTPS                                 | Secure communication         |
| 2375 & 2376 | TCP      | **Docker Remote API (Non-SSL) and SSL**           | Docker communication &  Secure Docker communication        |
| 2377        | TCP      | **Docker Swarm Manager**                          | Swarm cluster                |
| 9090        | TCP      | **Prometheus**                                    | Monitoring                   |
| 3000        | TCP      | **Grafana** / NodeJS Apps                         | Dashboards/apps              |
| 5601        | TCP      | **Kibana**                                        | Log visualization            |
| 8080        | TCP      | HTTP Alternate / **Jenkins** / Tomcat             | DevOps tools                 |
| 50000       | TCP      | **Jenkins Agent Port**                            | Jenkins nodes                |
| 9000        | TCP      | **SonarQube**                                     | Code quality                 |
| 4954        |          | **Trivy Server Mode**                             | Docker image Vulnerability scanning server |
| 8000        | TCP      | Python/Django Apps                                | Web applications             
| 9092        | TCP      | Apache Kafka                                      | Messaging                    |
| 6379        | TCP      | **Redis**                                         | Cache/database               |
| 9200        | TCP      | **Elasticsearch REST API**                        | Search/log storage           |
| 9300        | TCP      | Elasticsearch Transport                           | Cluster communication        |
| 10250       | TCP      | Kubernetes Kubelet API                            | Node communication           |
| 10255       | TCP      | Read-Only Kubelet API                             | Kubernetes monitoring        |
| 6443        | TCP      | Kubernetes API Server                             | Kubernetes control plane     |
| 3306        | TCP      | MySQL                                             | Database                     |
| 5432        | TCP      | PostgreSQL                                        | Database                     |
| 27017       | TCP      | MongoDB                                           | NoSQL database               |
| 8081        | TCP      | Nexus Repository (Maven)                          | Artifact management          |
| 9418        | TCP      | Git Native Protocol                               | Git repositories             |
| 88          | TCP/UDP  | Kerberos                                          | Authentication               |
| 110         | TCP      | POP3 (Post Office Protocol v3)                    | Receiving emails             |
| 514         | UDP      | Syslog                                            | Log management               |
| 5900        | TCP      | VNC (Virtual Network Computing)                   | Remote desktop               |

##### Commands
```bash
netstat -tulnp
ss -tulnp
lsof -i :80
nc -zv localhost 22
telnet localhost 443
```
---
#### 6. Protocols: Rules for communication.
##### Important Protocols

| Protocol | Full Form                          | Purpose                      |
| -------- | ---------------------------------- | ---------------------------- |
| HTTP     | HyperText Transfer Protocol        | Website communication        |
| HTTPS    | HyperText Transfer Protocol Secure | Secure website communication |
| TCP      | Transmission Control Protocol      | Reliable communication       |
| UDP      | User Datagram Protocol             | Fast communication           |
| SSH      | Secure Shell                       | Remote server login          |
| FTP      | File Transfer Protocol             | File transfer                |
| SMTP     | Simple Mail Transfer Protocol      | Sending emails               |

---
#### 7. TCP vs UDP
| Feature            | TCP                           | UDP                    |
| ------------------ | ----------------------------- | ---------------------- |
| Full Form          | Transmission Control Protocol | User Datagram Protocol |
| Communication Type | Connection-oriented           | Connectionless         |
| Reliability        | Reliable                      | Not reliable           |
| Speed              | Slower                        | Faster                 |
| Error Checking     | Yes                           | Minimal                |
| Data Order         | Maintains order               | No order guarantee     |
| Packet Delivery    | Guaranteed                    | Not guaranteed         |
| Acknowledgement    | Required                      | Not required           |
| Best For           | Accuracy                      | Speed                  |
| Used In            | Websites, databases           | Streaming, gaming      |
| Example Protocols  | HTTP, HTTPS, SSH              | DNS, VoIP, Gaming      |


---

#### 8. OSI Model

Very important for interviews.

| Layer          | Purpose            |
| -------------- | ------------------ |
| 7 Application  | HTTP, DNS. user interaction      |
| 6 Presentation | Encryption. convert data into a secure / encryption formate so hacker can not reat it    |
| 5 Session      | Manages sessions/connections between systems. Responsibilities: Start,Maintain and End sessions  |
| 4 Transport    | TCP: Ensures message reaches correctly. Breaks data into pices/packets, error checking, reliable Delivery, Re-sending if needed /UDP |
| 3 Network      | Finding/ decides the best path/Route. Use IP address and Routers work here         |
| 2 Data Link    | Tranfers data within local Network using MAC Address  Wi-fi ethernet      |
| 1 Physical     | Actual singal (real physical Transmission). Electrial signal,ratio waves, fiber and Cable/Wire         |

```text
Easy Shortcut: Please Do Not Throw Sausage Pizza Away
```
---

#### 9. TCP/IP Model

Real-world networking model.

| Layer          | Protocols |
| -------------- | --------- |
| Application    | HTTP, DNS |
| Transport      | TCP, UDP  |
| Internet       | IP        |
| Network Access | Ethernet  |
---
#### 10. Subnetting: Subnetting divides large networks into smaller networks.
Dividing one big network into smaller parts using IP range or Ip base network

##### CIDR (Class less inter domain routing) / Compact subnet notation.
- Example: 192.168.1.0/24
- /24 means: The number after "/ " Shows how many bits are used for the network port.
- First 24 bits for network remaining bits for Devices/ Hosts
- /32 = 1ip (2^0) for host/device like
- 31=2ip  remaing number is 1 so the value is (2^1) , 30=4ip same as (2^2) , 29=8ip (2^3), 28=16ip (2^4), 27=32ip (2^5), 26=64ip (2^6), 25=128ip
| CIDR | Hosts         |
| ---- | ------------- |
| /24  | 256  (2^7)    |
| /16  | 65536         |
| /8   | 1.6 cr Large network |
- Why Used: Better security, Better management and Reduce traffic
---
#### 11. Gateway: Gateway connects one network to another.

Example: Local network → Internet

### Command

```bash
ip route
route -n
```
---

#### 12. Router: Router forwards packets between networks.
Routing is use to finding/ choose the best or shortest path/ route to send data / data packets to travel from source to destination across networks.
- To avoid network congestion: Use routing table repeately until to find the best path.
- static routing is manually configured route.
- dynamic routing is automatically using protocals/rules.
- Example: Home Router connects: Laptop ↔ Internet

---
#### 13. Switch: Switch connects devices inside same network. Works using MAC addresses.
---
#### 14. Firewall: It's a security graud for company network
- A firewall is a security system that mointors and  controls incoming/outgoing network traffic.
- It soes not allow unauthorized person to access the data, data theft, malware attacks  this are blocked by firewall.

Types of firewall
- network firewall: protect entire network
- Host firewall: Install on individual system
- Cloud firewall: AWS security Groups: Acts like firewall, controles inbound and outbound traffic/ calls

Linux Firewall

```bash
ufw
iptables
firewalld
Example: Allow SSH: ufw allow 22
```
---
#### 15. NAT (Network Address Translation): Converts private IP vice-versa public IP.
- NAT allows private networks to access the internet using a public IP.
- In AWS private network cant access the public internet directly so that use NAT gateway
Type
1. Static NAT: 1 private --> 1 public.
2. Dynamic: uses pool of public IP.
3. PAT (Port Address Transiation): Many private IP's 1--> 1 public IP using ports 
- Example: Multiple systems use one public IP.
- Used in: Home routers, Cloud networking, Kubernetes
---
#### 16. DHCP: DHCP automatically assigns IP addresses.
- Without DHCP: Need manual IP configuration.
- Commands
```bash
dhclient
```
---
#### Cloud Network: Network inside the cloud like rent it. Play how much you use or how much you wnat.

#### 17. VPN (Virtual Private Network): Secure encrypted connection between user and company network.
- VPC is your private, secure and separete network inside the cloud
- Used in: Remote work, Secure access, Cloud connectivity
---
#### 18. Load Balancer: Distributes traffic across multiple servers.

#### Types

| Type    | Usage      |
| ------- | ---------- |
| Layer 4 | TCP/UDP    |
| Layer 7 | HTTP/HTTPS |

#### Popular Load Balancers

* NGINX
* HAProxy
* AWS ELB
* Traefik
---
#### 19. Reverse Proxy: Client sends request to proxy → proxy forwards to backend.
- Used For: SSL termination, Security, Load balancing, Routing
- Examples: NGINX, Traefik
---
#### 20. SSL/TLS: SSL (Secure Sockets Layer): Secure communication over network. TLS (Transport Layer Security): Modern secure communication protocol

Why
- Encrypt communication
- Protect sensitive data
- Secure websites
- Prevent hacking/sniffingEncrypts communication.

Used in:
- HTTPS websites
- APIs
- Banking apps
- Kubernetes ingress
- DevOps tools

Example: HTTP  → Not Secure or HTTPS → Secure

##### Certificate Files

```text
.crt
.key
.pem
```
---
#### 21. HTTP Methods

| Method | Purpose    |
| ------ | ---------- |
| GET    | Fetch data |
| POST   | Send data  |
| PUT    | Update     |
| DELETE | Remove     |

---

#### 22. API: API allows applications to communicate. `Example: Frontend ↔ Backend ↔ Database`
- API Types: REST API, SOAP API, GraphQL
---
#### 23. Packet: Small piece of data transferred over network.
---
#### 24. Latency: Delay in communication. `Check latency: ping google.com`
---
#### 25. Bandwidth: Bandwidth = Amount of data transferable. `Example: 100 Mbps or 1 Gbps`
---
#### 26. Ping: Checks connectivity. `ping google.com`
---
#### 27. Traceroute: Shows path packets travel.

```bash
traceroute google.com
tracepath google.com
```
---
#### 30. Network Interface Card (NIC): Hardware/network adapter used for communication. `Command: ip link`

These are the most important concepts DevOps engineers use daily.

---

# 1. Linux Networking

Must Know:

```bash
ping
curl
wget
netstat
ss
telnet
nc
ip addr
ip route
traceroute
tcpdump
nslookup
dig
```

---

# 2. DNS Troubleshooting

Common Issue:

```text
Website not opening due to DNS failure
```

### Commands

```bash
nslookup
dig
cat /etc/resolv.conf
```

---

# 3. Load Balancing

Used in:

* Kubernetes
* NGINX
* AWS ELB
* Ingress Controllers

Concepts:

* Round Robin
* Sticky Sessions
* Health Checks

---

# 4. Reverse Proxy

Very important in:

* NGINX
* Kubernetes Ingress
* API Gateway

---

# 5. Kubernetes Networking

Very important.

Must Know:

* Pod Networking
* Service Networking
* ClusterIP
* NodePort
* LoadBalancer
* Ingress
* CNI Plugins

### Popular CNI

* Calico
* Flannel
* Cilium

---

# 6. Container Networking

Docker Networking Types:

| Type    | Usage               |
| ------- | ------------------- |
| Bridge  | Default             |
| Host    | Shares host network |
| Overlay | Multi-host          |
| None    | No networking       |

### Commands

```bash
docker network ls
docker inspect
```

---

# 7. Cloud Networking

Important in:

* Amazon Web Services
* Microsoft Azure
* Google Cloud Platform

Must Know:

* VPC
* Subnets
* Security Groups
* NAT Gateway
* Route Tables
* Internet Gateway

---

# 8. Security Groups & Firewall

DevOps engineers manage:

* Open ports
* SSH access
* HTTPS access
* Kubernetes security

---

# 9. SSL/TLS Management

Tasks:

* Renew certificates
* Configure HTTPS
* Troubleshoot SSL errors

Tools:

* Certbot
* OpenSSL

---

# 10. CI/CD Networking

Example:

```text
GitHub → Jenkins → Docker → Kubernetes
```

Need networking between:

* Git server
* CI server
* Registry
* Kubernetes

---

# 11. Monitoring Networking

Tools:

* Prometheus
* Grafana
* ELK Stack

Need:

* Open ports
* Scraping endpoints
* Service discovery

---

# 12. Network Troubleshooting

Daily DevOps Troubleshooting:

| Problem               | Troubleshooting |
| --------------------- | --------------- |
| Server unreachable    | ping            |
| DNS issue             | nslookup/dig    |
| Port blocked          | telnet/nc       |
| Service not listening | netstat/ss      |
| SSL issue             | openssl         |
| Packet issue          | tcpdump         |

---

# 13. API Gateway & Ingress

Used in Kubernetes microservices.

Examples:

* Kong
* NGINX Ingress
* Traefik

---

# 14. Observability Networking

Monitoring tools collect:

* Metrics
* Logs
* Traces

Need proper:

* Port access
* Service discovery
* Scraping configuration

---

# 15. DevOps Networking Architecture Flow

```text
User
 ↓
DNS
 ↓
Load Balancer
 ↓
Reverse Proxy
 ↓
Kubernetes Ingress
 ↓
Service
 ↓
Pod/Application
 ↓
Database
```

---

# Most Important Networking Topics for DevOps Interviews

1. OSI Model
2. TCP/IP
3. DNS
4. HTTP/HTTPS
5. Load Balancer
6. Reverse Proxy
7. Kubernetes Networking
8. Docker Networking
9. VPC & Cloud Networking
10. Firewall & Security Groups
11. SSL/TLS
12. API & API Gateway
13. Troubleshooting Commands
14. Ingress & Service Mesh
15. VPN & NAT

---

# Important Networking Commands for DevOps

```bash
ping
curl
wget
ssh
scp
netstat
ss
ip addr
ip route
traceroute
tracepath
tcpdump
iftop
nmap
dig
nslookup
host
telnet
nc
openssl
```

---

# Real-Time DevOps Networking Issues

| Issue                         | Cause                       |
| ----------------------------- | --------------------------- |
| Pod not reachable             | CNI issue                   |
| 502 Bad Gateway               | Reverse proxy/backend issue |
| SSL handshake failed          | Certificate problem         |
| DNS lookup failed             | DNS issue                   |
| Connection timeout            | Firewall/security group     |
| High latency                  | Network congestion          |
| Jenkins cannot connect GitHub | Port/DNS/proxy issue        |
| Prometheus cannot scrape      | Port blocked                |
