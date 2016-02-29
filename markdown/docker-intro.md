# Docker
![docker-logo](images/what_is_docker.jpg)

!SUB
### Docker architecture
![architecture](images/architecture.jpg)

!SUB
### Docker architecture
![architecture](images/docker-execdriver-diagram.png)

!SUB
## The Life of a Container  

!SUB
## Conception  
BUILD an Image from a Dockerfile  

!SUB
## Birth  
RUN (create+start) a container  

!SUB
## Reproduction  
COMMIT (persist) a container to a new image  
RUN a new container from an image  

!SUB
## Sleep  
STOP or KILL a running container  

!SUB
## Wake  
START a stopped container  

!SUB
## Death  
RM (delete) a stopped container  

!SUB
## Extinction  
RMI a container image (delete image)

!SUB
### The Life of a Container by example.

```
 docker pull mongo:latest     # pull the mongo image from the registry
 docker inspect mongo:latest  # list information of the container
 docker run -p 27017:27017 \
        --name my-mongo -d \
        mongo:latest          # create and start a mongo container
 docker inspect my-mongo      # inspect the running container info
 docker logs -f my-mongo      # tail the log of the container
 docker stop my-mongo         # stop the container
 docker rm -v my-mongo        # remove the container
 docker rmi mongo:latest      # remove the image from the local repo
```


!SUB
## Docker stages
![stages](images/docker-stages.png)



!SUB
### Information of a containter.

| command      | description           |
| ------------ |---------------|
| ps |shows running containers.|
| logs |gets logs from container.|
| inspect |looks at all the info on a container (including IP address).|
| events |gets events from container.|
| port |shows public facing port of container.|
| top |shows running processes in container.|
| stats |shows containers' resource usage statistics.|

!SUB
## Dockerfile

Each Dockerfile is a script, composed of various commands and arguments listed successively to automatically perform actions on a base image in order to create a new one. They are used for organizing things and greatly help with deployments by simplifying the process start-to-finish.

!SUB
## Dockerfile by example
```
FROM dockerfile/java:oracle-java8
MAINTAINER Niek Palm <dev.npalm@gmail.com>

RUN apt-get install git -y

ADD service.jar

EXPOSE 8080

CMD ["java","-jar","/service.jar"]

```
