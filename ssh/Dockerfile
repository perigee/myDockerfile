FROM ubuntu:latest
MAINTAINER Jun HU <junhufr@gmail.com>

RUN apt-get update
RUN DEBIAN_FRONTEND=noninteractive apt-get install -y \
    openssh-server 



EXPOSE 22
CMD ["/usr/sbin/sshd","-D"]
