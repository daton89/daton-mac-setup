# Frequently used commands



* kill all running containers with `docker kill $(docker ps -q)`
* delete all stopped containers with `docker rm $(docker ps -a -q)`
* delete all images with `docker rmi $(docker images -q)`
* delete all unused stuff `docker system prune -a`



