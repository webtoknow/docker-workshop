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
```

* Whenever you don't remember a command, just type docker
* For more info, type `docker help COMMAND` (e.g. `docker help run`)

### RUN a "Hello World" container

```
docker run alpine echo "Hello World"
```

* If the Image is not cached, it pulls it automatically
* It prints `Hello World` and exits

### SEARCH a Container

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
docker run -d -p 4001:80 -v $(pwd)/code/hello-world/site/:/usr/share/nginx/html:ro nginx
```
Open a BROWSER with URL [localhost:4001](http://localhost:4001/)

* **-v**: Bind mount a volume (e.g., from the host: -v /host:/container, from docker: -v /container)
* The volume is **linked** inside the container. Any external changes are visible directly inside the container.
* This example breaks the immutability of the container, good for debuging, not recommended for production (Volumes should be used for data, not code)


# Navigation 

Previous | Next 
:------- | ---: 
← [Docker Workshop - Home](https://github.com/bmnicolae/docker-workshop) | [Docker Workshop - Docker machine](../01-docker-machine) →