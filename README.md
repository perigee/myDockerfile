# Docker 
-----------------

## Prerequisites 


### Installation

The installation of docker is out of scope of this tutorial, please refer the official [document](https://docs.docker.com/installation/ubuntulinux/) for the docker installation.

### Rules

- Create the Images (Dockfiles) for development (mount project as volume) and deployment (integrate project) 
- Keep persistent data separating from docker container
- Connect the docker containers instead of putting everything in the same container

## Operations

### Run 

#### Run docker container in interactive mode with option `-t` and `-i`

``` bash
    > docker run -t -i ubuntu:14.04.2 /bin/bash
```

#### Run docker container with [volume](https://docs.docker.com/userguide/dockervolumes/) mounted by option `-v`

``` bash
    > docker run -t -i -v hostDir1:containerDir1 \
                       -v hostDir2:containerDir2 \
                       ubuntu:14.04.2 /bin/bash
```

##### Set volume as privileged, Ex. active host usb 

``` bash
    > docker run -t -i --privileged -v /dev/bus/usb:/dev/bus/usb \
                                    ubuntu /bin/bash
```

#### Run docker container with ports opened by option `-p` 

``` bash
    > docker run -t -i -p 80:8080 ubuntu:14.04.2 /bin/bash
```

### Manage Image

#### Commit the change in container to image

``` bash
    > docker ps # verify the containerID
    > docker commit -m "some mesg" containerID imageName:tag
```

#### Export/Import Image to `tar` file

##### Export the image

##### Import the image


## Dockerfile


> **!** For Ubuntu/Debian, it is better to create a base system image with upgraded package `apt-get update && apt-get upgrade -y`


### Dockerfile example

```
# DOCKER-VERSION 1.6.0
# Erlang docker image

FROM ubuntubase:v1
MAINTAINER Jun HU <junhufr@gmail.com>


# add the erlang repo and key
RUN echo "deb http://packages.erlang-solutions.com/ubuntu trusty contrib" >> /etc/apt/sources.list
RUN DEBIAN_FRONTEND=noninteractive apt-get install wget -y
RUN wget http://packages.erlang-solutions.com/ubuntu/erlang_solutions.asc
RUN apt-key add erlang_solutions.asc

RUN apt-get update
RUN DEBIAN_FRONTEND=noninteractive apt-get install -y \
    erlang \
    rebar

```


### Build image from Dockerfile

``` bash
    > docker build -t "MyDockerImageName:tag" -f MyDockerfile # by default, the file name is Dockerfile
```


## Coordination among docker containers

### Use same data volume container as common data layer

#### create container

```bash
$ docker create -v /home/docker:/docker --name docker ubuntu:14.04.2
9aa88c08f319cd1e4515c3c46b0de7cc9aa75e878357b1e96f91e2c773029f03
$  docker run --rm --volumes-from docker ubuntu ls -la /docker
```




## Management

### Pull the images from Docker public repository


### Build private local repository

#### Ref
1. [Ref1](https://www.vultr.com/docs/setup-your-own-docker-registry-on-coreos)



## References 

1. Docker without docker [slide](https://chimeracoder.github.io/docker-without-docker/#1)
2. Docker on arm processor [tutorial](https://github.com/umiddelb/armhf/wiki/Installing,-running,-using-docker-on-armhf-%28ARMv7%29-devices)

-----------------------
_______________________

## Definitions

#### Container



#### Image

Docker images are the basis of containers. 


#### Data volume

A data volume is a specially-designated directory within one or more containers that bypasses the Union File System. Data volumes provide several useful features for persistent or shared data:

- Volumes are initialized when a container is created. If the container's base image contains data at the specified mount point, that data is copied into the new volume.
- Data volumes can be shared and reused among containers.
- Changes to a data volume are made directly.
- Changes to a data volume will not be included when you update an image.
- Data volumes persist even if the container itself is deleted.

Data volumes are designed to persist data, independent of the container's life cycle. Docker therefore never automatically delete volumes when you remove a container, nor will it "garbage collect" volumes that are no longer referenced by a container.

## Preparation

The official tutorial can be found [here](https://docs.docker.com/installation/ubuntulinux/#optional-configurations-for-docker-on-ubuntu)

#### Install docker


#### Create docker group


```bash
    > sudo usermod -aG docker yourusername
```

#### Adjust memory and swap accounting

Set **GRUB_CMDLINE_LINUX** in **/etc/default/grub**

```
   GRUB_CMDLINE_LINUX="cgroup_enable=memory swapaccount=1"
```

Update Grub and reboot

```bash
    > sudo update-grub && sudo reboot
```

#### Upgrade and reboot docker

```bash
    > wget -N https://get.docker.com/ | sh
    > sudo restart network-manager $ sudo restart docker
````




