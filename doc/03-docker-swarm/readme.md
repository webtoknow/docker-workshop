# [![docker.com](https://www.docker.com/favicons/favicon-32x32.png)](https://www.docker.com/) Docker workshop - Swarm

This section will show an introduction to features of Docker Engine Swarm mode.
Please go to [Docker Play](http://labs.play-with-docker.com/) and create 5 instances. 

# Swarm Cluster
The first thing to do is initialize the Swarm. Please chose the first node and init the swarm with the right ip address (e.g. 192.168.1.8).

```
docker swarm init --advertise-addr MANAGER_IP
```

We will see something like this:
```
$ docker swarm init --advertise-addr 10.0.36.4
Swarm initialized: current node (bcehpw80n4fs95stybwc7j4in) is now a manager.

To add a worker to this swarm, run the following command:

    docker swarm join \
    --token SWMTKN-1-45zr6hp91nty0yfveavjz1ptq7kfj2xzswizirqhd4a2ubnfm2-a24rmohwucu00y4i2rkv3ik0b \
    10.0.36.4:2377

To add a manager to this swarm, run 'docker swarm join-token manager' and follow the instructions.
```

We can check Swarm status by firing the node ls command to view information about nodes

```
docker node ls
```

Select a new node add it to swarm:

```
docker swarm join \
    --token SWMTKN-1-45zr6hp91nty0yfveavjz1ptq7kfj2xzswizirqhd4a2ubnfm2-a24rmohwucu00y4i2rkv3ik0b \
    10.0.36.4:2377
```

Let's check again nodes list:

```
docker node ls
```
# Create a Service
Now that we have our swarm up and running, it is time to schedule our containers on it. 

Start a service
```
docker service create --replicas 5 -p 80:80 --name web nginx
```

See service status
```
docker service ls
```

In the meanwhile, you can also see the status of the service and how it is getting orchestrated to the different nodes:

```
docker service ps web
```

# Scaling up and Scaling down

Let us bump it up to 8 as shown below by executing the command on the manager1 node.

```
docker service scale web=8
```

Let's check again how many containers are running

```
docker service ps web
```
# Inspecting nodes
You can inspect the nodes anytime via the docker node inspect command.

For manager:
```
docker node inspect self
```
For workers:
```
docker node inspect node.1
```

# Remove the Service
You can simply use the service rm command to remove web service
```
docker service rm web
```
# Applying Rolling Updates

This is straight forward. In case you have an updated Docker image to roll out to the nodes, all you need to do is fire an service update command.

For e.g.
```
docker service update --image <imagename>:<version> web
```


# Navigation 

Previous | Next 
:------- | ---: 
← [Docker Workshop - Docker compose](../02-docker-compose) | [Docker Workshop - Home](https://github.com/bmnicolae/docker-workshop) →
