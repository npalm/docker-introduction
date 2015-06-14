# Hands on Labs
## Prerequisites



### Network
* Connect via guest wifi to the internet and save your self some time.



### Ubuntu / Mint Linux

* Follow this [guide](http://docs.docker.com/installation/ubuntulinux/#installing-docker-on-ubuntu) 
* Add your user to the docker group.
* Update `/etc/default/docker` and update the `DOCKER_OPTS` to 
    ```
    DOCKER_OPTS="-H tcp://0.0.0.0:2375 -H unix:///var/run/docker.sock"
     ```
* Or see alternative ...



### Ubuntu / Mint Linux
* Alternatively you can execute the script below.

```
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 \
  --recv-keys 36A1D7869245C8950F966E92D8576A8BA88D21E9
sudo sh -c "echo deb https://get.docker.com/ubuntu docker main \
  > /etc/apt/sources.list.d/docker.list"

sudo apt-get update
sudo groupadd docker
user=$(whoami)
sudo gpasswd -a $user docker
sudo apt-get install cgroup-lite apparmor lxc-docker -y

sudo sh -c 'echo DOCKER_OPTS=\"-H tcp://0.0.0.0:2375 -H \
  unix:///var/run/docker.sock\" \
  > /etc/default/docker'
```



### Ubuntu / Mint Linux
* Test your installation as follow
    * open a shell
    * run 
        ```
        docker info
        ```



### Windows
For windows you should install virtualbox, git bash and boot2docker.
* Follow this (guide)[http://docs.docker.com/installation/windows/#installation]
    * Virtual box is used by boot2docker to host docker.
    * git bash, gives some working shell. Just install (git)[https://git-scm.com/download/win]
    * Boot2Docker provides a docker client and manage your docker in the vm.



### Windows
* Test your installation as follow
    * Windows start menu -> Start boot2docker
    * run
    ```
        docker info
    ```



### Mac
* Follow this (guide)[http://docs.docker.com/installation/mac/#install-boot2docker]
