# Hands on Labs
## Prerequisites



### Network
* Use the guest wifi, mobile or BYO Network
- Next sections will describe setup for a local or Amazon environment.



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
* Follow this [guide](http://docs.docker.com/installation/windows/#installation)
    * Virtual box is used by boot2docker to host docker.
    * git bash, gives some working shell. Just install [git](https://git-scm.com/download/win)
    * Boot2Docker provides a docker client and manage your docker in the vm.



### Windows
* Test your installation as follow
    * Windows start menu -> Start boot2docker
    * run
    ```
        docker info
    ```




### Windows shell client
Alternatively for the windows shell you can directly login to the docker vm using putty.
* Download [putty ssh client](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html)
* Start putty
  - Hostname: localhost
  - Port: Start vitualbox and lookup the ssh port, see portfowarding section.
  - SSH: Section tunnel and add the tunnel: Source port "8888", Destination "localhost:8888"
  - Go back to the main section and save the session (user: docker, password: tcuser)




### Mac
* Follow this [guide](http://docs.docker.com/installation/mac/#install-boot2docker)




### AWS
We are using AWS as infrastructure for running our Continuous Delivery services.



### AWS
Below some background information about Amazon Web Services:
- We have automated the creation of our AWS instances with the following tools:
  - Ansible in combination with ec2 module to use AWS EC2 api.
  - EC2 external inventory scripts to use dynamic inventory.
  - we have created ansible-playbook scripts that create the instances and provision the created instances with the necessary software for this handson lab.



### Linux/Mac Users: How to login to an AWS instance
- Windows users: skip this slide
- We are using a key file (.pem) to access the AWS instances.  
'Save link as' [here](key/HANDSON.pem) to download the key and save it locally.
- Open an terminal
- Your key must not be publicly viewable for SSH to work.

```
chmod 400 <path>/HANDSON.pem
```

- To prevent ssh timeout add ServerAliveInterval=120 as option  
to ssh command
- Connect via ssh

```
 ssh -o ServerAliveInterval=120 -i <path>/HANDSON.pem \
   ubuntu@<ip-aws-instance>
```



### Windows Users: How to login to an AWS instance

- We are using a pem file (.ppk) to access the AWS instances. Click [here](key/HANDSON.ppk) to download the key and save it locally.
- Download [putty](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html)
- Start putty and enter the host ip
- Select `data` on the left hand side under `auto-login username` enter the user `ubuntu`
- Select `SSH`->`Auth` on the left hand side then under `private key for authentication` select the .ppk file we just downloaded.
- To prevent ssh timeout in putty select `connection`. Under "Sending of null packets to keep session active - Seconds between keepalives (0 to turn off)", enter `120` in the text box.
- Go back to the top and connect to your instance.
