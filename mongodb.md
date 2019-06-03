# MongoDB

## Running MongoDB in a docker container

Open a terminal window and run:

```bash
docker run -d --name mongodb \
    --restart unless-stopped \
    -v /Users/tony/data-db/mongodb:/data/db \
    -v /Users/tony/data-db/mongodumps:/mongodumps \
    -p 27017:27017 mongo:3.4
```

{% hint style="info" %}
 Running databases in containers is not suggested for production environment
{% endhint %}

{% hint style="info" %}
On WSL you could have issues mounting the volume into the container.



```bash
docker volume create \
  --opt type=cifs \
  --opt device=c:\Users\tonyd\data-db\mongodb \
  --opt o=username=DockerHost,password=dockerhost,file_mode=0777,dir_mode=0777,uid=2000,gid=2000 \
  mongodb
```



```bash
docker run -d --name mongodb \
    --restart unless-stopped \
    -v mongodb:/data/db \
    -v mongodumps:/mongodumps \
    -p 27017:27017 mongo:3.4
```
{% endhint %}

## Install MongoDB Compass

To manage your MongoDB instance we use Compass:

```bash
brew cask install mongodb-compass
```

## Create MongoDB container for build tests 

Open a terminal window and run: 

```bash
docker run -d --name mongodb-test \
    --restart unless-stopped \
    -p 127.0.0.1:37017:27017 mongo:3.4
```

Once it is running the shell will return the container id that looks like: 

```text
0cd914b8310184808ce749ab3222e3fa480038952af39807f571b39a52e7e3f8
```

Now we should enter in the container and run the mongoShell to operate on the db:

```bash
docker exec -it mongodb-test bash
# we can now launch the mongoshell typing mongo
root@0cd914b83101:/# mongo
MongoDB shell version v3.4.15
connecting to: mongodb://127.0.0.1:27017
MongoDB server version: 3.4.15
Welcome to the MongoDB shell.
For interactive help, type "help".
For more comprehensive documentation, see
	http://docs.mongodb.org/
Questions? Try the support group
	http://groups.google.com/group/mongodb-user
Server has startup warnings:
2018-09-27T11:54:42.732+0000 I STORAGE  [initandlisten]
2018-09-27T11:54:42.732+0000 I STORAGE  [initandlisten] ** WARNING: Using the XFS filesystem is strongly recommended with the WiredTiger storage engine
2018-09-27T11:54:42.732+0000 I STORAGE  [initandlisten] **          See http://dochub.mongodb.org/core/prodnotes-filesystem
2018-09-27T11:54:42.854+0000 I CONTROL  [initandlisten]
2018-09-27T11:54:42.855+0000 I CONTROL  [initandlisten] ** WARNING: Access control is not enabled for the database.
2018-09-27T11:54:42.855+0000 I CONTROL  [initandlisten] **          Read and write access to data and configuration is unrestricted.
2018-09-27T11:54:42.855+0000 I CONTROL  [initandlisten]
>
```

We are now ready to populate the db with some sample data for out tests suite. 

### Populating the Database

With the command `use DATABASE_NAME` MongoDB will create a new db called _DATABASE\_NAME_, then we can check if it worked typing `show dbs`, since it hasn't any document it doesn't show the created db, so we need to insert a document by typing `db.users.insert({"username": "daton", "password": "$2a$13$RnsMJ9C6LgZTOOYANiTKbO4vgnVo3MulMMfrL/Ly7E04sqSGmg8dO"})`, now typing `show dbs` return also the list of the newly created db. 

```bash
> use daton_auth
switched to db daton_auth
> show dbs
admin  0.000GB
local  0.000GB
> db.users.insert({"username": "daton", "password": "$2a$13$RnsMJ9C6LgZTOOYANiTKbO4vgnVo3MulMMfrL/Ly7E04sqSGmg8dO"})
WriteResult({ "nInserted" : 1 })
> show dbs
admin        0.000GB
local        0.000GB
daton_auth  0.000GB
>
```

We can now exit from the shell and the container, press ctrl+c then ctrl+d:

```text
> ^C
bye
root@0cd914b83101:/# exit
```

We are now ready to build and push the image to docker registry.

### Push Image to Private Docker Registry

```text
14:28:10 in ~ via ⬢ v8.11.2 took 27m 45s
➜ docker commit $(docker ps -lq) mongodb-test
sha256:10276f0e2af807d725905c52f020a2a86b29c8caf5cbae2061e50b94f630ab2f

14:28:28 in ~ via ⬢ v8.11.2
➜ docker tag mongodb-test $REGISTRYADDRESS/mongodb-test

14:29:02 in ~ via ⬢ v8.11.2
➜ docker push $REGISTRYADDRESS/mongodb-test
The push refers to repository [$REGISTRYADDRESS/mongodb-test]
a0c3435b9e9f: Pushed
3bdfc7b15c4a: Pushed
84d5f4a4e9e6: Pushed
8cbce8e02108: Pushed
278c33372e35: Pushed
a0d9c837c597: Pushed
68a272e55e7a: Pushed
a2287de7d928: Pushed
8e810b18217e: Pushed
b81c040c9ace: Pushed
8d8ae80a45b3: Pushed
ba291263b085: Pushed
latest: digest: sha256:a022b3a241f28416aa7ec90bd660a38c4cc02ecda7b518cca5fbf57c9472c4d2 size: 2821
```

