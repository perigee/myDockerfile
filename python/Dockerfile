# DOCKER-VERSION 1.6.0
#########################################
# Dockerfile to build Python development 
# environment with pip installed 
#########################################


FROM ubuntubase:v1
MAINTAINER Jun HU <jh@2klic.com>


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
RUN pip install -U pip
RUN pip install virtualenv

