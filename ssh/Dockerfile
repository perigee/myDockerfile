FROM ubuntu:latest
MAINTAINER Jun HU <junhufr@gmail.com>

RUN apt-get update
RUN DEBIAN_FRONTEND=noninteractive apt-get install -y \
    openssh-server \
    sudo

RUN useradd -m docker && echo "docker:docker" | chpasswd && adduser docker sudo

RUN mkdir /home/docker/.ssh
ADD keys/public.pem /home/docker/.ssh/authorized_keys
RUN chmod 700 /home/docker/.ssh
RUN chmod 600 /home/docker/.ssh/authorized_keys


USER docker
EXPOSE 22
CMD ["/usr/sbin/sshd","-e", "-D"]
