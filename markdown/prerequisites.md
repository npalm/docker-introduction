# Hands on Labs
## Prerequisites


!SUB
### Some guidelines
* You will find the slides here: [http://npalm.github.io/docker-introduction-dl/](http://npalm.github.io/docker-introduction-dl/)
- Navigation through the slides is easy, just use your arrow keys. Left and right for going to the previous or next section and up and down for previous or next page. The space bar always give you the next page.
- All code blocks unless mentioned are meant to execute by your self.
- Have fun, take your time and feel free to ask questions.

!SUB
### Environment Introduction
* We use a VirtualBox VM to setup a common environment.
* We use Vagrant to automate the setup of the VM
* The VirtualBox appliance contains
  * Ubuntu 14.04 Desktop
  * Tools: Docker, Docker Compose and Git (at least)
  * User: Vagrant, Password: Vagrant


!SUB
### Installation
* Download and install [VirtualBox](https://www.virtualbox.org/wiki/Downloads) and [Vagrant](https://www.vagrantup.com/downloads.html)
* Once VirtualBox and Vagrant are installed you open an terminal
  * Create a new directory.
```
mkdir docker-introduction
cd docker-introduction
```
  * Initialize vagrant and download the images when not available locally. 
```
vagrant init npalm/ubuntu-1404-dev-desktop
```
  * Start the virtual environment for the workshop.
```
vagrant up --provider virtualbox
```
* We have now running Ubuntu linux VM running with all the needed packages for the workshop. The default user is vagrant with password vagrant. 

!SUB
### Vagrant basics
* Below some useful vagrant commands.

```
vagrant up               # Starts the VM
vagrant halt             # Stops the VM
vagrant destory          # Removes the VM
vagrant box list         # Shows all the local vagrant boxes
vagrant box remove <id>  # Removes a box
```
