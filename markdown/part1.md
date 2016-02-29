# Hands on Lab 1
![helloworld](images/helloworld.png)
## Hello world

!SUB
### Some notes
* All steps assumes you have a command line open.
  * Almost all steps formatted as code can be executed.
    *  `\` is a line break and can be copied and pasted.
    * `< ... > ` indicates you should replace the value
* Since the VM includes a local registry cache some steps are slight different for a VM. These steps are prefixed with \[VM\].


!SUB
### Docker basics
* Below some of the basic docker commands

```
docker help

# Partial output
Commands:
    images    List images
    logs      Fetch the logs of a container
    ps        List containers
    pull      Pull an image or a repository from a Docker registry
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
* [VM]: The VM already containers the images.
```
docker pull ubuntu
```
* We have now the image of ubuntu in our local repository, verify with the command:
```
docker images
```
* [VM]: You will see many images since all images are pre fetched.


!SUB
### Start a docker container
* Time for hello world.
* With the next command you start an ubuntu container and execute the command echo some famous string.
```
docker run ubuntu echo "hello world"
```
* Running the command above creates, starts and exit the ubuntu container. 
- Observe the output with commands below, remember you can get help by executing `docker help` or `docker help ps`
```
docker ps
docker ps -a
```
- Remove the container
```
docker rm <id or name>
```

!SUB
### Start a docker container
* Start a container as deamon which prints the string "hello world" every second.
```
docker run -d --name mycontainer ubuntu /bin/sh -c \
   "while true; do echo Hello world; sleep 1; done"
```
* Inspect the logging
```
docker logs -f mycontainer
```
* Hit ctrl-c to exit the logging
* Stop the container
```
docker ps
docker stop mycontainer
docker ps
docker ps -a
```

!SUB
### Update a docker image

* Changes made in a container are persisted only in that container. At the moment the container is destroyed the change is lost too.
* Commit a change made in a container to an image, persists the change.

```
# Start our container
docker start mycontainer

# Exec the bash shell, this command gives access to our container
docker exec -i -t mycontainer /bin/bash

## You should see now something like:
> root@<id>:/# _
```

!SUB
### Update a docker image
* Next we are going to
  * update the repositories
  * install the game cowsay
  * create a symbolic link
  * clean up
* The next command is a composite of all these actions.

```
apt-get update && apt-get install cowsay -y && \
  ln /usr/games/cowsay /usr/bin/cowsay && rm -rf /var/lib/apt/lists/*

```

!SUB
### Update a docker image

* Test the game is working.
```
cowsay "Hello world"
```
* Next we exit the container.
```
exit
```
* Our installed game is now available in the docker container with the name mycontainer. But not in the image that is used to create the container.
* You can now execute the cowsay command in the same way as running the bash shell.
```
docker exec -i -t mycontainer cowsay "Hello <name>"
```

!SUB

### Update a docker image
* Commit your changes in the container to an (new) image.
```
docker commit mycontainer <yourname>/ubuntu
```
* Inspect your changes.
```
docker diff mycontainer           # shows the added files
docker history ubuntu             # shows the image history
docker history <yourname>/ubuntu  # shows the image history
```
* Remove the container.
```
docker stop mycontainer \
       | xargs docker rm          # remove the container
```


!SUB
### Update a docker image
* Now create a new container based on the new created image and run the game.
```
docker run --rm <yourname>/ubuntu cowsay "Hello world"
```
* The next command shows that the game isn't available in the ubuntu image.
```
docker run --rm ubuntu cowsay "Hello world"
```
* You can push your change to the docker registry therefore you need to create an own repository. But rememeber it is a bad practice to push manual build binaries into a repository.


!SUB
### Adding docker ui
- In the next part we are creating more docker containers. Just for the fun we install a dockerui on our host. So we can observer our containers via a web application.
- Create a container for running dockerui as follow.

```
docker run -d -p 9000:9000 \
  -v /var/run/docker.sock:/var/run/docker.sock \
  --privileged dockerui/dockerui
```
- Browse to [http://localhost:9000](http://localhost:9000) to see which containers are running, when using docker toolbox on Mac or Windows replace localhost by the ip of the docker machine.
