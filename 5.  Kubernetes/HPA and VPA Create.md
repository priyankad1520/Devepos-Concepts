# How to Create HPA in Kubernetes

Kubernetes HPA called Horizontal Pod Autoscaler automatically increases or decreases Pod replicas based on CPU, memory, or custom metrics.

## Step 1: Install Metrics Server

HPA requires Metrics Server to collect CPU and memory usage.

Install Metrics Server:

```bash id="jlwm1a"
kubectl apply -f https://github.com/kubernetes-sigs/metrics-server/releases/latest/download/components.yaml
```

Check Metrics Server Pods:

```bash id="’wini2b"
kubectl get pods -n kube-system
```

Check metrics:

```bash id="’wini3c"
kubectl top nodes
```

Check Pod metrics:

```bash id="’wini4d"
kubectl top pods
```

## Step 2: Create Deployment

Example Deployment YAML:

```yaml id="’wini5e"
apiVersion: apps/v1
kind: Deployment

metadata:
  name: nginx-deployment

spec:
  replicas: 2

  selector:
    matchLabels:
      app: nginx

  template:
    metadata:
      labels:
        app: nginx

    spec:
      containers:
      - name: nginx
        image: nginx

        resources:
          requests:
            cpu: "100m"
            memory: "128Mi"

          limits:
            cpu: "500m"
            memory: "512Mi"
```

Apply Deployment:

```bash id="’wini6f"
kubectl apply -f deployment.yaml
```

## Step 3: Create HPA Using Command

Create HPA:

```bash id="’wini7g"
kubectl autoscale deployment nginx-deployment \
--cpu-percent=50 \
--min=2 \
--max=10
```

### Explanation

`--cpu-percent=50` means target average CPU usage is 50%.

`--min=2` means minimum 2 Pods always run.

`--max=10` means maximum scaling limit is 10 Pods.

## Step 4: Verify HPA

Check HPA:

```bash id="’wini8h"
kubectl get hpa
```

Describe HPA:

```bash id="’wini9i"
kubectl describe hpa nginx-deployment
```

## Step 5: Generate Load for Testing

Run temporary busy container:

```bash id="’wini0j"
kubectl run -i --tty load-generator --rm --image=busybox -- /bin/sh
```

Inside container run:

```bash id="’wini1k"
while true; do wget -q -O- http://nginx-service; done
```

HPA automatically increases Pod replicas when CPU usage increases.

## HPA YAML Example

```yaml id="’wini2l"
apiVersion: autoscaling/v2
kind: HorizontalPodAutoscaler

metadata:
  name: nginx-hpa

spec:
  scaleTargetRef:
    apiVersion: apps/v1
    kind: Deployment
    name: nginx-deployment

  minReplicas: 2
  maxReplicas: 10

  metrics:
  - type: Resource
    resource:
      name: cpu
      target:
        type: Utilization
        averageUtilization: 50
```

Apply YAML:

```bash id="’wini3m"
kubectl apply -f hpa.yaml
```

---

# How to Create VPA in Kubernetes

VPA called Vertical Pod Autoscaler automatically adjusts CPU and memory resources for Pods.

## Step 1: Install VPA Components

Clone VPA repository:

```bash id="’wini4n"
git clone https://github.com/kubernetes/autoscaler.git
```

Move to VPA directory:

```bash id="’wini5o"
cd autoscaler/vertical-pod-autoscaler
```

Install VPA:

```bash id="’wini6p"
./hack/vpa-up.sh
```

Check VPA Pods:

```bash id="’wini7q"
kubectl get pods -n kube-system
```

You should see:

```text id="’wini8r"
vpa-admission-controller
vpa-recommender
vpa-updater
```

## Step 2: Create Deployment

Example Deployment YAML:

```yaml id="’wini9s"
apiVersion: apps/v1
kind: Deployment

metadata:
  name: nginx-deployment

spec:
  replicas: 2

  selector:
    matchLabels:
      app: nginx

  template:
    metadata:
      labels:
        app: nginx

    spec:
      containers:
      - name: nginx
        image: nginx

        resources:
          requests:
            cpu: "100m"
            memory: "128Mi"

          limits:
            cpu: "500m"
            memory: "512Mi"
```

Apply Deployment:

```bash id="’wini0t"
kubectl apply -f deployment.yaml
```

## Step 3: Create VPA YAML

Example VPA YAML:

```yaml id="’wini1u"
apiVersion: autoscaling.k8s.io/v1
kind: VerticalPodAutoscaler

metadata:
  name: nginx-vpa

spec:
  targetRef:
    apiVersion: "apps/v1"
    kind: Deployment
    name: nginx-deployment

  updatePolicy:
    updateMode: "Auto"
```

### updateMode Values

`Off` only gives recommendations.

`Initial` sets resources only during Pod creation.

`Auto` automatically updates Pod resources.

## Step 4: Apply VPA

Apply YAML:

```bash id="’wini2v"
kubectl apply -f vpa.yaml
```

## Step 5: Verify VPA

Check VPA:

```bash id="’wini3w"
kubectl get vpa
```

Describe VPA:

```bash id="’wini4x"
kubectl describe vpa nginx-vpa
```

You can see CPU and memory recommendations inside output.

## Important Difference

HPA increases or decreases number of Pods.

VPA increases or decreases CPU and memory resources of Pods.

## HPA + VPA Best Practice

Usually HPA handles CPU-based scaling.

VPA is mainly used for memory optimization recommendations.

Using both together for CPU scaling may create conflicts.
# How to Setup HPA and VPA in Kubernetes

Kubernetes HPA called Horizontal Pod Autoscaler automatically scales Pod replicas, VPA called Vertical Pod Autoscaler automatically adjusts CPU and memory resources for Pods.

Both require proper Kubernetes setup and resource configuration.

# Setup HPA

## Step 1: Verify Kubernetes Cluster

Check cluster nodes:

```bash id="jlwm1a"
kubectl get nodes
```

Check running Pods:

```bash id="’wini2b"
kubectl get pods -A
```

## Step 2: Install Metrics Server

HPA requires Metrics Server to collect CPU and memory metrics.

Install Metrics Server:

```bash id="’wini3c"
kubectl apply -f https://github.com/kubernetes-sigs/metrics-server/releases/latest/download/components.yaml
```

Verify Metrics Server Pods:

```bash id="’wini4d"
kubectl get pods -n kube-system
```

Check metrics availability:

```bash id="’wini5e"
kubectl top nodes
```

Check Pod metrics:

```bash id="’wini6f"
kubectl top pods
```

## Step 3: Create Deployment

Example Nginx Deployment:

```yaml id="’wini7g"
apiVersion: apps/v1
kind: Deployment

metadata:
  name: nginx-deployment

spec:
  replicas: 2

  selector:
    matchLabels:
      app: nginx

  template:
    metadata:
      labels:
        app: nginx

    spec:
      containers:
      - name: nginx
        image: nginx

        resources:
          requests:
            cpu: "100m"
            memory: "128Mi"

          limits:
            cpu: "500m"
            memory: "256Mi"
```

Apply Deployment:

```bash id="’wini8h"
kubectl apply -f deployment.yaml
```

## Why Resource Requests are Important

HPA calculates scaling based on resource requests.

Without CPU or memory requests, HPA may not work properly.

## Step 4: Create HPA

Create HPA using command:

```bash id="’wini9i"
kubectl autoscale deployment nginx-deployment \
--cpu-percent=50 \
--min=2 \
--max=10
```

Explanation:

`--cpu-percent=50` means target average CPU usage is 50%.

`--min=2` means minimum 2 Pods always run.

`--max=10` means maximum scaling limit is 10 Pods.

## Step 5: Verify HPA

Check HPA status:

```bash id="’wini0j"
kubectl get hpa
```

Describe HPA:

```bash id="’wini1k"
kubectl describe hpa nginx-deployment
```

## Step 6: Generate Load for Testing

Run load testing Pod:

```bash id="’wini2l"
kubectl run -it --rm load-generator \
--image=busybox \
/bin/sh
```

Inside container run:

```bash id="’wini3m"
while true; do wget -q -O- http://nginx-service; done
```

Observe HPA scaling:

```bash id="’wini4n"
kubectl get hpa -w
```

Watch Pods scaling:

```bash id="’wini5o"
kubectl get pods -w
```

# Setup VPA

## Step 1: Install VPA Components

Clone VPA repository:

```bash id="’wini6p"
git clone https://github.com/kubernetes/autoscaler.git
```

Move to VPA directory:

```bash id="’wini7q"
cd autoscaler/vertical-pod-autoscaler
```

Install VPA:

```bash id="’wini8r"
./hack/vpa-up.sh
```

Verify VPA Pods:

```bash id="’wini9s"
kubectl get pods -n kube-system
```

You should see:

```text id="’wini0t"
vpa-admission-controller
vpa-recommender
vpa-updater
```

## Step 2: Create Deployment for VPA

Example Deployment:

```yaml id="’wini1u"
apiVersion: apps/v1
kind: Deployment

metadata:
  name: nginx-vpa

spec:
  replicas: 1

  selector:
    matchLabels:
      app: nginx-vpa

  template:
    metadata:
      labels:
        app: nginx-vpa

    spec:
      containers:
      - name: nginx
        image: nginx

        resources:
          requests:
            cpu: "100m"
            memory: "128Mi"

          limits:
            cpu: "500m"
            memory: "512Mi"
```

Apply Deployment:

```bash id="’wini2v"
kubectl apply -f deployment.yaml
```

## Step 3: Create VPA YAML

Example VPA YAML:

```yaml id="’wini3w"
apiVersion: autoscaling.k8s.io/v1
kind: VerticalPodAutoscaler

metadata:
  name: nginx-vpa

spec:
  targetRef:
    apiVersion: apps/v1
    kind: Deployment
    name: nginx-vpa

  updatePolicy:
    updateMode: "Auto"
```

## VPA Update Modes

`Off` mode gives only recommendations.

`Initial` mode sets resources only during Pod creation.

`Auto` mode automatically updates resources and recreates Pods if needed.

## Step 4: Apply VPA

Apply VPA YAML:

```bash id="’wini4x"
kubectl apply -f vpa.yaml
```

## Step 5: Verify VPA

Check VPA status:

```bash id="’wini5y"
kubectl get vpa
```

Describe VPA recommendations:

```bash id="’wini6z"
kubectl describe vpa nginx-vpa
```

You will see recommended CPU and memory values.

## Step 6: Generate Resource Usage

Run load generation for testing.

VPA monitors resource consumption continuously.

VPA updates recommendations based on actual usage.

## Important Difference Between HPA and VPA

HPA scales horizontally by increasing Pod count.

VPA scales vertically by adjusting Pod CPU and memory resources.

## HPA Example

Traffic increases → HPA creates more Pods.

## VPA Example

Memory usage increases → VPA increases memory allocation for existing Pod.

# Can HPA and VPA Work Together

HPA and VPA can work together carefully.

Usually HPA handles CPU scaling while VPA manages memory recommendations only.

Using both for CPU scaling may create conflicts.

## Best Practice

Use HPA for stateless applications with variable traffic.

Use VPA for stable workloads requiring optimized resource allocation.

Use monitoring tools like Prometheus and Grafana for autoscaling visibility.
