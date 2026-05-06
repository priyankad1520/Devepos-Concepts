# What is CRI-O?

CRI-O is a lightweight container runtime specially designed for Kubernetes.

It is used to run containers inside Kubernetes.

---

# Simple Definition

> "CRI-O is a container runtime that helps Kubernetes run containers."

## Container Runtime

A container runtime is the software responsible for running and managing containers on a system.

It handles:

* Starting containers
* Stopping containers
* Managing container resources
* Isolating containers

Examples:

* Docker
* containerd
* CRI-O

---

# Why CRI-O Came?

Earlier Kubernetes used:

```text id="9h5ch7"
Docker
```

as container runtime.

But Kubernetes later removed direct Docker support because:

* Docker has many extra features
* Kubernetes only needs container runtime features
* Docker was heavier

So Kubernetes started using CRI-compatible runtimes like:

| Runtime    | Purpose                 |
| ---------- | ----------------------- |
| CRI-O      | Lightweight K8s runtime |
| containerd | Popular runtime         |
| Docker     | Full container platform |

---

# Full Form

```text id="mrx2kw"
CRI = Container Runtime Interface
O   = Open Container Initiative (OCI)
```

---

# Main Purpose

CRI-O acts as a bridge between:

```text id="8m0g1d"
Kubernetes
      ↓
CRI-O
      ↓
OCI Runtime (runc)
      ↓
Containers
```

---

# Architecture

```text id="3pvk8h"
Kubernetes API
      ↓
Kubelet
      ↓
CRI-O
      ↓
runc
      ↓
Container
```

---

# What Does CRI-O Do?

CRI-O handles:

* Pulling container images
* Starting containers
* Stopping containers
* Managing container lifecycle
* Communicating with Kubernetes

---

# Important Concept

## Kubernetes Does NOT Run Containers Directly

Kubernetes uses:

```text id="3e8m7p"
Container Runtime
```

Examples:

* CRI-O
* containerd

These runtimes actually run the containers.

---

# Difference Between Docker and CRI-O

| Feature | Docker | CRI-O |
|---|---|
| Full platform | Yes | No |
| Kubernetes focused | No | Yes |
| Lightweight | Less | More |
| Built only for K8s | No | Yes |
| CLI available | docker | crictl |
| Uses OCI standard | Yes | Yes |

---

# Real Flow in Kubernetes

When you run:

```bash id="7r4d2d"
kubectl apply -f app.yaml
```

Flow:

```text id="hn0vcz"
Kubernetes Scheduler
      ↓
Kubelet on Node
      ↓
CRI-O
      ↓
Pull Image
      ↓
Create Container
      ↓
Run Pod
```

---

# CRI-O Uses OCI Runtime

Usually:

```text id="p6j6rq"
runc
```

runc is low-level runtime that actually creates Linux containers using:

* namespaces
* cgroups

---

# Common Commands

Check runtime:

```bash id="pffm4g"
kubectl get nodes -o wide
```

---

Check CRI-O service:

```bash id="t9ppj8"
systemctl status crio
```

---

Start service:

```bash id="4d61dy"
systemctl start crio
```

---

Enable service:

```bash id="09v16x"
systemctl enable crio
```

---

# crictl Command

CRI-O uses:

```text id="sk4f0i"
crictl
```

instead of Docker CLI.

---

Examples:

## List containers

```bash id="3mhk4f"
crictl ps
```

## List images

```bash id="aql8kz"
crictl images
```

## Pull image

```bash id="n58f4t"
crictl pull nginx
```

---

# Why Companies Use CRI-O?

Because it is:

* Lightweight
* Fast
* Secure
* Kubernetes-native
* Less overhead

---

# CRI-O vs containerd

| Feature | CRI-O | containerd |
|---|---|
| Built only for K8s | Yes | No |
| CNCF project | Yes | Yes |
| Popularity | Medium | Very High |
| Lightweight | Yes | Yes |

---

# Important DevOps Interview Question

## Does Kubernetes need Docker?

Answer:

> "No. Kubernetes does not require Docker. It can use CRI-compatible runtimes like CRI-O or containerd."

---

# Simple Real-Time Analogy

```text id="6wrzjx"
Kubernetes = Manager
CRI-O      = Worker
Container  = Actual running application
```

Kubernetes tells CRI-O:

```text id="0kp40s"
"Run this container"
```

CRI-O runs it.

---

# One-Line Interview Answer

> "CRI-O is a lightweight container runtime designed specifically for Kubernetes to run OCI-compatible containers."
