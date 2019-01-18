# Kubernetes

Use the Kubernetes command-line tool, [kubectl](https://kubernetes.io/docs/user-guide/kubectl/), to deploy and manage applications on Kubernetes. Using kubectl, you can inspect cluster resources; create, delete, and update components; look at your new cluster; and bring up example apps.

{% embed url="https://kubernetes.io/docs/tasks/tools/install-kubectl/" %}

### Install Helm

We can install Helm with _brew_ just running in a terminal: 

```bash
brew install kubernetes-helm
```

Then we need to initialise it:

```bash
helm init
```

### Useful commands

The purpose of Minikube is testing without pay for a cluster in a provider. 

So you might need to clean up it when you work with it.

```bash
# Delete all pods
kubectl delete pods --all

# Delete all services 
kubectl delete services --all

# Delete all deployments
kubectl delete deployments --all

# Delete all replicasets
kubectl delete replicasets --all

# Delete all
kubectl delete daemonsets,replicasets,services,deployments,pods,rc --all

```

