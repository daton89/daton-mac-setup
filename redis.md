# Redis

##  Running Redis in a docker container <a id="running-mongodb-in-a-docker-container"></a>

Open a terminal window an run:

```bash
docker run -d --name redis \
    --restart unless-stopped \
    -v ~/data-db/redis:/data \
    -p 6379:6379 redis:4
```

### On Windows

```bash
# First create a volume 
docker volume create --name=redisdata

# Run the container
docker run -d --restart unless-stopped --name redis -v redisdata:/data -d -p 6379:6379 redis:5
```

