# Frequently used commands



* kill all running containers with `docker kill $(docker ps -q)`
* delete all stopped containers with `docker rm $(docker ps -a -q)`
* delete all images with `docker rmi $(docker images -q)`
* delete all unused stuff `docker system prune -a`

Other commands:

{% embed url="https://medium.com/the-code-review/top-10-docker-commands-you-cant-live-without-54fb6377f481" %}

