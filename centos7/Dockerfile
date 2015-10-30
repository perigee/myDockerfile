FROM centos:centos7

MAINTAINER jun HU


RUN yum update -y
RUN yum install -y sudo openssh-server emacs-nox openssh-client
RUN mkdir /var/run/sshd

RUN sed -ri 's/UsePAM yes/#UsePAM yes/g' /etc/ssh/sshd_config
RUN sed -ri 's/#UsePAM no/UsePAM no/g' /etc/ssh/sshd_config

RUN useradd admin -G wheel
RUN usermod -s /bin/bash admin
ENV HOME /home/admin

ADD public.pem /tmp/public.pem
RUN su - admin
RUN mkdir .ssh
RUN chmod 700 .ssh
RUN cat /tmp/public.pem > .ssh/authorized_keys
RUN chmod 600 .ssh/authorized_keys


EXPOSE 22
CMD ["/usr/sbin/sshd", "-D"]
