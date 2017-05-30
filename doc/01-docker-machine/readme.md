# [![docker.com](https://www.docker.com/favicons/favicon-32x32.png)](https://www.docker.com/) Docker workshop - Machine

In this section we'll introduce `docker-machine`.

## Create a VM running Docker

Open a terminal on your computer. 

Create and run a VM named `default` using the following command:

```
docker-machine create -d virtualbox default
```

You can list the existing docker-machines:

```
docker-machine ls
```

In case you already had the machine created, you can simply start the VM:

```
docker-machine start default
```

## Run a docker container in a docker-machine
We can see `default` machine environment variables:

```
docker-machine env default
```

Now, let's use the docker-machine we've just created. We want to run the `hello-world`.

If you use Mac, you need to run:
```
eval $(docker-machine env default)
```

This command set the `DOCKER_HOST` variable to the IP of your `default` `docker-machine`.

Then we can run the `hello-world` container:
```
docker run hello-world
```

## Clean up

After we tested our `default` `docker-machine` we want to remove it from our computer.

Stop the VM named `default`:

```
docker-machine stop default
```

You can destroy the VM named `default`:

```
docker-machine rm default
```

## Create two machines

To create two machines do:

```
docker-machine create -d virtualbox client1
docker-machine create -d virtualbox client2
```

Now you can see the machines with:

```
docker-machine ls
```

## Run Nginx on client1

```
eval $(docker-machine env client1)
docker run -d -p 80:80 nginx:1.8-alpine
docker-machine ip client1
open "http://$(docker-machine ip client1)"
```

## Run Nginx on client2

```
eval $(docker-machine env client2)
docker run -d -p 80:80 nginx:1.8-alpine
docker-machine ip client2
open "http://$(docker-machine ip client2)"
```

## SSH to machine

To SSH inside a machine:

```
docker-machine ssh client1
```

Exit machine:
```
exit
```

## Environment variables

Docker client is configured by environment variables to connect with remote daemons. The following command outputs the variables for connecting to previously created `default` VM.

```
docker-machine env client1
```

## Active Machine

To get the active machine's name do:

```
docker-machine active
```

## Cleanup


```
docker-machine stop client1 client2
docker-machine rm client1 client2
```


# Navigation 

Previous | Next 
:------- | ---: 
← [Docker Workshop - Docker Basics](../00-docker-basics) | [Docker Workshop - Docker Compose](../02-docker-compose) →

# Credits

This workshop was prepared by [harbur.io](http://harbur.io), under MIT License. Feel free to fork and improve.


# Navigation 

Previous | Next 
:------- | ---: 
← [Docker Workshop - Docker Basics](../00-docker-basics) | [Docker Workshop - Docker Compose](../02-docker-compose) →
