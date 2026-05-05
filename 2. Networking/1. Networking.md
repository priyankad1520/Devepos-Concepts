# Networking Concepts Full Explanation

Networking is the process of connecting computers, servers, devices, and applications to communicate and share data.

Networking allows systems to exchange information over local networks and the internet.

Networking is very important in DevOps, Cloud Computing, Kubernetes, Docker, CI/CD, and Server Management.

Applications, servers, containers, and cloud services communicate using networking concepts.

## What is Network

A Network is a group of connected devices that communicate and share resources with each other.

Networks can share files, internet connections, printers, and applications.

Devices communicate using networking protocols and IP addresses.

## Types of Networks

LAN called Local Area Network connects devices within a small area, such as office or home.

WAN called Wide Area Network connects networks across large geographical areas.

MAN called Metropolitan Area Network connects networks across cities.

PAN called Personal Area Network connects personal devices like phones and laptops.

## Network Devices

Router connects different networks together and forwards data packets between networks.

Switch connects devices inside the same network and transfers data using MAC addresses.

Hub broadcasts data to all connected devices without filtering.

Firewall filters incoming and outgoing network traffic for security.

Modem connects local networks to internet service providers.

Access Point provides wireless network connectivity for devices.

Load Balancer distributes traffic across multiple servers for performance and availability.

## IP Address

IP Address is a unique identifier assigned to each device in a network.

IP addresses help systems identify source and destination devices.

IPv4 uses 32-bit addresses.

Example IPv4 address:

```text id="5a1hxe"
192.168.1.10
```

IPv6 uses 128-bit addresses and provides a larger address range.

Example IPv6 address:

```text id="f6uzg7"
2001:0db8:85a3:0000:0000:8a2e:0370:7334
```

## Public and Private IP

Public IP is accessible over the internet.

Private IP is used inside internal local networks.

Private IP ranges:

```text id="p4q7dj"
10.0.0.0 - 10.255.255.255
172.16.0.0 - 172.31.255.255
192.168.0.0 - 192.168.255.255
```

## Subnet Mask

Subnet Mask separates network portion and host portion of an IP address.

Subnetting improves network organization and reduces traffic.

Example subnet mask:

```text id="x7pby4"
255.255.255.0
```

## CIDR Notation

CIDR called Classless Inter-Domain Routing represents subnet masks compactly.

Example:

```text id="wntk5r"
192.168.1.0/24
```

`/24` means first 24 bits are network bits.

## Gateway

Gateway is the device that connects one network to another network.

Default Gateway allows devices to communicate outside their local network.

Routers commonly act as gateways.

## MAC Address

MAC Address is a physical hardware address assigned to network interface cards.

MAC addresses operate at Data Link Layer.

Example MAC Address:

```text id="spmz7z"
00:1A:2B:3C:4D:5E
```

## Port Numbers

Ports are logical communication endpoints used by applications and services.

Each service runs on a specific port number.

Common ports:

```text id="1x09gn"
22   SSH
80   HTTP
443  HTTPS
21   FTP
25   SMTP
53   DNS
3306 MySQL
5432 PostgreSQL
8080 Jenkins
6443 Kubernetes API Server
```

## Protocols

Protocols define communication rules between systems.

### HTTP

HTTP called HyperText Transfer Protocol transfers website data.

HTTP uses port `80`.

### HTTPS

HTTPS is secure HTTP communication using SSL/TLS encryption.

HTTPS uses port `443`.

### SSH

SSH called Secure Shell provides secure remote login access.

SSH uses port `22`.

### FTP

FTP called File Transfer Protocol transfers files between systems.

FTP uses port `21`.

### SMTP

SMTP called Simple Mail Transfer Protocol sends emails.

SMTP uses port `25`.

### DNS

DNS called Domain Name System converts domain names into IP addresses.

DNS uses port `53`.

## TCP and UDP

TCP called Transmission Control Protocol provides reliable communication.

TCP guarantees packet delivery and maintains connection state.

TCP is slower but reliable.

Examples using TCP are HTTP, HTTPS, SSH, and FTP.

UDP called User Datagram Protocol provides fast communication without delivery guarantee.

UDP is faster but less reliable.

Examples using UDP are video streaming, gaming, and DNS queries.

## OSI Model

OSI called Open Systems Interconnection Model explains network communication in 7 layers.

### Layer 1 Physical Layer

Physical Layer handles cables, signals, and hardware transmission.

### Layer 2 Data Link Layer

Data Link Layer handles MAC addresses and switching.

### Layer 3 Network Layer

Network Layer handles IP addressing and routing.

### Layer 4 Transport Layer

Transport Layer handles TCP and UDP communication.

### Layer 5 Session Layer

Session Layer manages communication sessions between systems.

### Layer 6 Presentation Layer

Presentation Layer handles encryption, compression, and data formatting.

### Layer 7 Application Layer

Application Layer provides services like HTTP, FTP, DNS, and SMTP.

## TCP/IP Model

TCP/IP Model is the practical networking model used on the internet.

Layers are Network Access Layer, Internet Layer, Transport Layer, and Application Layer.

## DNS

DNS converts domain names into IP addresses.

Example:

```text id="sywml4"
google.com -> 142.250.183.14
```

DNS improves usability because users remember names instead of IP addresses.

## NAT

NAT called Network Address Translation converts private IP addresses into public IP addresses.

NAT allows multiple devices to share one public IP address.

## DHCP

DHCP called Dynamic Host Configuration Protocol automatically assigns IP addresses to devices.

DHCP reduces manual network configuration work.

## Firewall

Firewall filters network traffic based on security rules.

Firewalls protect systems from unauthorized access.

Linux firewalls include `iptables` and `firewalld`.

## VPN

VPN called Virtual Private Network creates secure encrypted connections over the internet.

VPN allows remote users to access internal company networks securely.

## Proxy

Proxy Server acts as an intermediary between client and server.

Forward Proxy handles client requests to internet servers.

Reverse Proxy handles incoming requests before reaching backend servers.

Nginx is commonly used as a reverse proxy server.

## Load Balancer

Load Balancer distributes incoming traffic across multiple servers.

Load balancing improves availability, scalability, and performance.

Layer 4 Load Balancer works at Transport Layer using IP and ports.

Layer 7 Load Balancer works at Application Layer using HTTP and HTTPS traffic.

## SSL and TLS

SSL called Secure Sockets Layer secures network communication using encryption.

TLS called Transport Layer Security is the modern secure replacement for SSL.

HTTPS uses SSL/TLS certificates for encrypted communication.

## Network Commands in Linux

Check IP address:

```bash id="r5dbz7"
ip addr
```

Check connectivity:

```bash id="yvzn6m"
ping google.com
```

Check open ports:

```bash id="ub9o8g"
netstat -tulnp
```

Modern replacement for netstat:

```bash id="6i9g59"
ss -tulnp
```

Check DNS resolution:

```bash id="r9mjlwm"
nslookup google.com
```

Trace network route:

```bash id="41i2y9"
traceroute google.com
```

Download files:

```bash id="zkq3fx"
wget https://example.com/file.zip
```

Transfer data using APIs:

```bash id="95fgm4"
curl https://example.com
```

## Networking in Docker

Docker creates virtual networks for containers.

Bridge Network is default Docker network.

Containers communicate using container IP addresses.

Docker supports Host, Bridge, and Overlay networking modes.

## Networking in Kubernetes

Kubernetes networking allows communication between Pods, Services, and external systems.

Each Pod gets a unique IP address.

Kubernetes Services expose applications inside or outside the cluster.

Ingress manages external HTTP and HTTPS traffic routing.

CNI called Container Network Interface provides Kubernetes networking functionality.

## Cloud Networking

Cloud providers offer virtual networking services.

AWS uses VPC called Virtual Private Cloud.

Azure uses Virtual Network called VNet.

Google Cloud uses VPC networks.

Cloud networking includes subnets, routing tables, NAT gateways, and security groups.

## Networking Security

Use firewalls to filter unauthorized traffic.

Use HTTPS instead of HTTP for secure communication.

Use SSH keys instead of passwords when possible.

Close unused ports to reduce attack surface.

Monitor network logs and suspicious traffic.

Use VPN for secure remote access.

## Networking Troubleshooting

Check IP configuration using `ip addr`.

Check connectivity using `ping`.

Check DNS resolution using `nslookup` or `dig`.

Check open ports using `ss -tulnp`.

Check routing path using `traceroute`.

Check firewall rules using `iptables -L`.

Check logs for errors and connectivity issues.

## Networking Workflow

Client sends request to server using IP address and port.

DNS resolves domain name into IP address.

Packets travel through routers and switches across networks.

TCP or UDP protocols manage data communication.

Server processes request and sends response back to client.

Firewall and load balancers manage security and traffic distribution.

Applications communicate continuously using networking protocols and ports.
