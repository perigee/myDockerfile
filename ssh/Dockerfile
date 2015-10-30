FROM ubuntu:14.04
MAINTAINER Jun HU <junhufr@gmail.com>

RUN apt-get update
RUN DEBIAN_FRONTEND=noninteractive apt-get install -y \
    openssh-server \
    emacs24-nox \
    sudo

RUN mkdir /var/run/sshd

RUN useradd -m docker && echo "docker:docker" | chpasswd && adduser docker sudo


RUN mkdir /home/docker/.ssh
ADD keys/public.pem /home/docker/.ssh/authorized_keys
ADD ssh/my_init.sh /sbin/my_init.sh
RUN chown docker:docker /sbin/my_init.sh
RUN chmod +x /sbin/my_init.sh
RUN chmod 700 /home/docker/.ssh
RUN chmod 600 /home/docker/.ssh/authorized_keys

RUN sed -i 's/PermitRootLogin without-password/PermitRootLogin yes/' /etc/ssh/sshd_config
# SSH login fix. Otherwise user is kicked off after login
RUN sed 's@session\s*required\s*pam_loginuid.so@session optional pam_loginuid.so@g' -i /etc/pam.d/sshd


ENV NOTVISIBLE "in users profile"
RUN echo "export VISIBLE=now" >> /etc/profile


#USER docker
EXPOSE 22
CMD ["/usr/sbin/sshd", "-D"]
