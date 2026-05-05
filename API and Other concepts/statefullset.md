# StatefulSet in Kubernetes

Kubernetes StatefulSet is a Kubernetes workload controller used to manage stateful applications.

Stateful applications are applications that require persistent storage, stable network identity, and ordered deployment behavior.

StatefulSet provides stable Pod names, persistent storage, and predictable Pod ordering.

StatefulSet is mainly used for databases, distributed systems, and applications requiring data persistence.

Examples are MySQL, PostgreSQL, MongoDB, Cassandra, Kafka, and Elasticsearch clusters.

## What is Stateful Application

Stateful Application stores data or session information persistently.

The application depends on stored state and identity for proper functioning.

If Pods restart, data and identity must remain consistent.

## Why StatefulSet is Used

StatefulSet provides stable Pod names.

StatefulSet provides persistent storage for each Pod.

StatefulSet ensures ordered Pod creation and deletion.

StatefulSet maintains stable network identity.

StatefulSet supports stateful distributed applications reliably.

## StatefulSet vs Deployment

Deployment is mainly used for stateless applications.

StatefulSet is mainly used for stateful applications.

Deployment Pods are interchangeable and randomly named.

StatefulSet Pods have stable unique identities.

Deployment does not guarantee Pod ordering.

StatefulSet guarantees ordered creation, scaling, and deletion.

Deployment usually uses shared storage or temporary storage.

StatefulSet provides dedicated persistent storage for each Pod.

## StatefulSet Features

### Stable Pod Names

Each Pod gets a fixed predictable name.

Example Pod names:

```text id="jlwm1a"
mysql-0
mysql-1
mysql-2
```

Pod names remain the same even after restart or rescheduling.

### Stable Network Identity

Each Pod gets a stable DNS hostname.

Pods communicate reliably using fixed identities.

Example DNS name:

```text id="’wini2b"
mysql-0.mysql.default.svc.cluster.local
```

### Persistent Storage

Each Pod gets its own Persistent Volume.

Data remains available even if Pods restart or move to another node.

### Ordered Deployment

Pods are created sequentially from lowest index to highest index.

Example order:

```text id="’wini3c"
mysql-0 -> mysql-1 -> mysql-2
```

### Ordered Termination

Pods are deleted in reverse order.

Example deletion order:

```text id="’wini4d"
mysql-2 -> mysql-1 -> mysql-0
```

## StatefulSet Architecture

StatefulSet works together with Pods, Headless Service, Persistent Volumes, and Persistent Volume Claims.

## Headless Service

StatefulSet commonly uses Headless Service for stable Pod DNS resolution.

Headless Service does not use ClusterIP.

Headless Service directly exposes Pod IP addresses.

Example Headless Service:

```yaml id="’wini5e"
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

`clusterIP: None` makes it a Headless Service.

## StatefulSet YAML Example

```yaml id="’wini6f"
apiVersion: apps/v1
kind: StatefulSet

metadata:
  name: mysql

spec:
  serviceName: "mysql"

  replicas: 3

  selector:
    matchLabels:
      app: mysql

  template:
    metadata:
      labels:
        app: mysql

    spec:
      containers:
      - name: mysql
        image: mysql:5.7

        ports:
        - containerPort: 3306

        volumeMounts:
        - name: mysql-storage
          mountPath: /var/lib/mysql

  volumeClaimTemplates:
  - metadata:
      name: mysql-storage

    spec:
      accessModes: [ "ReadWriteOnce" ]

      resources:
        requests:
          storage: 1Gi
```

## Important StatefulSet Fields

### serviceName

`serviceName` connects StatefulSet with Headless Service.

### replicas

Defines number of Pods.

### volumeClaimTemplates

Automatically creates Persistent Volume Claims for each Pod.

## StatefulSet Storage

Each StatefulSet Pod gets its own Persistent Volume Claim called PVC.

Example PVC names:

```text id="’wini7g"
mysql-storage-mysql-0
mysql-storage-mysql-1
mysql-storage-mysql-2
```

Each Pod stores data independently.

## StatefulSet Scaling

Scale StatefulSet:

```bash id="’wini8h"
kubectl scale statefulset mysql --replicas=5
```

New Pods are created sequentially.

## StatefulSet Commands

Create StatefulSet:

```bash id="’wini9i"
kubectl apply -f statefulset.yaml
```

View StatefulSets:

```bash id="’wini0j"
kubectl get statefulsets
```

Describe StatefulSet:

```bash id="’wini1k"
kubectl describe statefulset mysql
```

Delete StatefulSet:

```bash id="’wini2l"
kubectl delete statefulset mysql
```

## StatefulSet Rolling Updates

StatefulSet supports rolling updates carefully and sequentially.

Pods update one by one to maintain application stability.

Update order follows Pod sequence.

## Pod Management Policy

### OrderedReady

Pods start sequentially only after previous Pod becomes ready.

This is default behavior.

### Parallel

Pods start simultaneously without waiting for readiness sequence.

## StatefulSet Use Cases

Databases like MySQL and PostgreSQL.

Distributed messaging systems like Apache Kafka.

Search engines like Elasticsearch.

Monitoring systems requiring persistent storage.

Applications requiring stable Pod identities.

## Advantages of StatefulSet

Provides stable Pod identity.

Provides persistent storage for each Pod.

Supports ordered deployment and deletion.

Works well for stateful distributed applications.

Supports reliable service discovery.

## Limitations of StatefulSet

StatefulSet is more complex than Deployment.

Scaling and updates may be slower because of ordered operations.

Persistent storage management increases operational complexity.

Improper storage configuration may affect application stability.

## StatefulSet Workflow

User creates StatefulSet YAML.

Kubernetes creates Headless Service.

StatefulSet Controller creates Pods sequentially.

Each Pod gets stable name and dedicated storage.

Persistent Volume Claims are created automatically.

Pods maintain identity and storage during restarts.

Applications continue running reliably with persistent state management.
