# Use Docker Images from Private Registry

## Login into the registry

On your laptop, you must authenticate with a registry in order to pull a private image:

```bash
docker login
```

When prompted, enter your Docker username and password.

The login process creates or updates a `config.json` file that holds an authorization token.

View the `config.json` file:

```bash
cat ~/.docker/config.json
```

The output contains a section similar to this:

```javascript
{
    "auths": {
        "https://index.docker.io/v1/": {
            "auth": "c3R...zE2"
        }
    }
}
```

## Create the secret

Create the base64 of the docker config.json file:

```bash
base64 ~/.docker/config.json > docker-registry-secret.yml
```

Now edit the docker-registry-secret.yml file like this:

```yaml
apiVersion: v1
kind: Secret
metadata:
  name: docker-registry
  namespace: default
data:
  .dockerconfigjson: PUT_THE_BASE64_HERE
type: kubernetes.io/dockerconfigjson
```

Now create the secret into kubernetes cluster:

```bash
kubectl apply -f docker-registry-secret.yml
```

## Create a Pod that uses your Secret

Now in your deployment.yml:

```yaml
apiVersion: v1
kind: Deployment
metadata:
  name: app
spec:
  containers:
  - name: app
    image: <your-private-image>
  imagePullSecrets:
  - name: docker-registry

```

