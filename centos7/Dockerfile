FROM centos:centos7

MAINTAINER jun HU


RUN yum update -y
RUN yum install -y sudo openssh-server emacs-nox openssh-clients
RUN mkdir /var/run/sshd

RUN sed -ri 's/UsePAM yes/#UsePAM yes/g' /etc/ssh/sshd_config
RUN sed -ri 's/#UsePAM no/UsePAM no/g' /etc/ssh/sshd_config

RUN ssh-keygen -t rsa -f /etc/ssh/ssh_host_rsa_key
RUN ssh-keygen -t dsa -f /etc/ssh/ssh_host_dsa_key

RUN useradd -m docker -G wheel
RUN usermod -s /bin/bash docker


RUN mkdir /home/docker/.ssh
ADD keys/docker.pub  /home/docker/.ssh/authorized_keys
RUN chmod 700 /home/docker/.ssh
RUN chmod 600 /home/docker/.ssh/authorized_keys

RUN chown -R docker:docker /home/docker

EXPOSE 22
CMD ["/usr/sbin/sshd", "-D"]
