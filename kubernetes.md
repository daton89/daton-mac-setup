# Kubernetes

## **Install kubectl, the official Kubernetes command-line tool**

You won’t be able to connect just yet, but that shouldn’t stop you from getting your local machine or remote management server set up to manage your cluster. In either case, the management machine will need:

1. kubectl, the official Kubernetes command-line tool, which you’ll use to connect to the cluster
2. The cluster configuration file, which contains authentication certificates

The Kubernetes project provides detailed directions for installation on a variety of platforms. Use `kubectl version` to make sure that your install is working and within one minor version of your cluster.

### Install with Homebrew on macOS <a id="install-with-homebrew-on-macos"></a>

If you are on macOS and using [Homebrew](https://brew.sh/) package manager, you can install kubectl with Homebrew.

1. Run the installation command:

   ```text
   brew install kubernetes-cli
   ```

2. Test to ensure the version you installed is sufficiently up-to-date:

   ```text
   kubectl version
   ```

### **Connect to your cluster**

Once you’ve installed kubectl, next download its config file with the button below. You can place the config file anywhere on the machine where you run `kubectl` and invoke it with the `--kubeconfig` option. By convention, Kubernetes config files are stored in hidden folder in your home directory named `.kube`

### **Test the connection**

To test that the file authenticates successfully, you can use the following command from within the .kube directory:

```text
kubectl --kubeconfig="cluster1-kubeconfig-dupe.yaml" get nodes
```

If you are using kubectl from elsewhere on the filesystem, supply the full path to the config file.

### **Command success**

When the command is successful, it should return information similar to the following, although the details will vary depending on the specific cluster configuration:

```text
NAME          STATUS    ROLES     AGE       VERSION
worker-9511   Ready     <none>    3d        v1.10.7
worker-9512   Ready     <none>    3d        v1.10.7
worker-9513   Ready     <none>    3d        v1.10.7
```

Once kubectl and the cluster configuration file are in place, you can create, manage, and deploy clusters. From here, you can add [DigitalOcean Load Balancers](https://cloud.digitalocean.com/networking/load_balancers?i=28b6d9) and [block storage volumes](https://cloud.digitalocean.com/volumes?i=28b6d9) to your cluster.

## **Deploy a Workload to your cluster**

In Kubernetes there’s various types of workloads you can deploy. Below you can find 4 different example manifests that can be deployed to your cluster. Copy the example manifest to a file on your workstation and use kubectl to apply it.

```text
kubectl create -f ./my-manifest.yaml
```

CopyCopy

### **Create a Deployment**

Deployments describe a set of identical Pods without unique identities. A Deployment will run multiple replicas of your application and will automatically replace instances that fail or become unresponsive.

```text
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deployment-example
spec:
  replicas: 1
  selector:
    matchLabels:
      app: nginx-deployment-example
  template:
    metadata:
      labels:
        app: nginx-deployment-example
    spec:
      containers:
        - name: nginx
          image: library/nginx
```

CopyCopy

### **Create a CronJob**

A Cron Job creates Jobs on a time-based schedule. One CronJob object is like one line of a crontab \(cron table\) file. It runs a job periodically on a given schedule, written in Cron format.

```text
apiVersion: batch/v1beta1
kind: CronJob
metadata:
  name: cronjob-example
spec:
  schedule: '*/5 * * * *'
  jobTemplate:
    spec:
      template:
        spec:
          containers:
            - name: cronjob-example
              image: busybox
              args:
                - /bin/sh
                - '-c'
                - echo This is an example cronjob running every five minutes
          restartPolicy: OnFailure
```

CopyCopy

### **Create a Pod**

A Pod is the basic building block of Kubernetes–the smallest and simplest unit in the Kubernetes object model that you create or deploy. A Pod represents a running process on your cluster.

```text
apiVersion: v1
kind: Pod
metadata:
  name: nginx-pod-example
spec:
  containers:
    - name: nginx-pod-example
      image: library/nginx
```

CopyCopy

### **Create a ReplicaSet**

A ReplicaSet ensures that a specified number of pod replicas are running at any given time. You can specify how many replicas of the pod that should be running by editing the 'replicas' key in the example below:

```text
apiVersion: apps/v1
kind: ReplicaSet
metadata:
  name: nginx-replicaset-example
spec:
  replicas: 1
  selector:
    matchLabels:
      app: nginx-replicaset-example
  template:
    metadata:
      labels:
        app: nginx-replicaset-example
    spec:
      containers:
        - name: nginx-replicaset-example
          image: library/nginx
```

## **Add resources** 

### **Add Block Storage Volumes to your cluster**

When you need to write and access persistent data in a Kubernetes cluster, you can create and access DigitalOcean block storage volumes by creating a PersistentVolumeClaim as part of your deployment.

The claim can allow cluster workers to read and write database records, user-generated website content, log files, and other data that should persist after a process has completed.

### **Create a Configuration File**

The example configuration defines two types of objects:

1. The `PersistentVolumeClaim` called `csi-pvc` which is responsible for locating the block storage volume by name if it already exists and creating the volume if it does not.
2. The Pod named `my-csi-app`, which will create containers, then add a mountpoint to the first object and mount the volume there.

Continue on to define the [Persistent Volume Claim](https://www.digitalocean.com/docs/kubernetes/how-to/add-persistent-storage/).

### **Add a Load Balancer to your cluster**

The DigitalOcean Cloud Controller supports provisioning DigitalOcean Load Balancers in a cluster’s resource configuration file.

The example configuration will define a load balancer and create it if one with the same name does not already exist.

### **Create a Configuration File**

You can add an external load balancer to a cluster by creating a new configuration file or adding the following lines to your existing service config file. Note that both the type and ports values are required for type: LoadBalancer:

```text
spec:
  type: LoadBalancer
  ports:
    - port: 80
      targetPort: 3000
      name: http
```

CopyCopy

Continue on to see [how this might look like in the context of a service file](https://www.digitalocean.com/docs/kubernetes/how-to/add-load-balancer/).

