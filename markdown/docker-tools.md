# Docker tools
![docker-tools](images/docker-tools.jpg)

!SUB
### Docker toolbox

- The Docker Toolbox is an installer to quickly and easily install and setup a Docker environment on your computer.
- Available for both Windows and Mac, the Toolbox installs Docker Client, Machine, Compose (Mac only) and Kitematic.

![docker-toolbox](images/docker-toolbox.png)


!SUB
### Docker toolbox
![linux-mac-docker](images/linux-vm-docker.png)


!SUB
### Docker machine
Machine makes it really easy to create Docker hosts on your computer, on cloud providers and inside your own data center. It creates servers, installs Docker on them, then configures the Docker client to talk to them.
![docker-machine](images/docker-machine.png)



!SUB
### Docker compose

Compose is a tool for defining and running complex applications with Docker. With Compose, you define a multi-container application in a single file, then spin your application up in a single command which does everything that needs to be done to get it running.

![docker-compose](images/docker-compose.png)

!SUB
### Docker compose
```
gitlabdb:
  image: postgres
  environment:
    - POSTGRES_USER=gitlab
    - POSTGRES_PASSWORD=password
gitlab:
  image: sameersbn/gitlab
  links:
    - gitlabdb:postgresql
  environment:
    - DB_USER=gitlab
    - DB_PASS=password
  ports:
    - "10080:80"
  volumes:
    - ./data/gitlab/data:/home/git/data

```



!SUB
### Docker swarm
Docker Swarm is native clustering for Docker. It turns a pool of Docker hosts into a single, virtual host.


!SUB
## TOOLS - TOOLS - TOOLS
![tools](images/tools.jpg)


!SUB
## What about Microsoft?
![tools](images/docker-microsoft.jpg)

!SUB
## Container solution on Azure
![tools](images/docker-windows-linux.jpg)
