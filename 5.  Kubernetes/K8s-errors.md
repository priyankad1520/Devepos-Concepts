# Kubernetes Issues and Troubleshooting for DevOps Engineers

Kubernetes troubleshooting is one of the most important skills for a DevOps engineer.

Most common issues happen in:

* Pods
* Nodes
* Networking
* Storage
* Deployments
* Services
* DNS
* Ingress
* Resource usage
---
## Real-Time DevOps Troubleshooting Flow

```text id="crz0jk"
Application Down
       ↓
Check Pods
kubectl get pods
       ↓
Check Logs
kubectl logs pod-name
       ↓
Describe Pod
kubectl describe pod pod-name
       ↓
Check Service
kubectl get svc
       ↓
Check Node
kubectl get nodes
       ↓
Fix Issue
       ↓
Restart Deployment
kubectl rollout restart deployment app
```
## 1. Pod Status = CrashLoopBackOff
- Meaning: Container starts and crashes repeatedly.

**Possible Causes**

* Application error
* Wrong environment variable
* Missing dependency
* Database connection failure
* Wrong startup command
#### Troubleshooting Commands
```bash id="3a63cl"
# Check Pod
kubectl get pods

# Check Logs
kubectl logs pod-name

# Check Previous Logs
kubectl logs pod-name --previous

# Describe Pod
kubectl describe pod pod-name
```
#### Solution Example
```bash id="k1ykmg"
# Wrong DB Password

# Update Secret:
kubectl edit secret db-secret

# Restart Deployment:
kubectl rollout restart deployment app
```
## 2. ImagePullBackOff / ErrImagePull
- Meaning: Kubernetes cannot download Docker image.

**Causes**

* Wrong image name
* Wrong image tag
* Private registry authentication issue
* Docker registry unavailable
#### Troubleshooting

```bash id="3j9n6v"
kubectl describe pod pod-name

# Look for:
Failed to pull image
```
#### Solution
```yaml id="3mjlwm"
# Correct Image Name
image: nginx:latest

# Restart Deployment
kubectl rollout restart deployment nginx
```
## 3. Pod Status = Pending
- Meaning: Pod is not scheduled on any node.

 **Causes**

* Insufficient CPU/Memory
* Node taints
* PVC issue
* Node unavailable
#### Troubleshooting

```bash id="y45ckm"
kubectl describe pod pod-name

# Check Events section:
0/3 nodes are available
```
#### Solutions
- Increase Cluster Resources
- Reduce Resource Requests

```yaml id="e8zh5f"
resources:
  requests:
    memory: "256Mi"
```

```bash id="3s1s8f"
# Check Nodes
kubectl get nodes
```
## 4. Node Status = NotReady
- Meaning: Worker node disconnected from cluster.

**Causes**

* Kubelet stopped
* Network issue
* Disk full
* CPU/Memory high
### Troubleshooting

```bash id="y7vh14"
kubectl get nodes
kubectl describe node node-name
```
## Solution
```bash id="qv29ut"
# Restart Kubelet
sudo systemctl restart kubelet

# Check Disk Space
df -h
```
## 5. Service Not Accessible
- Meaning: Application cannot be accessed externally.

**Causes**

* Wrong service type
* Wrong targetPort
* Pod labels mismatch
* Network policy issue

#### Troubleshooting
```bash id="zxlm83"
# Check Services
kubectl get svc

# Describe Service
kubectl describe svc nginx

# Check Endpoints
kubectl get endpoints
```
#### Solution
```yaml id="vjlwmz"
# Correct Selector Labels
selector:
  app: nginx
```
```yaml id="o2qjlwm"
# Verify Ports
ports:
- port: 80
  targetPort: 8080
```
## 6. Pod Cannot Communicate With Another Pod

**Causes**

* Network policy
* DNS issue
* Service issue

#### Troubleshooting
```bash id="n2vjpa"
# Enter Pod
kubectl exec -it pod-name -- sh

# Ping Service
ping service-name

# DNS Check
nslookup service-name
```
#### Solution
```bash id="yq0gcf"
# Restart CoreDNS
kubectl rollout restart deployment coredns -n kube-system
```
## 7. OOMKilled (Out Of Memory)
- Meaning: Container exceeded memory limit.
#### Troubleshooting

```bash id="jlwmx0"
kubectl describe pod pod-name

#Look for: OOMKilled
```
#### Solution
```yaml id="jlwm8f"
# Increase Memory Limit
resources:
  limits:
    memory: "1Gi"
```
## 8. PVC (Persistent Volume Claim) Pending
- Meaning: Storage not allocated.

**Causes**

* No storage class
* No available PV
* Wrong access mode

#### Troubleshooting

```bash id="6rjlwm"
kubectl get pvc
kubectl describe pvc pvc-name
```
#### Solution
```bash id="jlwm6k"
# Check StorageClass
kubectl get storageclass

# Create PV
kind: PersistentVolume
```
## 9. ConfigMap or Secret Not Working
**Causes**
* Wrong mount path
* Wrong key name
* Pod not restarted

#### Troubleshooting

```bash id="jlwm4c"
kubectl describe pod pod-name
```
#### Solution
```bash id="jlwm3v"
# Restart Deployment
kubectl rollout restart deployment app
```
## 10. Deployment Failed
**Causes**

* Invalid YAML
* Wrong image
* Port conflict
#### Troubleshooting

```bash id="jlwm7x"
kubectl get deploy
kubectl describe deployment app
```
#### Solution
```bash id="jlwm5m"
# Validate YAML
kubectl apply -f deployment.yaml --dry-run=client
```
## 11. Ingress Not Working
**Causes**

* Ingress controller missing
* Wrong host/path
* DNS issue

#### Troubleshooting

```bash id="jlwm1y"
kubectl get ingress
kubectl describe ingress app-ingress
```

#### Solution
```bash id="jlwm0p"
# Install NGINX Ingress Controller
kubectl apply -f ingress-controller.yaml
```
## 12. High CPU Usage

#### Troubleshooting

```bash id="jlwm8n"
kubectl top pod
kubectl top node
```
#### Solution
```bash id="jlwm6s"
# Scale Application
kubectl scale deployment app --replicas=5
```
### 13. DNS Resolution Failure
- Symptoms: Pods cannot resolve service names.

#### Troubleshooting

```bash id="jlwm4f"
kubectl get pods -n kube-system

# Check CoreDNS:
kubectl logs -n kube-system deployment/coredns
```
#### Solution
```bash id="jlwm1d"
# Restart DNS
kubectl rollout restart deployment coredns -n kube-system
```

#### 14. Kubernetes API Server Not Responding
- Symptoms: `Unable to connect to the server`
#### Troubleshooting

```bash id="jlwm3g"
kubectl cluster-info
```
#### Solution
```bash id="jlwm9r"
# Restart API Server
# (Self-managed cluster)
sudo systemctl restart kube-apiserver
```
### 15. Worker Node Disk Full
- Symptoms: Pods failing randomly.
#### Troubleshooting
```bash id="jlwm2q"
df -h
```
#### Solution
```bash id="jlwm5t"
# Remove Unused Docker Images
docker system prune -a
```
## 16. Pod Stuck in Terminating State
**Causes**

* Finalizer issue
* Volume issue
## Solution
```bash id="jlwm7u"
# Force Delete Pod
kubectl delete pod pod-name --force --grace-period=0
```
## 17. Helm Release Failed

#### Troubleshooting

```bash id="jlwm8i"
helm list
helm status release-name
```
#### Solution
```bash id="jlwm0c"
# Rollback Helm
helm rollback release-name 1
```

## 18. Certificate Expired
- Symptoms: TLS/SSL errors.
#### Troubleshooting

```bash id="jlwm4y"
kubectl get csr
```
#### Solution
```bash id="jlwm3t"
# Renew Certificates
kubeadm certs renew all
```

## 19. Container Cannot Start
**Causes**

* Wrong command
* Missing file
* Permission denied

#### Troubleshooting

```bash id="jlwm9v"
kubectl describe pod pod-name
```
#### Solution
```yaml id="jlwm2n"
# Check Startup Command
command: ["nginx"]
```
## 20. Namespace Stuck in Terminating

#### Solution
```bash id="jlwm5r"
# Remove Finalizers
kubectl get namespace namespace-name -o json
# Edit finalizers manually.
```
## Most Important Troubleshooting Commands

| Command                 | Purpose           |
| ----------------------- | ----------------- |
| kubectl get pods        | View pods         |
| kubectl describe pod    | Detailed pod info |
| kubectl logs            | Check logs        |
| kubectl get events      | Cluster events    |
| kubectl top pod         | CPU/Memory        |
| kubectl exec            | Access container  |
| kubectl get svc         | Check services    |
| kubectl get nodes       | Node status       |
| kubectl rollout undo    | Rollback          |
| kubectl apply --dry-run | Validate YAML     |


## Real-Time Troubleshooting Flow Used by DevOps Engineers

```text id="jlwm8m"
Issue Reported
      ↓
Check Pods
      ↓
kubectl get pods
      ↓
Check Logs
      ↓
kubectl logs pod-name
      ↓
Describe Resource
      ↓
kubectl describe pod/service/deployment
      ↓
Identify Root Cause
      ↓
Fix YAML / Resource / Config
      ↓
Restart Deployment
      ↓
Verify Application
```

---

| **Production-Level Troubleshooting Mindset** |
| Problem Area      | Check First |
| ----------------- | ----------- |
| Pod issue         | Logs        |
| Service issue     | Endpoints   |
| Network issue     | DNS         |
| Node issue        | kubelet     |
| Storage issue     | PVC/PV      |
| Deployment issue  | Events      |
| Performance issue | CPU/Memory  |
| **Quick Troubleshooting Cheat Sheet** |
| Issue             | Command                     |
| ----------------- | --------------------------- |
| Pod crash         | kubectl logs pod-name       |
| Pod pending       | kubectl describe pod        |
| Node issue        | kubectl get nodes           |
| Service issue     | kubectl describe svc        |
| High CPU          | kubectl top pod             |
| Deployment failed | kubectl rollout status      |
| DNS problem       | nslookup kubernetes.default |
| Storage issue     | kubectl get pvc             |
| Network issue     | kubectl get networkpolicy   |
| **Most Important Troubleshooting Commands** |
| Command              | Purpose                  |
| -------------------- | ------------------------ |
| kubectl get pods     | Check pod status         |
| kubectl describe pod | Detailed troubleshooting |
| kubectl logs         | Application logs         |
| kubectl exec         | Access container         |
| kubectl get events   | Cluster events           |
| kubectl top pod      | CPU/memory usage         |
| kubectl get svc      | Check services           |
| kubectl get nodes    | Node status              |
| kubectl rollout undo | Rollback deployment      |

## 1. Pod Status Troubleshooting
```bash id="1m5b0w"
# Check Pods
kubectl get pods

# Detailed Information
kubectl describe pod pod-name

# Check Logs
kubectl logs pod-name
```
## 2. CrashLoopBackOff
- Meaning: Container starts and crashes repeatedly.

**Common Causes**

* Application error
* Wrong environment variables
* Database connection failure
* Missing files
* Port conflict

#### Troubleshooting Steps
```bash id="4mjk4u"
# Step 1: Check Logs
kubectl logs pod-name

# Step 2: Describe Pod
kubectl describe pod pod-name

# Step 3: Enter Container
kubectl exec -it pod-name -- /bin/bas
```
#### Example

```text id="4l5olw"
Error: Database connection failed
```
**Fix**

* Verify DB hostname
* Check DB credentials
* Check secret/configmap

### 3. ImagePullBackOff
- Meaning: Kubernetes cannot pull Docker image.

**Common Causes**

* Wrong image name
* Wrong image tag
* Private registry authentication issue
* Internet issue

#### Troubleshooting
```bash id="bdc45h"
# Check Pod Details
kubectl describe pod pod-name
```
#### Example Error

```text id="1ftwnn"
Failed to pull image "ngnix:latest"

# Spelling mistake: ngnix
# Correct: nginx

# Fix Deployment
kubectl edit deployment nginx
```
### 4. Pod Pending State
- Meaning: Pod is not scheduled to any node.

**Common Causes**

* Insufficient CPU/memory
* Node taints
* PVC issue
* Node not ready
#### Troubleshooting
```bash id="r0s5tr"
# Check Pod
kubectl describe pod pod-name

# Check Nodes
kubectl get nodes

# Check Resource Usage
kubectl top node
```
#### Example Error

```text id="9u7gw8"
0/2 nodes available: insufficient memory
```

##### Fix

* Increase node size
* Add worker node
* Reduce pod resources

### 5. OOMKilled (Out of Memory)
- Meaning: Container exceeded memory limit.

```bash id="whtz99"
# Check Pod Status
kubectl describe pod pod-name
```
#### Example

```text id="v9fwd8"
Reason: OOMKilled
```
##### Fix
Example YAML:

```yaml id="xjn74t"
# Increase Memory Limit
resources:
  requests:
    memory: "256Mi"
  limits:
    memory: "512Mi"
```
```bash id="rlnz7j"
# Reapply YAML
kubectl apply -f deployment.yaml
```
### 6. Service Not Accessible
- Meaning: Application not reachable.
#### Troubleshooting
```bash id="2c8g10"
# Check Service
kubectl get svc

# Describe Service
kubectl describe svc service-name

# Check Endpoints
kubectl get endpoints
```
**Common Causes**

* Wrong selector labels
* Wrong targetPort
* Pod not running

##### Example
```yaml id="qwl7x3"
# Service Selector
selector:
  app: nginx
```
```yaml id="z8gt9n"
# Pod Label
labels:
  app: apache
```
- Problem isLabels do not match.
### 7. Node Not Ready
- Meaning: Worker node unavailable.
```bash id="5fd2jk"
# Check Nodes
kubectl get nodes

# Detailed Information
kubectl describe node node-name
```
**Common Causes**

* Kubelet stopped
* Disk full
* Network issue
* CPU overload

**Fix**
```bash id="a7j4rm"
# Restart Kubelet
sudo systemctl restart kubelet

# Check Disk
df -h
```
### 8. DNS Resolution Issue
- Symptoms: Pods cannot communicate using service names.
#### Troubleshooting
```bash id="7j5yl9"
# Enter Pod
kubectl exec -it pod-name -- sh

# Test DNS
nslookup kubernetes.default

# Check CoreDNS
kubectl get pods -n kube-system

# Restart CoreDNS
kubectl rollout restart deployment coredns -n kube-system
```
### 9. PVC Pending Issue
- Meaning: Persistent storage not attached.
```bash id="3gf1s6"
# Check PVC
kubectl get pvc

# Describe PVC
kubectl describe pvc pvc-name
```
**Common Causes**

* No storage class
* Storage unavailable

```bash id="37jlwm"
# Check Storage Class
kubectl get sc
```
### 10. Deployment Failed
```bash id="6zv6pa"
# Check Deployment
kubectl get deploy

# Describe Deployment
kubectl describe deployment deployment-name

# Check Rollout
kubectl rollout status deployment/nginx

# Rollback Deployment
kubectl rollout undo deployment/nginx
```
### 11. Container Creating Issue
- Meaning: Container stuck while starting.

**Common Causes**

* Volume mounting issue
* Image pull slow
* Secret/configmap missing
#### Troubleshooting

```bash id="r0j5sj"
kubectl describe pod pod-name
```
### 12. ConfigMap or Secret Missing
```bash id="g4v23t"
# Check ConfigMaps
kubectl get configmap

# Check Secrets
kubectl get secrets

# Describe Secret
kubectl describe secret secret-name
```
### 13. Ingress Not Working
```bash id="5j6w6q"
# Check Ingress
kubectl get ingress

# Describe Ingress
kubectl describe ingress ingress-name

# Check Ingress Controller
kubectl get pods -n ingress-nginx
```

### 14. High CPU Usage
```bash id="9zhwbt"
# Check Resource Usage
kubectl top pod

# Node Usage
kubectl top node
```
**Fix**

* Increase resources
* Scale deployment
* Optimize application

### 15. Pod Communication Issue

```bash id="u1l7iy"
# Test Connectivity
kubectl exec -it pod1 -- ping pod2-ip

# Check Service
kubectl get svc

# Check Network Policies
kubectl get networkpolicy
```
### 16. Namespace Issue
```bash id="p5w3mg"
# View Namespaces
kubectl get ns
```

```bash id="wl0q87"
# Problem Example: Application deployed in wrong namespace.
# Fix
kubectl get pods -n dev
```
### 17. Kubernetes API Server Issue
- Symptoms: kubectl commands not working.

```bash id="r5dxw3"
# Check Cluster
kubectl cluster-info

# Check API Server Pod
kubectl get pods -n kube-system
```
### 18. etcd Issue
- Meaning: Cluster database issue.
- Symptoms: Cluster unstable, Data missing

```bash id="ax1k6f"
# Check etcd
kubectl get pods -n kube-system
```
### 19. Disk Pressure Issue

```bash id="y0u4ql"
# Check Node
kubectl describe node node-name

# Example
DiskPressure=True

# Fix: Clean logs and  Remove unused Docker images
```
### 20. NetworkPolicy Blocking Traffic
```bash id="t7f3n0"
# Check Policies
kubectl get networkpolicy

# Describe Policy
kubectl describe networkpolicy policy-name
```
