FROM centos:centos7

MAINTAINER jun HU

# generate locale and set timezone
RUN localedef --no-archive -i en_US -f UTF-8 en_US.UTF-8
RUN rm -f /etc/localtime && ln -s /usr/share/zoneinfo/UTC /etc/localtime
RUN echo 'ZONE="UTC"' > /etc/sysconfig/clock && echo 'UTC=True' >> /etc/sysconfig/clock


RUN yum update -y
RUN yum install -y sudo openssh-server emacs-nox openssh-clients
RUN mkdir /var/run/sshd

RUN sed -ri 's/UsePAM yes/#UsePAM yes/g' /etc/ssh/sshd_config
RUN sed -ri 's/#UsePAM no/UsePAM no/g' /etc/ssh/sshd_config
RUN sed -ri 's/PasswordAuthentication yes/PasswordAuthentication no/g' /etc/ssh/sshd_config


RUN sed -i 's/#PermitRootLogin without-password/PermitRootLogin yes/' /etc/ssh/sshd_config
# SSH login fix. Otherwise user is kicked off after login
RUN sed 's@session\s*required\s*pam_loginuid.so@session optional pam_loginuid.so@g' -i /etc/pam.d/sshd

RUN ssh-keygen -t rsa -f /etc/ssh/ssh_host_rsa_key
RUN ssh-keygen -t dsa -f /etc/ssh/ssh_host_dsa_key


# setup default user
RUN useradd docker -G wheel -s /bin/bash -m
RUN echo 'docker:docker' | chpasswd
RUN echo '%wheel ALL=(ALL) ALL' >> /etc/sudoers
#RUN su - docker -c "byobu-launcher-install"


RUN mkdir /home/docker/.ssh
ADD keys/docker.pub  /home/docker/.ssh/authorized_keys
RUN chmod 700 /home/docker/.ssh
RUN chmod 600 /home/docker/.ssh/authorized_keys

RUN mkdir /etc/ssh/docker
ADD keys/docker.pub  /etc/ssh/docker/authorized_keys
RUN sed -i 's/AuthorizedKeysFile      .ssh\/authorized_keys/AuthorizedKeysFile      \/etc\/ssh\/docker\/authorized_keys/' /etc/ssh/sshd_config


RUN chmod 755 /etc/ssh/docker
RUN chmod 644 /etc/ssh/docker/authorized_keys

RUN chown -R docker:docker /home/docker
RUN chown -R docker:docker /etc/ssh/docker


EXPOSE 22
CMD ["/usr/sbin/sshd", "-D"]
