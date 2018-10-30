Docker Cheatsheet
===

## Commonly Used Commands
1. Pull image from registry (docker hub)
```
$ docker pull [OPTIONS] NAME[:TAG|@DIGEST]
```
2. List Local Images
```
$ docker images 
```
3. Run a command in a **new** container
```
# normal run
$ docker run -it IMAGE bash
```
```
# run in background
$ docker run -it -d IMAGE bash
```
```
# mount local directory on container
$ docker run -it -v LOCAL_DIR_PATH IMAGE bash
```
4. Check container status
```
$ docker ps -a
``` 
5. Stop one or more running containers
```
$ docker stop CONTAINER
```
6. Start one or more stopped containers
```
$ docker start CONTAINER
```
7. Run a command in a running container
> Can be used to reconnect to containers that run on the background
```
$ docker exec -it CONTAINER bash
```
8. Commit image: Create a new image from a container's change
```
$ docker commit [-m "COMMIT MESSAGE"] [-a "AUTHOR"] CONTAINER [REPOSITORY[:TAG]]
```
9. Create a tag TARGET_IMAGE that refers to SOURCE_IMAGE
```
$ docker tag SOURCE_IMAGE[:TAG] TARGET_IMAGE[:TAG]
```
10. Remove one or more images
```
$ docker rmi [OPTIONS] IMAGE [IMAGE...]
```
11. Remove one or more containers
```
$ docker rm [OPTIONS] IMAGE [IMAGE...]
```
12. Push a image or repository to a registry
```
$ docker push [OPTIONS] NAME[:TAG]
```
