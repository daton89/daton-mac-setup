# Kubernetes

## Prerequisites

Use the Kubernetes command-line tool, [kubectl](https://kubernetes.io/docs/user-guide/kubectl/), to deploy and manage applications on Kubernetes. Using kubectl, you can inspect cluster resources; create, delete, and update components; look at your new cluster; and bring up apps.

{% embed url="https://kubernetes.io/docs/tasks/tools/install-kubectl/" %}

For development and practice you can use a Minikube cluster, but it only intended for testing without pay for a cluster in a provider. 

## Useful commands

### Deployments and status

Start deployment:

```bash
kubectl apply -f nginx-deployment.yaml
```

Check the status of a deployment:

```bash
kubectl rollout status deployments nginx-deployment
```

```bash
kubectl get deployments
```

```bash
kubectl describe deployments nginx-deployment
```

```bash
kubectl rollout history
```

### Clean up cluster

You might need to clean up it when you work with it.

Delete all pods:

```bash
kubectl delete pods --all
```

Delete all services:

```bash
kubectl delete services --all
```

Delete all deployments:

```bash
kubectl delete deployments --all
```

Delete all replicasets:

```bash
kubectl delete replicasets --all
```

Delete all:

```bash
kubectl delete daemonsets,replicasets,services,deployments,pods,rc --all
```

