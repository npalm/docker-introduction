# Docker tools
![docker-tools](images/docker-tools.jpg)

!SUB
### Docker compose
Compose is a tool for defining and running complex applications with Docker. With Compose, you define a multi-container application in a single file, then spin your application up in a single command which does everything that needs to be done to get it running.

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
### Docker machine
Machine makes it really easy to create Docker hosts on your computer, on cloud providers and inside your own data center. It creates servers, installs Docker on them, then configures the Docker client to talk to them.
![docker-machine](images/beta.png)

!SUB
### Docker swarm
Docker Swarm is native clustering for Docker. It turns a pool of Docker hosts into a single, virtual host.


!SUB
### Service discovery
![service-discover](images/discover-flow.jpg)


!SUB
### Service discovery
|       |       |
| ------------ |---------------|
|etcd| service discovery, globally distributed key-value store|
|consul| service discovery, globally distributed key-value store|
|zookeeper| service discovery, globally distributed key-value store|
|confd| watches key-value store for changes and triggers reconfiguration of services with new values|
|       |       |

!SUB
### Scheduling, Cluster Management, and Orchestration
![example-schedule](images/example-schedule.jpg)

!SUB
### Scheduling, Cluster Management, and Orchestration
|       |       |
| ------------ |---------------|
|fleet| scheduler and cluster management tool.|
|marathon| scheduler and service management tool.|
|swarm| scheduler and service management tool.|
|mesos| host abstraction service that consolidates host resources for the scheduler.|
|kubernetes| advanced scheduler capable of managing container groups.|
|compose| container orchestration tool for creating container groups.|
|       |       |

!SUB
## TOOLS - TOOLS - TOOLS
![tools](images/tools.jpg)


!SUB
## What about Microsoft?
![tools](images/docker-microsoft.jpg)

!SUB
## Container solution on Azure
![tools](images/docker-windows-linux.jpg)
