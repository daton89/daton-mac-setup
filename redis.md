# Redis

##  Running Redis in a docker container <a id="running-mongodb-in-a-docker-container"></a>

Open a terminal window an run:

```text
docker run -d --name redis \
    --restart unless-stopped \
    -v /Users/tony/data-db/redis:/data \
    -p 6379:6379 redis:4
```

  


