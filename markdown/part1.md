# Hands on Lab 1
## Hello world

!SUB
* All steps assumes you have a command line open.
  * For Windows users.
    * Commands where a shell is invoked like `/bin/bash` will fial, pleas add a trailing slash.
    * You can also login the boot2docker vm: `boot2docker ssh`
  * Linux users can do the all exercises just in a normal terminal.
* Have fun


!SUB
### Docker basics
* Below some of the basic docker commands

```
Commands:
    images    List images
    logs      Fetch the logs of a container
    ps        List containers
    pull      Pull an image or a repository from a Docker registry server
    rm        Remove one or more containers
    rmi       Remove one or more images
    run       Run a command in a new container
    start     Start a stopped container
    stop      Stop a running container

Run 'docker help' for all commands.
Run 'docker COMMAND --help' for more information on a command.
```

!SUB
### Pull an image
* First we pull a base image. We use ubuntu 14.04 latest as base. See [Ubuntu repo on docker registry](https://registry.hub.docker.com/_/ubuntu/)

```
docker pull ubuntu
```
* We have now the image of ubuntu in our local repository, verify with the command:

```
docker images
```

!SUB
### Start a docker container
* So time for hello world.
* With the next command you start an ubuntu container and execute the command the echo some famous string.

```
docker run ubuntu echo "hello world"
```
* Running the command above creates, starts and exit the ubuntu container. Observe the output with commands below.

```
docker ps
docker ps -a
docker rm <id> # to remove the container
```

!SUB
### Start a docker container 
* Start a container as demon.

```
docker run -d --name ubuntu ubuntu /bin/sh -c \
   "while true; do echo Hello world; sleep 1; done"
```

* Inspect the logging
* Stop the container

```
docker logs -f ubuntu
docker stop ubuntu
```

!SUB
### Update a docker image

* Changes made in a container are only persists in that container. At the moment the container is dertoyed the change is lost.
* Commit a change made in a container to an image, persists the change.

```
docker start ubuntu
docker -i -t ubuntu /bin/bash
 
```
* Update repositories and install the game cowsay and create a link and clean up

```
apt-get update && apt-get install cowsay -y && \
  ln /usr/games/cowsay /usr/bin/cowsay && rm -rf /var/lib/apt/lists/*

```

!SUB
### Update a docker image

* Test the game is working, exit the container.
```
cowsay "Hello world"
exit
```
* Our installed game is now available in the docker container with the name ubuntu. But not in the image
that is used to create the container.
* Commit you change in the container to an (new) image.
* Remove the container.
```
docker commit ubuntu <yourname>/ubuntu
docker diff ubuntu                 # shows the added files
docker history <yourname>/ubuntu   # shows the history of the image
docker stop ubuntu | docker rm     # remove the container
```

!SUB
### Update a docker image
* Now create a new container based on the new created image and run the game.
* The second command shows that the game isn't available in the ubuntu image.
```
docker run --rm <yourname>/ubuntu cowsay "Hello world"
docker run --rm ubuntu cowsay "Hello world"
```
* You can push your change to the docker registry therefore you need to create an own repository.

