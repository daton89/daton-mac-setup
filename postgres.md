# Postgres

## Running Postgres in a docker container

Open a terminal window an run:

```bash
docker run -d --name postgres \
    --restart unless-stopped \
    -v ~/Documents/data-db/postgres:/var/lib/postgresql/data \
    -e POSTGRES_USER=root \
    -e POSTGRES_PASSWORD=root \
    -p 5432:5432 postgres:10
```



