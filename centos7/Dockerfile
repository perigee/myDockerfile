FROM centos:centos7

MAINTAINER jun HU


RUN yum update -y
RUN yum install -y sudo openssh-server emacs-nox


ADD public.pem /tmp/public.pem

RUN useradd admin -G wheel
RUN su - admin
RUN mkdir .ssh
RUN chmod 700 .ssh
RUN cat /tmp/public.pem > .ssh/authorized_keys
RUN chmod 600 .ssh/authorized_keys


EXPOSE 22
CMD ["/usr/sbin/sshd", "-e", "-D"]
