# Kubernetes (K8s) Commands Step-by-Step Process for a DevOps Engineer

Kubernetes is used to:

* Deploy applications
* Manage containers
* Scale applications
* Self-healing
* Load balancing
* CI/CD deployments

---

### 1. Check Kubernetes Cluster
- **Check Cluster Information:** `kubectl cluster-info`
- **Why We Use This:** Checks whether cluster is running or not.

### 2. Check Kubernetes Nodes
- **View Nodes:** `kubectl get nodes`
- **Detailed Node Information:** `kubectl describe node node-name`
- **What is Node?**A worker machine where pods run.

### 3. Check Namespaces
```bash id="g20e8t"
# View Namespaces
kubectl get ns
OR
kubectl get namespaces
```
> Why We Use Namespace? Separates environments: dev, test, prod

### 4. Create Namespace

```bash id="m6zdf8"
kubectl create namespace dev
```
### 5. Check Pods
```bash id="8vv1zw"
# View Pods
kubectl get pods

# View Pods in All Namespaces
kubectl get pods -A

# Wide Output
kubectl get pods -o wide
```
> What is Pod?. Smallest deployable unit in Kubernetes.

### 6. Create Pod
```bash id="wl4bku"
# Using YAML File
kubectl apply -f pod.yaml
```
> Why We Use YAML?. Infrastructure as Code (IaC).

### 7. Describe Pod

```bash id="a5xrfy"
kubectl describe pod pod-name
```
> Why We Use This. Checks: Events, Errors, Container status, Node details

### 8. Check Pod Logs

```bash id="s3q6yu"
kubectl logs pod-name

# Live Logs
kubectl logs -f pod-name
```
> Why DevOps Engineers Use Logs: Troubleshooting application issues.

### 9. Enter Into Pod

```bash id="9x59ye"
kubectl exec -it pod-name -- /bin/bash
# OR
kubectl exec -it pod-name -- sh
```
> Why We Use This: To access container terminal.

### 10. Delete Pod

```bash id="9ew11f"
kubectl delete pod pod-name
```

### 11. Deploy Application
```bash id="3lzocg"
# Create Deployment
kubectl create deployment nginx --image=nginx
```

### 12. Check Deployments

```bash id="lby8t9"
kubectl get deployments
# OR
kubectl get deploy
```
### 13. Scale Deployment
```bash id="ayjkm8"
# Increase Pods
kubectl scale deployment nginx --replicas=5
```
> What Happens?. Kubernetes creates 5 pods.

### 14. Edit Deployment
```bash id="o1w5l0"
kubectl edit deployment nginx
```

### 15. Rollout Status

```bash id="c2v5b9"
kubectl rollout status deployment/nginx
```
> Why We Use This: Checks deployment progress.

### 16. Rollback Deployment

```bash id="q08c56"
kubectl rollout undo deployment/nginx
```
> Why DevOps Engineers Use This: Rollback failed deployments.

### 17. Expose Deployment
```bash id="3y5n7v"
# Create Service
kubectl expose deployment nginx --type=NodePort --port=80
```
> What Happens?. Makes application accessible.

### 18. Check Services

```bash id="b89e2k"
kubectl get svc
# OR
kubectl get services
```

### 19. Describe Service

```bash id="63ruqj"
kubectl describe svc nginx
```
### 20. Port Forwarding

```bash id="5h8t7i"
kubectl port-forward pod-name 8080:80
```
> Why We Use This: Access application locally.

### 21. Apply YAML File

```bash id="g0r7go"
kubectl apply -f deployment.yaml
```
Why DevOps Engineers Use This
- Deploy: Pods, Services, Deployments, ConfigMaps, Secrets

### 22. Delete Resources

```bash id="4x1l1g"
# Delete YAML Resources
kubectl delete -f deployment.yaml
```

### 23. Check Events

```bash id="xgkz4u"
kubectl get events
```
> Why We Use This: Troubleshoot cluster issues.

### 24. Resource Usage
```bash id="8bdvbx"
# Pod CPU and Memory
kubectl top pod

# Node CPU and Memory
kubectl top node
```
### 25. ConfigMaps
```bash id="d6v8tx"
# Create ConfigMap
kubectl create configmap app-config --from-literal=ENV=prod

# View ConfigMaps
kubectl get configmaps
```
### 26. Secrets
```bash id="0b2j6g"
# Create Secret
kubectl create secret generic db-secret --from-literal=password=admin123

# View Secrets
kubectl get secrets
```
### 27. Check All Resources
```bash id="e8tkfd"
kubectl get all
```
### 28. Labels
```bash id="xv01ul"
# Add Label
kubectl label pod nginx env=prod

# Show Labels
kubectl get pods --show-labels
```

### 29. Taints and Tolerations
```bash id="gnyh40"
# View Taints
kubectl describe node node-name

# Add Taint
kubectl taint nodes node-name env=prod:NoSchedule
```
> Why We Use This: Controls pod scheduling.

### 30. Drain Node

```bash id="3g93r9"
kubectl drain node-name --ignore-daemonsets
```
> Why DevOps Engineers Use This: Before maintenance.

### 31. Uncordon Node

```bash id="j5m8t9"
kubectl uncordon node-name
```
> What Happens?. Node becomes schedulable again.

### 32. Cordon Node

```bash id="11z8ei"
kubectl cordon node-name
```
> What Happens?. Stops new pods from scheduling.

### 33. Check Persistent Volumes

```bash id="mv1s4q"
kubectl get pv

# Check PVC
kubectl get pvc
```
### 34. Restart Deployment

```bash id="v70n1p"
kubectl rollout restart deployment nginx
```

### 35. Copy File to Pod

```bash id="8k4vbo"
kubectl cp test.txt pod-name:/tmp/
```

### 36. Copy File From Pod

```bash id="gq71vh"
kubectl cp pod-name:/tmp/test.txt .
```

### 37. Check API Resources

```bash id="9j4ml7"
kubectl api-resources
```
### 38. Explain YAML Fields

```bash id="cyfc0g"
kubectl explain deployment

# Deep Explanation
kubectl explain deployment.spec
```
### 39. Check Context

```bash id="dczmkl"
kubectl config current-context
```
### 40. View Kubeconfig

```bash id="0j4n7o"
kubectl config view
```
## Real-Time DevOps Kubernetes Workflow

##### Step 1: Check Cluster

```bash id="t7xt2u"
kubectl get nodes
```
##### Step 2: Deploy Application

```bash id="j9z57o"
kubectl apply -f deployment.yaml
```
##### Step 3: Check Pods

```bash id="eh4v7h"
kubectl get pods
```
##### Step 4: Check Logs

```bash id="s3o38m"
kubectl logs pod-name
```
##### Step 5: Expose Application

```bash id="zw3fwl"
kubectl expose deployment nginx --type=LoadBalancer --port=80
```

##### Step 6: Verify Service

```bash id="7gvd7z"
kubectl get svc
```
##### Step 7: Scale Application

```bash id="gc0uf1"
kubectl scale deployment nginx --replicas=10
```
##### Step 8: Monitor Resources

```bash id="0iygq5"
kubectl top pod
```
##### Step 9: Rollback if Failure

```bash id="qcm7v2"
kubectl rollout undo deployment/nginx
```

## Important Kubernetes Commands Used Daily

| Command          | Purpose               |
| ---------------- | --------------------- |
| kubectl get pods | View pods             |
| kubectl logs     | Check logs            |
| kubectl describe | Detailed info         |
| kubectl exec     | Enter pod             |
| kubectl apply    | Deploy YAML           |
| kubectl delete   | Remove resources      |
| kubectl scale    | Increase pods         |
| kubectl rollout  | Deployment management |
| kubectl get svc  | View services         |
| kubectl top      | Resource monitoring   |

---

## Common Kubernetes Issues and Troubleshooting

#### 1. Pod CrashLoopBackOff
```bash id="glt7lq"
# Check Logs
kubectl logs pod-name
```
#### 2. ImagePullBackOff
- Cause: Wrong Docker image name.

#### Solution
```bash id="6rfr2d"
kubectl describe pod pod-name
```
#### 3. Pod Pending
- Cause: No resources, Node issue
#### Solution
```bash id="t8lg4g"
kubectl describe pod pod-name
```
#### 4. Service Not Accessible
```bash id="h5r9mk"
# Check Service
kubectl get svc
```
#### 5. Node Not Ready
```bash id="0q98e9"
# Check Nodes
kubectl get nodes
```
## Kubernetes Resources

| Resource   | Purpose                |
| ---------- | ---------------------- |
| Pod        | Runs container         |
| Deployment | Manages pods           |
| Service    | Networking             |
| ConfigMap  | Store configs          |
| Secret     | Store sensitive data   |
| Namespace  | Environment separation |
| PV/PVC     | Storage                |
| Ingress    | External access        |

## Kubernetes Architecture Simple Flow

```text id="kn2x9m"
Developer Pushes Code
        ↓
CI/CD Pipeline
        ↓
Docker Image Build
        ↓
Push to Docker Registry
        ↓
Kubernetes Deployment
        ↓
Pods Created
        ↓
Service Exposes Application
        ↓
Users Access Application
```
