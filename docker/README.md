# Docker

## Installing Docker

brew cask install docker

## Installing Kitematic

You can install `Kitematic`  from your terminal running:  `brew cask install kitematic`

## Create a Private Docker Registry

### Installing Package for Added Security <a id="step-1-&#x2014;-installing-package-for-added-security"></a>

We'll install the `apache2-utils` package which contains the `htpasswd` utility that can easily generate password hashes Nginx can understand:

```bash
sudo apt-get -y install apache2-utils
```

### Installing and Configuring the Docker Registry <a id="step-2-&#x2014;-installing-and-configuring-the-docker-registry"></a>

Docker Compose allows you to write one `.yml` configuration file for the configuration for each container 

First create a folder where our files for this tutorial will live and some of the subfolders we'll need:

```bash
mkidr ~/docker-registry && cd $_
mkdir data
```

Using your favorite text editor, create a `docker-compose.yml` file:

```bash
nano docker-compose.yml
```

Add the following contents to the file:

```text
version: '2'

services:

  registry:
    hostname: registry
    restart: unless-stopped
    image: registry:2
    ports:
      - 127.0.0.1:5000:5000
    environment:    
      REGISTRY_STORAGE_FILESYSTEM_ROOTDIRECTORY: /data
    volumes:
      - ./data:/data
    networks:
      - registry_platform

networks:
  traefik_proxy:
    external: true
  registry_platform:
    external: false
    driver: bridge
```

Docker registry's data all gets stored in `~/docker-registry/data` on our local machine.

### Setting Up an Nginx Container <a id="step-3-&#x2014;-setting-up-an-nginx-container"></a>

Let's get to work on fixing these security issues. The first step is to set up a copy of Nginx inside another Docker container and link it up to our Docker registry container.

Let's start by creating a directory to store our Nginx configuration:

```bash
mkdir ~/docker-registry/nginx
```

Now, re-open your `docker-compose.yml` file in the `~/docker-registry` directory:

Add a service on top of the registry service:

```text
version: '2'

services:

  nginx:
    restart: unless-stopped
    image: "nginx:1.9"
    ports: 
      - 5043:443
    volumes: 
      - ./nginx:/etc/nginx/conf.d:ro
    labels:
      - traefik.backend=registry
      - traefik.docker.network=traefik_proxy
      - traefik.frontend.rule=Host:registry.daton.it,docker-registry.daton.it
      - traefik.port=443
    networks:
      - traefik_proxy
      - registry_platform
```

Your full `docker-compose.yml` file should now look like this:

```text
version: '2'

services:

  nginx:
    restart: unless-stopped
    image: "nginx:1.9"
    ports: 
      - 5043:443
    volumes: 
      - ./nginx:/etc/nginx/conf.d:ro
    labels:
      - traefik.backend=registry
      - traefik.docker.network=traefik_proxy
      - traefik.frontend.rule=Host:registry.yourdomain.com
      - traefik.port=443
    networks:
      - traefik_proxy
      - registry_platform

  registry:
    hostname: registry
    restart: unless-stopped
    image: registry:2
    ports:
      - 127.0.0.1:5000:5000
    environment:    
      REGISTRY_STORAGE_FILESYSTEM_ROOTDIRECTORY: /data
    volumes:
      - ./data:/data
    networks:
      - registry_platform

networks:
  traefik_proxy:
    external: true
  registry_platform:
    external: false
    driver: bridge
```

We need to configure Nginx before this will work though, so let's create a new Nginx configuration file.

Create a `registry.conf` file:

```bash
nano ~/docker-registry/nginx/registry.conf
```

Copy the following into the file:

```text
upstream docker-registry {
  server registry:5000;
}

server {
  listen 443;
  server_name myregistrydomain.com;

  # SSL
  # ssl on;
  # ssl_certificate /etc/nginx/conf.d/domain.crt;
  # ssl_certificate_key /etc/nginx/conf.d/domain.key;

  # disable any limits to avoid HTTP 413 for large image uploads
  client_max_body_size 0;

  # required to avoid HTTP 411: see Issue #1486 (https://github.com/docker/docker/issues/1486)
  chunked_transfer_encoding on;

  location /v2/ {
    # Do not allow connections from docker 1.5 and earlier
    # docker pre-1.6.0 did not properly set the user agent on ping, catch "Go *" user agents
    if ($http_user_agent ~ "^(docker\/1\.(3|4|5(?!\.[0-9]-dev))|Go ).*$" ) {
      return 404;
    }

    # To add basic authentication to v2 use auth_basic setting plus add_header
    # auth_basic "registry.localhost";
    # auth_basic_user_file /etc/nginx/conf.d/registry.password;
    # add_header 'Docker-Distribution-Api-Version' 'registry/2.0' always;

    proxy_pass                          http://docker-registry;
    proxy_set_header  Host              $http_host;   # required for docker client's sake
    # Since we are using Nginx behind Traefik we don't need these headers
    # proxy_set_header  X-Real-IP         $remote_addr; # pass on real client's IP
    # proxy_set_header  X-Forwarded-For   $proxy_add_x_forwarded_for;
    # proxy_set_header  X-Forwarded-Proto $scheme;
    proxy_read_timeout                  900;
  }
}
```

Save and exit the file.

Now you can install Nginx and start up the two Docker containers all with one command:

```text
docker-compose up
```

First, make an HTTP request directly to the Docker registry:

```text
curl http://localhost:5000/v2/
```

As of this writing Docker returns an empty json object, so you should see:

```bash
{}
```

Now send an HTTP request to the Nginx port:

```text
curl http://localhost:5043/v2/
```

You should see the same output:

```bash
{}
```

### Setting Up Authentication <a id="step-4-&#x2014;-setting-up-authentication"></a>

Set up HTTP authentication so that we can control who has access to our Docker registry. To do that we'll create an authentication file in Apache format \(Nginx can read it too\) via the `htpasswd` utility we installed earlier and add users to it.

Create the first user as follows, replacing USERNAME with the username you want to use:

```bash
cd ~/docker-registry/nginx
htpasswd -c registry.password USERNAME
```

Create a new password for this user when prompted.

If you want to add more users in the future, just re-run the above command without the `-c` option \(the `c`is for create\):

```bash
htpasswd registry.password USERNAME
```

At this point we have a `registry.password` file with our users set up and a Docker registry available. You can take a peek at the file at any point if you want to view your users \(and remove users if you want to revoke access\).

Next, we need to tell Nginx to use that authentication file.

Open up `~/docker-registry/nginx/registry.conf` in your favorite text editor:

```bash
nano ~/docker-registry/nginx/registry.conf
```

Uncomment the two lines that start with `auth_basic` as well as the line that starts with `add_header` by removing the `#` character at the beginning  
of the lines. It should then look like this:~/docker-registry/nginx/registry.conf

```text
# To add basic authentication to v2 use auth_basic setting plus add_header
auth_basic "registry.localhost";
auth_basic_user_file /etc/nginx/conf.d/registry.password;
add_header 'Docker-Distribution-Api-Version' 'registry/2.0' always;
```

We've now told Nginx to enable HTTP basic authentication for all requests that get proxied to the Docker registry and told it to use the password file we just created.

Let's bring our containers back up to see if authentication is working:

```text
cd ~/docker-registry
docker-compose up
```

Repeat the previous curl test:

```text
curl http://localhost:5043/v2/
```

You should get a message complaining about being unauthorized:

```text
Output of curl<html>
<head><title>401 Authorization Required</title></head>
<body bgcolor="white">
<center><h1>401 Authorization Required</h1></center>
<hr><center>nginx/1.9.7</center>
</body>
</html>
```

Now try adding the username and password you created earlier to the `curl` request:

```text
curl http://USERNAME:PASSWORD@localhost:5043/v2/
```

You should get the same output you were getting before — the empty json object `{}`. You should also see the same `registry_` output in the `docker-compose` terminal.

Go ahead and use `CTRL-C` in the `docker-compose` terminal to shut down the Docker containers.

### Starting Docker Registry as a Service <a id="step-8-&#x2014;-starting-docker-registry-as-a-service"></a>

Let's go ahead and start it up to make sure everything is in order:

```bash
cd ~/docker-registry
docker-compose rm   # this removes the existing containers
docker-compose up -d
```

If everything went well you should have your Docker Registry up and running.

### Publish to your Private Docker Registry

From your **client machine**, create a small empty image to push to our new registry.

```bash
docker run -t -i ubuntu /bin/bash
```

After it finishes downloading you'll be inside a Docker prompt. Let's make a quick change to the filesystem by creating a file called `SUCCESS`:

```bash
touch /SUCCESS
```

Exit out of the Docker container:

```bash
exit
```

Commit the change:

```bash
docker commit $(docker ps -lq) test-image
```

Log in to your registry:

```text
docker login https://YOUR-DOMAIN
```

Enter the username and password you set up earlier, now let's tag our image to our private registry:

```bash
docker tag test-image [YOUR-DOMAIN]/test-image
```

Note that you are using the local name of the image first, then the tag you want to add to it. The tag does **not** use `https://`, just the domain, port, and image name.

Now we can push that image to our registry. This time we're using the tag name only:

```bash
docker push [YOUR-DOMAIN]/test-image
```

### Pull from Your Docker Registry <a id="step-11-&#x2014;-pull-from-your-docker-registry"></a>

To make sure everything worked, let's go back to our original server \(where you installed the Docker registry\) and pull the image we just pushed from the client. You could also test this from a third server.

If Docker is not installed on your test pull server, go back and follow the installation instructions \(and if it's a third server, the SSL instructions\) from Step 6.

Log in with the username and password you set up previously.

```bash
docker login https://[YOUR-DOMAIN]
```

And now pull the image. You want just the "tag" image name, which includes the domain name, port, and image name \(but not `https://`\):

```bash
docker pull [YOUR-DOMAIN]/test-image
```

## Docker Registry Manager

We can install a useful manager like this:

{% embed url="https://github.com/snagles/docker-registry-manager" %}

We just need to clone the repo and edit the `registry.yml` file, then run `docker-compose up -d` and go to `http://localhost:8080`

