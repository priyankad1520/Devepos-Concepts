# ArgoCD Full Concepts

Argo CD is a GitOps Continuous Delivery tool used to deploy and manage applications in Kubernetes clusters.

ArgoCD automatically synchronizes Kubernetes manifests from Git repositories to Kubernetes clusters.

ArgoCD follows the GitOps methodology, Git repository becomes the single source of truth for infrastructure and application deployment.

ArgoCD continuously monitors Git repositories and Kubernetes clusters, it ensures the cluster state matches the desired state defined in Git.

ArgoCD is mainly used in DevOps, Kubernetes environments, CI/CD pipelines, and cloud-native application deployments.

## What is GitOps

GitOps is a deployment methodology where Git repositories store Kubernetes configurations and infrastructure definitions.

GitOps uses Git as the central place for version control, change tracking, and deployment management.

Any changes pushed to Git are automatically applied to Kubernetes clusters using tools like Argo CD.

GitOps improves automation, consistency, rollback capability, auditing, and deployment reliability.

## Why ArgoCD is Used

ArgoCD automates Kubernetes deployments directly from Git repositories.

ArgoCD reduces manual deployment work and configuration drift.

ArgoCD provides visibility into application deployment status and synchronization state.

ArgoCD supports automatic rollback and self-healing features.

ArgoCD improves deployment consistency across environments.

ArgoCD integrates easily with CI/CD pipelines and Kubernetes clusters.

## ArgoCD Architecture

ArgoCD Architecture contains multiple components working together for GitOps deployment management.

Main components are API Server, Repository Server, Application Controller, Redis, Dex, and UI/CLI.

### API Server

ArgoCD API Server exposes REST API, Web UI, and CLI interfaces.

The API Server handles authentication, authorization, and communication between components.

Users interact with ArgoCD through UI, CLI, or API Server.

### Repository Server

Repository Server connects to Git repositories and stores Kubernetes manifests information.

The Repository Server generates Kubernetes manifests from Helm Charts, Kustomize, YAML files, or Jsonnet templates.

### Application Controller

Application Controller continuously monitors application states.

The controller compares desired state from Git with live state in Kubernetes clusters.

If differences are detected, the controller synchronizes the cluster automatically or manually.

### Redis

Redis stores temporary cache data for faster performance.

Redis improves ArgoCD response speed and state management.

### Dex

Dex provides authentication integration for ArgoCD.

Dex supports SSO integration with GitHub, Google, LDAP, and other identity providers.

### UI and CLI

ArgoCD provides a web-based UI for monitoring deployments visually.

ArgoCD CLI allows managing applications and deployments through terminal commands.

## How ArgoCD Works

Developer pushes Kubernetes manifest files to a Git repository.

ArgoCD monitors the Git repository continuously.

ArgoCD detects changes in Git repository manifests.

ArgoCD compares desired state in Git with current state in Kubernetes cluster.

If differences exist, ArgoCD synchronizes the cluster with Git definitions.

Applications are deployed or updated automatically inside Kubernetes clusters.

ArgoCD continuously monitors for configuration drift and corrects mismatched states.

## ArgoCD Installation

ArgoCD is commonly installed inside Kubernetes clusters.

Create namespace:

```bash id="sk5q4h"
kubectl create namespace argocd
```

Install ArgoCD:

```bash id="5v1y86"
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
```

Check running pods:

```bash id="t9vwsd"
kubectl get pods -n argocd
```

Expose ArgoCD Server:

```bash id="vq8sra"
kubectl port-forward svc/argocd-server -n argocd 8080:443
```

## ArgoCD Login

Get admin password:

```bash id="mlvjl8"
kubectl get secret argocd-initial-admin-secret -n argocd -o yaml
```

Decode password:

```bash id="0mwxhf"
echo password | base64 --decode
```

Login using CLI:

```bash id="d4ukmd"
argocd login localhost:8080
```

## ArgoCD Application

Application is the main deployment object in ArgoCD.

An application connects Git repository manifests to a Kubernetes cluster and namespace.

Applications define source repository, target cluster, namespace, and synchronization settings.

Create application using CLI:

```bash id="4k5yqg"
argocd app create myapp \
--repo https://github.com/user/repo.git \
--path manifests \
--dest-server https://kubernetes.default.svc \
--dest-namespace default
```

Sync application manually:

```bash id="o8eq3q"
argocd app sync myapp
```

Check application status:

```bash id="if1eb9"
argocd app get myapp
```

Delete application:

```bash id="rk61za"
argocd app delete myapp
```

## Synchronization in ArgoCD

Synchronization means applying Git repository changes to Kubernetes clusters.

Manual Sync requires users to trigger deployments manually.

Automatic Sync automatically deploys changes whenever Git repository updates occur.

Enable auto-sync:

```bash id="a7s3n0"
argocd app set myapp --sync-policy automated
```

## Self-Healing

Self-healing automatically restores Kubernetes resources if someone manually changes cluster configurations.

ArgoCD detects configuration drift and re-applies correct configurations from Git.

## Pruning

Pruning removes Kubernetes resources deleted from Git repositories.

Without pruning, deleted Git resources may still remain inside Kubernetes clusters.

Enable pruning:

```bash id="vl0pmx"
argocd app set myapp --auto-prune
```

## Health Status

ArgoCD monitors application health continuously.

Healthy means resources are running correctly.

Progressing means deployment is in progress.

Degraded means resources have failures or unhealthy states.

Missing means resources are not found in the cluster.

## Supported Deployment Methods

ArgoCD supports plain YAML manifests.

ArgoCD supports Helm Charts.

ArgoCD supports Kustomize configurations.

ArgoCD supports Jsonnet templates.

## Helm with ArgoCD

Helm Charts can be deployed directly using ArgoCD.

ArgoCD automatically renders Helm templates before deployment.

Example Helm application:

```bash id="0imrja"
argocd app create nginx-app \
--repo https://github.com/user/helm-repo.git \
--path nginx-chart \
--dest-server https://kubernetes.default.svc \
--dest-namespace default
```

## Multi-Cluster Management

ArgoCD supports multiple Kubernetes clusters.

One ArgoCD instance can manage applications across multiple clusters.

Add cluster:

```bash id="ofmt6m"
argocd cluster add mycluster
```

List clusters:

```bash id="sll8bx"
argocd cluster list
```

## ArgoCD Security

ArgoCD supports RBAC called Role-Based Access Control.

RBAC controls user permissions for applications and clusters.

ArgoCD supports SSO authentication integration.

TLS encryption secures ArgoCD communication.

Git repositories should use secure authentication methods like SSH keys or tokens.

## ArgoCD Notifications

ArgoCD supports notifications for deployment events.

Notifications can be sent through Slack, Email, Microsoft Teams, and Webhooks.

## ArgoCD CLI Commands

List applications:

```bash id="3y4nxy"
argocd app list
```

List clusters:

```bash id="rj7t0z"
argocd cluster list
```

List repositories:

```bash id="4yzg0r"
argocd repo list
```

Refresh application state:

```bash id="5v98p4"
argocd app refresh myapp
```

Rollback application:

```bash id="2z1i1d"
argocd app rollback myapp
```

## ArgoCD Advantages

ArgoCD provides automated Kubernetes deployments.

ArgoCD improves deployment consistency using GitOps.

ArgoCD supports rollback and version control through Git.

ArgoCD provides self-healing and drift detection.

ArgoCD improves deployment visibility using UI dashboards.

ArgoCD supports multi-cluster management.

ArgoCD integrates with Helm and Kustomize easily.

## ArgoCD Limitations

ArgoCD mainly focuses on Kubernetes environments.

Complex Git repository structures may become difficult to manage.

Large-scale deployments may require proper performance tuning.

Improper Git access management may create security risks.

## ArgoCD Workflow

Developer updates Kubernetes manifests in Git repository.

Git stores configuration changes with version control.

ArgoCD monitors the repository continuously.

ArgoCD detects repository changes automatically.

ArgoCD compares desired state with live cluster state.

ArgoCD synchronizes Kubernetes resources with Git configurations.

Applications are deployed or updated inside Kubernetes clusters.

ArgoCD continuously monitors cluster state for drift and health status.
