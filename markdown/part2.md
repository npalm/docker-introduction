# Hands On Lab 2
![dockerfile](images/dockerfile.png)
## Building a image

!SUB
### Docker building your own webserver
* Below some of the docker commands

```
docker help

# Partial output

Commands:
    build     Build an image from a Dockerfile
    commit    Create a new image from a container's changes
    info      Display system-wide information
    inspect   Return low-level information on a container or image
    login     Register or log in to a Docker registry server
    logout    Log out from a Docker registry server
    port      Lookup the public-facing port that is NAT-ed to
              PRIVATE_PORT
    push      Push an image or a repository to a Docker registry server
    tag       Tag an image into a repository
    top       Lookup the running processes of a container
```

!SUB
### Building our own webserver
* In this lab we are going to build our own webserver image that hosts some static pages.
* Steps
    * Create some static content
    * Create a Dockerfile
    * Build a docker image
    * Run the image

!SUB
### Create some static content
* Create a empty dir.
```
mkdir lab2-web
cd lab2-web
```
* Add some static contact, create a file `index.html` with some content for example.

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

!SUB
### Build docker image
Create a file named `Dockerfile` and add the following content

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
* Check the result
```
docker images
```

!SUB
### Run the image
* First we have a look of the description of the image. Here you will see two ports are exposed, 80 and 443. We will use port 80 and map it to 8888.
Start the container as deamon
```
docker run -d --name myapp -p 8888:80 lab2/webapp
```
* Test with a browser or curl.
* Clean up
```
docker stop myapp | xargs docker rm
```

!SUB
### Run the image [OPTIONAL]
* When automating it does not work when you have to decide on design time which port you need to claim on the host.
* You can let docker decide which port to claim by leaving the map on the host site empty. `docker run -d -p 80 ...`. The result of this command is the container id. By using the command `docker port <id>` you can find the mapped port.
* The next command combines all previous actions.
```
docker port $(docker run -d --name myapp -p 80 lab2/webapp) | \
    cut -d\> -f2 | \
    xargs curl
```
* Clean up
```
docker stop myapp | xargs docker rm
```

!SUB
### Automated build

![docker-machine](images/optional.jpg)

###This section is optional
* Less than 20 minutes to go, read the next slide and go to lab 3


!SUB
### Automated build
* In Lab 1 we have build a docker container manually. In the first part of the second lab we automated our build using a Dockerfile. The next step is to automate the proces as whole.
* The docker hub provides automated build. Follow the next steps to autoomate the docker build.
* The next steps will guide you to set up the build.
  * Create a git repo in GitHub or BitBucket, create an account if you don't have
  * Create a dockerhub account if you don't have it yet.
  * Create an automated build on dockerhub.
  * Push the source code to your git repo.

!SUB
### Automated build (GIT)
- Create a [GitHub](http://www.github.com) or [BitBucket](http://www.bitbucket.org) account (or use an existing if you have). We using a public git repo to host our code.
- Create a new repository `lab2-web`.


!SUB
### Automated build (DockerHub)
The next step is to automate the build.
- Go to the Docker hub: [dockerhub])(https://hub.docker.com/) and create an account.
- Connect your GitHub (or BitBucket) to your Docker Hub account.
- Create an automated build (top menu).
- Use as name for the docker hub repo: `lab2-web` and choose create.
- Next go to build settings:
  - Set Name to `master`, should be the default.
  - Set Docker Tag Name to `latest`, should be the default.
- Click save changes.

!SUB
### Automated build
- Commit and push your sources to the created git repo to trigger a build.

```
# Ensure you are in the directory lab2-web
echo '# lab2-web' >> README.md
git init
git add --all
git commit -m "Some comment"
git remote add origin <your git url>
git push -u origin master

```

!SUB
### Automated build
- Observe the output on the build page on Docker Hub. Once the build is done create a container based on your new build image.
- You could also trigger a build with a HTTP post. See the instructions on the build settings page.

```
docker run -d --name myapp -p 8888:80 \
    <docker-hub-account>/lab2-web
```


!SUB
### Same same but different
![easy](images/easy.jpg)
```
docker run -d -p 8888:80 --name myapp -v \
  <dir-to-webapp>:/usr/share/nginx/html nginx
```
