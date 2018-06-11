# Redis

##  Running Redis in a docker container {#running-mongodb-in-a-docker-container}

Open a terminal window an run:

```text
docker run -d --name redis \
    --restart unless-stopped \
    -v /Users/tony/data-db/redis:/data \
    -p 6379:6379 redis:4
```

  


