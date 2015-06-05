# DOCKER-VERSION 1.6.0
#########################################
# Dockerfile to build Python2.7 development 
# environment with pip installed 
#########################################


FROM ubuntubase:v1
MAINTAINER Jun HU <jh@2klic.com>


ENV libsodium libsodium-1.0.3
ENV zeromq zeromq-4.1.1


RUN apt-get update
RUN DEBIAN_FRONTEND=noninteractive apt-get install -y \
    build-essential \
    wget \
    git \ 
    python2.7 \
    python-dev


RUN mkdir /home/src
WORKDIR /home/src
RUN wget https://bootstrap.pypa.io/get-pip.py
RUN python get-pip.py
RUN rm get-pip.py
RUN pip install -U pip setuptools
RUN pip install virtualenv

################################
## GET zeromq ready 
################################

RUN DEBIAN_FRONTEND=noninteractive apt-get install -y \
    libtool \
    pkg-config \
    autoconf \
    automake \
    uuid-dev 

RUN wget https://download.libsodium.org/libsodium/releases/$libsodium.tar.gz
RUN wget http://download.zeromq.org/$zeromq.tar.gz

RUN tar zvxf $libsodium.tar.gz 
WORKDIR /home/src/$libsodium 
RUN ./configure
RUN make && make check && make install


WORKDIR /home/src/$zeromq
RUN ./configure
RUN make && make install

## ADD working dir into the container


## expose the ports for zmq communciation
EXPOSE 5556 5557 

CMD ['cd','/home/src']