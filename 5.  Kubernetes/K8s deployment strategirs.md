Deployment strategies are different ways of releasing a new version of an application to users while reducing downtime, failures, and risk in production environments.

Recreate deployment means the old version of the application is completely stopped and then the new version is started, which is simple but causes downtime.

Rolling deployment means the new version is released gradually by replacing old application instances one by one, which reduces downtime and allows smooth updates.

Blue-Green deployment means two identical environments are maintained where one environment runs the current version and the other runs the new version, and traffic is switched to the new environment after testing.

Canary deployment means the new version is released only to a small group of users first, and if everything works correctly, it is gradually released to all users.

A/B deployment means different versions of the application are shown to different groups of users to compare performance, features, or user behavior.

Shadow deployment means the new version runs in parallel with the old version and receives real user traffic for testing without affecting actual users.

Feature flag deployment means new features are hidden behind configuration switches so developers can enable or disable features without redeploying the application.

Immutable deployment means instead of updating existing servers, completely new servers or containers with the new version are created and the old ones are removed.

Progressive deployment means the application update is released step by step to users or servers while continuously monitoring performance and stability.

Ramped deployment means the new version is slowly increased across servers over time until all traffic moves to the new release.

Hotfix deployment means a small urgent update is directly released to production to quickly fix critical bugs or security issues.
Rolling Deployment is a deployment strategy where the new version of an application is updated gradually, one server or pod at a time, instead of stopping the entire application at once.

In this method, some users continue using the old version while other users start using the new version during the update process. This helps avoid downtime and keeps the application available continuously.

For example, suppose an application is running with 4 pods in Kubernetes.

Initially:
Pod 1 → Version 1
Pod 2 → Version 1
Pod 3 → Version 1
Pod 4 → Version 1

During rolling deployment:
Step 1 → Replace Pod 1 with Version 2
Step 2 → Replace Pod 2 with Version 2
Step 3 → Replace Pod 3 with Version 2
Step 4 → Replace Pod 4 with Version 2

Finally:
Pod 1 → Version 2
Pod 2 → Version 2
Pod 3 → Version 2
Pod 4 → Version 2

In rolling deployment, the application does not completely stop because only a few pods are updated at a time.

Advantages of rolling deployment are reduced downtime, smooth updates, better user experience, and easier rollback if an issue happens.

The disadvantage is that old and new versions run together for some time, so compatibility issues may happen if both versions behave differently.

In Kubernetes, rolling deployment is mainly handled by a Deployment object using commands like:

```bash
kubectl apply -f deployment.yaml
```

To check rollout status:

```bash
kubectl rollout status deployment <deployment-name>
```

To see rollout history:

```bash
kubectl rollout history deployment <deployment-name>
```

To rollback:

```bash
kubectl rollout undo deployment <deployment-name>
```
Blue-Green deployment is a deployment strategy used to release a new version of an application with minimum downtime and lower risk.

In this strategy, two identical environments are maintained called Blue environment and Green environment.

The Blue environment contains the current live application version that users are already using.

The Green environment contains the new application version that developers want to release.

At the beginning, all user traffic goes to the Blue environment because it is the active production environment.

The new application version is deployed and tested in the Green environment without affecting real users.

After testing is successful, the traffic is switched from Blue to Green using a load balancer, DNS change, or reverse proxy.

Once the traffic moves to Green, users start using the new application version.

If any issue or bug is found in the new version, the traffic can quickly switch back to the Blue environment, which makes rollback very fast and safe.

Blue-Green deployment is mainly used to avoid downtime, reduce deployment risk, and provide quick rollback during production releases.

Example:
Suppose an e-commerce website version v1 is running in the Blue environment.

Developers create version v2 and deploy it in the Green environment.

After testing v2 successfully, the load balancer redirects all user traffic from Blue to Green.

Now users access version v2 without downtime.

If version v2 fails, traffic is immediately switched back to Blue where version v1 is still available.

Advantages of Blue-Green deployment are zero downtime deployment, easy rollback, safer production release, and better testing before release.

Disadvantages of Blue-Green deployment are higher infrastructure cost because two environments are required and database synchronization can become complex.

In Kubernetes, Blue-Green deployment is usually implemented using separate deployments and services where the service changes traffic from the old pods to the new pods.
In Blue-Green deployment, we maintain two separate environments called Blue and Green.

The Blue environment contains the current live application version running in production.

The Green environment contains the new application version that we want to release.

First, users access the application through the Blue environment.

Then developers build a new application version and deploy it into the Green environment without disturbing users.

After deployment, the Green environment is tested properly using health checks, testing tools, or internal users.

Once testing is successful, traffic is switched from Blue to Green using a Load Balancer, Kubernetes Service, Ingress, or DNS.

After switching, all users start accessing the new application running in Green.

If the new version works correctly, the old Blue environment can be removed or kept as backup.

If any issue occurs in Green, traffic is immediately switched back to Blue for fast rollback.

Example in Kubernetes:

Suppose:
Blue deployment = app-v1
Green deployment = app-v2

First deploy Version 1:

```bash
kubectl apply -f blue-deployment.yaml
```

Deploy Version 2 in Green:

```bash
kubectl apply -f green-deployment.yaml
```

Service initially points to Blue pods:

```yaml
selector:
  version: blue
```

After testing Green, change Service selector:

```yaml
selector:
  version: green
```

Apply the updated service:

```bash
kubectl apply -f service.yaml
```

Now all traffic moves from Blue pods to Green pods.

Architecture Flow:

```text
Users
   ↓
Load Balancer / Service
   ↓
Blue Environment (Old Version)

After Switch

Users
   ↓
Load Balancer / Service
   ↓
Green Environment (New Version)
```

Real-time deployment process:
Developer → Build Docker Image → Push to Registry → Deploy Green Environment → Test → Switch Traffic → Monitor → Remove Blue if successful.
Canary deployment is a deployment strategy where a new version of an application is released to a small number of users or servers first instead of releasing it to everyone at once. If the new version works properly without errors, crashes, or performance issues, the deployment is gradually expanded to all users. This strategy helps reduce production risk because only a small percentage of users are affected if something goes wrong.

The word “Canary” comes from old coal mines where miners used canary birds to detect dangerous gases. If the bird was affected, miners knew there was danger. Similarly, in Canary deployment, a small group of users tests the new version before giving it to everyone.

In Canary deployment, both old and new versions run together at the same time. Traffic is split between them. For example, 90% of users may use version V1 and 10% may use version V2. After monitoring logs, CPU, memory, response time, and errors, traffic is slowly increased to the new version.

Example of Canary deployment flow:
Version V1 is running for all users → Deploy Version V2 to one server or pod → Send small traffic to V2 → Monitor application health → Increase traffic gradually → Remove old V1 after successful testing.

In Kubernetes, Canary deployment is commonly done using Deployments, Services, Ingress Controllers, or service mesh tools like Istio.

Simple Kubernetes Canary Deployment process:

Step 1: Deploy old application version.

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: myapp-v1
spec:
  replicas: 4
  selector:
    matchLabels:
      app: myapp
      version: v1
  template:
    metadata:
      labels:
        app: myapp
        version: v1
    spec:
      containers:
      - name: myapp
        image: myapp:v1
```

This runs Version 1 for users.

Step 2: Deploy new Canary version with fewer replicas.

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: myapp-v2
spec:
  replicas: 1
  selector:
    matchLabels:
      app: myapp
      version: v2
  template:
    metadata:
      labels:
        app: myapp
        version: v2
    spec:
      containers:
      - name: myapp
        image: myapp:v2
```

Here, only one pod runs the new version.

Step 3: Create a common Service.

```yaml
apiVersion: v1
kind: Service
metadata:
  name: myapp-service
spec:
  selector:
    app: myapp
  ports:
  - port: 80
    targetPort: 8080
```

The Service sends traffic to both V1 and V2 pods because both have the label `app: myapp`.

Traffic example:
4 V1 pods + 1 V2 pod means around 20% traffic goes to V2 automatically.

Step 4: Monitor the Canary version.

Check:
`kubectl get pods`
`kubectl logs pod-name`
`kubectl top pods`
`kubectl describe pod pod-name`

Monitor:
Error rate, CPU usage, memory usage, crashes, response time, and user feedback.

Step 5: Increase traffic gradually.

Increase V2 replicas:

```bash
kubectl scale deployment myapp-v2 --replicas=3
```

Decrease V1 replicas:

```bash
kubectl scale deployment myapp-v1 --replicas=2
```

Eventually move all traffic to V2.

Step 6: Remove old version.

```bash
kubectl delete deployment myapp-v1
```

Advantages of Canary deployment:
Less production risk, safer releases, easier rollback, real-user testing, minimal downtime, and better monitoring.

Disadvantages of Canary deployment:
More complex setup, requires monitoring tools, traffic management can be difficult, and both versions must run together which uses more resources.

Rollback in Canary deployment is simple because the old version is still running. If V2 fails, reduce V2 replicas to zero and send all traffic back to V1.

```bash
kubectl scale deployment myapp-v2 --replicas=0
```

Real-world tools used for Canary deployment:
Kubernetes, Argo Rollouts, Istio, NGINX, and Amazon Web Services load balancers.

Example real-world concept:
Imagine updating employees in a company shift by shift instead of replacing all employees at the same time. Work continues without interruption while new employees gradually take over.
