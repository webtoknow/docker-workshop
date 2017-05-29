# [![docker.com](https://www.docker.com/favicons/favicon-32x32.png)](https://www.docker.com/) Docker workshop - Basics

This section is separated in:

* [CLI Basics](#cli-basics)
* [Dockerfile basics](#dockerfile-basics)

# CLI Basics

### Version

Check you have latest version of docker installed:

```
docker version
docker -v
```

* If you don't have docker installed, check [here](https://docs.docker.com/installation/#installation)
* If you're not on the latest version, it will prompt you to update
* If you're not on docker group you might need to prefix commands with `sudo`. See [here](http://docs.docker.com/installation/ubuntulinux/#giving-non-root-access) for details about it.

### Commands

Check the available docker commands

```
docker
docker --help
```

* Whenever you don't remember a command, just type docker
* For more info, type `docker help COMMAND` (e.g. `docker help run`)

### RUN a "Hello World" container

```
docker run alpine echo "Hello World"
```

* If the Image is not cached, it pulls it automatically
* It prints `Hello World` and exits

### SEARCH a IMAGE

```
docker search -s 10 nginx
```

* **-s**: Only displays with at least x stars

### RUN a Container and expose a Port

```
docker run -d -p 4000:80 nginx
```
Open a BROWSER with URL [localhost:4000](http://localhost:4000/)

* **-d**: Detached mode: Run container in the background, print new container id
* **-p**: Publish a container's port to the host (format: *hostPort:containerPort*)
* For more info about the container, see [nginx](https://registry.hub.docker.com/_/nginx/)

### RUN a Container with a Volume

NOTE: Make sure to be on `Docker Workshop` directory since we'll use volume mounts in the containers of directories of the repository.

On Linux and Mac
```
docker run --name daemon -d -p 4001:80 -v $(pwd)/code/hello-world/src/:/usr/share/nginx/html:ro nginx
```
Open a BROWSER with URL [localhost:docker](http://localhost:4001/)

* **-v**: Bind mount a volume (e.g., from the host: -v /host:/container, from docker: -v /container)
* The volume is **linked** inside the container. Any external changes are visible directly inside the container.
* This example breaks the immutability of the container, good for debuging, not recommended for production (Volumes should be used for data, not code)

### SHOW all images
Let’s list our images:

```
docker image ls
```
* **docker image ls** is command to command to list images.

### SHOW all containers
Let’s see what containers do we have now:

```
docker ps -a
```
* **docker ps** is command to command to list containers.
* **-a** show all containers (default shows only running).

### SHOW container logs
Let’s see what daemon container is doing right - let’s see the logs of it:

```
docker logs -f daemon
```

* **docker logs** is command to fetch the logs of a container.
* **-f** flag to follow the log output (works actually like `tail -f`).

### STOP/START/REMOVE container

Now let’s stop `daemon` container:

```
docker stop daemon
```

* **docker stop** is command to stop Docker container.

```
docker ps -a
```

Now container `daemon` is stopped. We can start it again:

```
docker start daemon
```

And ensure that it’s running:

```
docker ps -a
```

Now let’s stop it again and remove all the containers manually:

```
docker stop daemon
docker rm <your first container name>
docker rm daemon
```

To remove all containers we can use this command:

```
docker rm -f $(docker ps -aq)
```

* **docker rm** is command to remove container.
* **-f** flag (for `rm`) is to stop container if it's running (force deletion).
* **-q** flag (for `ps`) is to print only container IDs.

Let's run `ps` again to ensure that we don't have containers:

```
docker ps -a
```
### Start Spring Boot MongoDB aplication

Let’s start mongoDb container

```
docker run --name mongo -p 27017:27017 -d mongo
```

Now we cand start Spring Boot aplication
```
cd code
git clone https://github.com/springframeworkguru/spring-boot-mongodb.git
cd spring-boot-mongodb/
mvn package install
cd target/
java -jar spring-boot-mongodb-0.0.1-SNAPSHOT.jar
```

Let’s stop `daemon` container:
```
docker stop mongo
```

Let’s start mongoDb container with volume
```
docker run -p 27017:27017 -d mongo -v /Users/bogdan/Desktop/mongo:/data/db
```

# Navigation 

Previous | Next 
:------- | ---: 
← [Docker Workshop - Home](https://github.com/bmnicolae/docker-workshop) | [Docker Workshop - Docker machine](../01-docker-machine) →