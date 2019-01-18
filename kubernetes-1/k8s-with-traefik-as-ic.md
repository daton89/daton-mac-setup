# K8S with Traefik as IC

To set up Traefik, copy / paste the following command line:

```bash
helm install --name=traefik \
--set rbac.enabled=true,dashboard.enabled=true,dashboard.domain=dashboard.localhost stable/traefik
```

In the above command line, we enabled the dashboard \(_`dashboard.enabled=true`_\) and made it available on [http://dashboard.localhost](http://dashboard.localhost/) \(_`dashboard.domain=localhost.domain`_\).

The output of the helm install command line will look like:

![](../.gitbook/assets/screen-shot-2019-01-18-at-13.22.23.png)



To remove all helm charts: 

```bash
helm ls --short | xargs -L1 helm delete
```



