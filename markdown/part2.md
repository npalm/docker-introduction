# Hands On Lab 2
## Building a image

!SUB
### Docker building your own webserver
* Below some of the docker commands

```
Commands:
    build     Build an image from a Dockerfile
    commit    Create a new image from a container's changes
    info      Display system-wide information
    inspect   Return low-level information on a container or image
    login     Register or log in to a Docker registry server
    logout    Log out from a Docker registry server
    port      Lookup the public-facing port that is NAT-ed to PRIVATE_PORT
    push      Push an image or a repository to a Docker registry server
    tag       Tag an image into a repository
    top       Lookup the running processes of a container

Run 'docker help' for all commands.
Run 'docker COMMAND --help' for more information on a command.
```

!SUB
### Building our own webserver
* In this lab we are going to build our own webserver images that hosts some static pages.
* Steps
    * Create some static content
    * Create a Dockerfile
    * Build a docker image
    * Run the image

!SUB 
### Create some static content

Create a empty dir.

```
mkdir webapp
cd webapp
```
Add some static contact, create a file index.html with some content for example.

```
<!DOCTYPE html>
<html><head> 
<meta charset="UTF-8"> 
<title>Hello world</title></head>

<body>Hello world</body>

</html>
```

!SUB
### The Dockerfile
With a dockerfile you specify how an images is build, which files are added and which command should executed when the container is started.

Create a file named Dockerfile and add the following content

```
FROM nginx
MAINTAINER <your name> <your.mail@domain.ext>

COPY index.html /usr/share/nginx/html/
```

!SUB
### Build docker image
* Building the image based on a parent image will create only the diff image. Now build the image, you should specify a repository and tag.
* Specify as repository "lab2/webapp" at leave the tag empty.

```
docker build --tag lab2/webapp .
```

Check the result
```
docker images 
docker history lab2/webapp
```

!SUB
### Run the image
So first we have a look of the description of the image. Here you will see two ports are exposed, 80 and 443. We will use port 80 and map it to 8888.
Start the container as deamon

```
docker run -d --name myapp -p 8888:80 lab2/webapp
```
Test with a browser or curl.

!SUB
### Clean up
* Have a look again on the description and you will see a volume will available.
* Since we did not mount the volume explicit it is mount implicit in ```/var/lib/docker/vfs/```. By adding the switch ```-v``` will remove the files as well.

```
docker stop myapp | xargs docker rm -v
```

!SUB
### Same same but different
![easy](images/easy.jpg)
```
docker run -d -p 8888:80 --name myapp -v \
  <dir-to-webapp>:/usr/share/nginx/html nginx
```
