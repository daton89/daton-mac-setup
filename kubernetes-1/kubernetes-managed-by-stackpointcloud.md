# Kubernetes managed by StackPointCloud



Assuming you have Homebrew installed and configured on your Mac, run the following command to install Helm:

```text
brew install kubernetes-helm
```

```text
Output==> Downloading https://homebrew.bintray.com/bottles/kubernetes-helm-2.8.2.high_sierra.bottle.tar.gz
...
==> Summary
🍺  /usr/local/Cellar/kubernetes-helm/2.8.2: 50 files, 121.7MB
```

Once Helm is installed, verify that you can run it by checking its current version.

```text
helm version
```

```text
OutputClient: &version.Version{SemVer:"v2.7.2", GitCommit:"8478fb4fc723885b155c924d1c8c410b7a9444e6", GitTreeState:"clean"}
Server: &version.Version{SemVer:"v2.8.2", GitCommit:"a80231648a1473929271764b920a8e346f6de844", GitTreeState:"clean"}
```

This confirms that the client is installed properly and is able to talk to Tiller.

In the next step, we will use Helm to deploy the MongoDB ReplicaSet in Kubernetes.

