# Understanding Helm Components


## 1. Helm Charts

A **Helm chart** is a collection of files that describe a set of Kubernetes resources. It acts as a **package** for your Kubernetes application, similar to a **DEB** or **RPM** file in Linux.

### **Components of a Chart:**

* **Chart.yaml:** Metadata about the chart (name, version, etc.).
* **values.yaml:** Default configuration values.
* **templates/**: Directory containing Kubernetes manifests as templates.
* **charts/**: Directory for chart dependencies.
* **README.md:** Optional documentation.
# Components of a Helm Chart

A Helm chart contains files and folders used to deploy applications in Kubernetes.

---

# Main Components

| Component   | Purpose                       |
| ----------- | ----------------------------- |
| Chart.yaml  | Chart metadata                |
| values.yaml | Custom configuration values   |
| templates/  | Kubernetes manifest templates |
| charts/     | Dependency charts             |
| .helmignore | Ignore unnecessary files      |

---

# Helm Chart Structure

```text id="v7m2k5"
mychart/
 ├── Chart.yaml
 ├── values.yaml
 ├── charts/
 ├── templates/
 └── .helmignore
```

---

# 1. Chart.yaml

Contains chart information.

Example:

```yaml id="p3x8n1"
apiVersion: v2
name: ecommerce
version: 1.0.0
description: Flipkart application
```

---

## Purpose

Stores:

* Chart name
* Version
* Description
* Dependencies

---

# 2. values.yaml

Contains configurable values.

Example:

```yaml id="x5r1m7"
replicaCount: 3

image:
  repository: nginx
  tag: latest
```

---

## Purpose

Used to customize deployment without changing templates.

Example:

* Dev environment
* Production environment

---

# 3. templates/

Contains Kubernetes manifest templates.

Example:

```text id="k8m4q2"
templates/
   deployment.yaml
   service.yaml
   ingress.yaml
```

---

## Purpose

Helm dynamically generates Kubernetes YAML using template values.

---

# Example Template

```yaml id="n2v9r4"
replicas: {{ .Values.replicaCount }}
```

Helm replaces:

```text id="y6m1k8"
{{ .Values.replicaCount }}
```

with value from:

```text id="q1r5v3"
values.yaml
```

---

# 4. charts/

Contains dependency charts.

Example:

```text id="c4m8x7"
charts/
   mysql-chart
```

---

## Purpose

Used when one application depends on another.

Example:

```text id="d7p2n5"
Application depends on MySQL
```

---

# 5. .helmignore

Like `.gitignore`.

Used to ignore unnecessary files during chart packaging.

Example:

```text id="m9q3r1"
.git/
temp/
```

---

# Real Deployment Flow

```text id="t6x4k2"
values.yaml
      ↓
Templates
      ↓
Helm Generates YAML
      ↓
Kubernetes Resources Created
```

---

# Simple Understanding

```text id="w3m7v9"
Chart.yaml    → Information
values.yaml   → Configurations
templates/    → K8s YAML files
charts/       → Dependencies
```

---

# Interview One-Line Answer

> "The main components of a Helm chart are Chart.yaml, values.yaml, templates, charts, and .helmignore, which together define and manage Kubernetes application deployments."

### **Creating a Chart:**

```bash
helm create myapp
```

This generates a new chart structure under the `myapp` directory.

### **Installing a Chart:**

```bash
helm install my-nginx bitnami/nginx
```

Charts enable you to define complex applications, including deployments, services, config maps, and more, all bundled together for easy management.

---

## 2. Helm Repositories

A **Helm repository** is a place where Helm charts are stored and shared. It’s similar to a **package repository** in Linux (like APT or YUM repos).

### **Adding a Repository:**

```bash
helm repo add bitnami https://charts.bitnami.com/bitnami
```

### **Listing Repositories:**

```bash
helm repo list
```

### **Updating Repositories:**

```bash
helm repo update
```

Repositories make it easy to organize, store, and distribute Helm charts, and they support versioning, so you can choose specific versions of a chart to install.

---

## 3. Helm Releases

A **Helm release** is a specific instance of a chart that has been deployed to your Kubernetes cluster. You can think of it as a **deployed version of your application.**

### **Creating a Release:**

```bash
helm install myapp ./myapp
```

### **Listing Releases:**

```bash
helm list
```

### **Upgrading a Release:**

```bash
helm upgrade myapp ./myapp
```

### **Rolling Back a Release:**

```bash
helm rollback myapp 1
```

### **Deleting a Release:**

```bash
helm uninstall myapp
```

Releases are useful for tracking deployed versions, performing rollbacks in case of failures, and managing multiple instances of the same chart.

---

## Summary

* **Charts** are packages that define Kubernetes resources.
* **Repositories** are storage locations for Helm charts.
* **Releases** are deployed instances of a chart.

