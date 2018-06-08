# MongoDB

## Running MongoDB in a docker container

Open a terminal window an run:

```bash
docker run -d --name mongodb \
    --restart unless-stopped \
    -v /Users/tony/data-db/mongodb:/data/db \
    -p 27017:27017 mongo:3.4
```

{% hint style="info" %}
 Running databases in containers is not suggested for production environment
{% endhint %}

## Install MongoDB Compass

To manage your MongoDB instance we use Compass:

```bash
brew cask install mongodb-compass
```



