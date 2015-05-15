# DOCKER-VERSION 1.6.0
#########################################
# Dockerfile to build redis
#########################################


FROM ubuntubase:v1
MAINTAINER Jun HU <jh@2klic.com>


RUN apt-get update
RUN DEBIAN_FRONTEND=noninteractive apt-get install -y \
    build-essential \
    wget \
    redis-server


CMD ["/bin/bash"] 
CMD ["redis-server"]