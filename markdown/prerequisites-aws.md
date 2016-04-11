# Hands on Labs
## Prerequisites - AWS

!SUB
### Docker
* For the workshop we use today an AWS instances.
* Alternatively you can run all handson on your local
  * Linux : Install docker, docker-compose, git and your favourite editor
  * Mac / Windows : Install docker toolbox (includes git and virtual box)
  * VM : See the section Prerequisites - Vagrant


!SUB
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
 ssh -o ServerAliveInterval=120 -i <path>/HANDSON.pem ubuntu@<ip-aws-instance>
```

!SUB
### Windows Users: How to login to an AWS instance

- We are using a pem file (.ppk) to access the AWS instances. Click [here](key/HANDSON.ppk) to download the key and save it locally.
- Download [putty](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html)
- Start putty and enter the host ip
- Select `data` on the left hand side under `auto-login username` enter the user `ubuntu`
- Select `SSH`->`Auth` on the left hand side then under `private key for authentication` select the .ppk file we just downloaded.
- To prevent ssh timeout in putty select `connection`. Under "Sending of null packets to keep session active - Seconds between keepalives (0 to turn off)", enter `120` in the text box.
- Go back to the top and connect to your instance.
