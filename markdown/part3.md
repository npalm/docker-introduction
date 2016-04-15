# Hands On Lab 3
![networking](images/turtles.jpg)
## Networking

!SUB
### Docker networking topology
![test](images/docker-network-topology.png)
- none, no networking
- bridge, each container has is own
- joined, containers shares a single networking
- hosts, use the host networking

!SUB
### Docker networking topology by Example


```
# Run a container with no network
docker run --rm --net none busybox:latest ifconfig

# Run a container in a bridged network
docker run --rm --net bridge busybox:latest ifconfig

# or (bridge is the default)
docker run --rm busybox:latest ifconfig

# joined
docker run --name joined1 -d --net none busybox:latest \
  nc -l 127.0.0.1:3333
docker run --rm -it --net container:joined1 busybox:latest netstat -al

# host
docker run --rm --net host busybox:latest ifconfig
```

!SUB
### Container linking
- Docker has a linking system that allows you to link multiple containers together and send connection information from one to another.
- When containers are linked, information about a source container can be sent to a recipient container.
- To establish links, Docker relies on the names of your containers.
- First we create a container for our database.
```
# EXAMPLE ONLY
docker run -d --name postgres <image> <command>
```
- Secondly we link our database to our web container
```
# EXAMPLE ONLY
docker run -d --link postgres:db --name web <image> <command
```

!SUB
### Building a cluster
Next we build a simple cluster containing.
- One node acting as proxy, nginx is used as proxy.
- Three nodes acting as web server, nginx is used as web server.
- One node acting as data store, redis is used as key value store.
![cluster](images/simple-cluster.jpg)

!SUB
### Building a cluster - getting sources
Clone the following git repo.
```
cd
git clone https://github.com/npalm/simple-docker-cluster.git
cd simple-docker-cluster
```

!SUB
### Building a cluster - data store
- For the data store we use redis, a fast in memory key store.
- We can build a redis image our selves or use the offical one. An example is available in the redis directory.

```
# Search for the offical redis image in the docker registry
docker search redis

# download the image
docker pull redis

# inspect the image and look for the volumes listed
docker inspect redis
```

- Using `docker inspect` you should be able to find the a section that describes the volumes. This is the part where the container is supposed to store the persistent data.


!SUB
### Building a cluster - data store
- The volume for the redis conatiner `/data` is thet place where the container stores ithe data. If we do not specify the volume explicit docker will create a volume for us, a docker managed volume.

```
# start a redis container
docker run -d --name redis redis

# find the volume name and list the volumes.
docker inspect --format='{{range .Mounts}}{{.Name}}{{end}}' redis
docker volume ls

# remove the redis contaienr, -v will remove the volume as well.
docker rm -v -f redis
```

- For our redis container we mount a volume explicit. We mount a directory from the host direct to the container.

```
# start the data store
mkdir .data \
docker run -d --name redis -v $(pwd)/.data:/data redis
```


!SUB
### Building a cluster - web layer
- We use node.js as web server.
- Have a look at the Dockerfile in the web directory. We use the official node image as base image.

```
# Build the image
docker build -t lab3/web web

# Start the container, not exposting the port is optional
docker run -d -p 8080:8080 --link redis:redis --name web1 lab3/web

# Test
curl http://localhost:8080

# Inspect logging
docker logs -f web1

# Add two more nodes
docker run -d --link redis:redis --name web2 lab3/web
docker run -d --link redis:redis --name web3 lab3/web

```

!SUB
### Building a cluster - proxy layter
- We use nginx as proxy server.
- Have a look at the nginx configuration file in the proxy directory.
- We build the proxy server on top of the official docker image. Have a look at the Dockerfile.

```
# Build the image
docker build -t lab3/proxy proxy

# Start the container.
docker run -d -p 80:80 --name proxy \
  --link web1:web1 --link web2:web2 --link web3:web3 lab3/proxy

# Test your cluster and inspect the logging
# Open a new terminal
docker logs -f proxy

# Back to terminal one and fire some requests (or use the browser)
for i in {0..99}; do curl http://localhost; echo ""; done
```


!SUB
### Clean up
- Docker ps shows you the conainters
- Docker rm removes conainters

```
# -v removes inplicit mounts volumes
# -f force to remove running containers
# -q shows id only
# -a show all (also stpped ones)
docker rm -v -f $(docker ps -q -a)
```

!SUB
### Same same but different
![easy](images/easy.jpg)
```
# have a look at the compose file
cat docker-compose.yml

# build the conatiners
docker-compose build

# start the containers
docker-compose up

# execute in a new terminal window
for i in {0..99}; do curl http://localhost; echo ""; done
```
