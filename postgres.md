# Postgres

## Running MongoDB in a docker container

Open a terminal window an run:

```bash
docker run -d --name postgres \
    --restart unless-stopped \
    -v /Users/tony/data-db/postgres:/var/lib/postgresql/data \
    -p 5432:5432 postgres:10
```



