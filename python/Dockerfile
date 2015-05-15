# DOCKER-VERSION 1.6.0
#########################################
# Dockerfile to build Python2.7 development 
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


WORKDIR /home
RUN wget https://bootstrap.pypa.io/get-pip.py
RUN python get-pip.py
RUN rm get-pip.py
RUN pip install -U pip setuptools
RUN pip install virtualenv

