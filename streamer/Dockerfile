# DOCKER-VERSION 1.6.0
#########################################
# Dockerfile to build Nginx+RTMP server
#########################################


FROM ubuntubase:v1
MAINTAINER Jun HU <jh@2klic.com>

ENV nginx  nginx-1.8.0
ENV ffmpeg ffmpeg-2.6.2 

# Prerequisites

RUN apt-get update
RUN DEBIAN_FRONTEND=noninteractive apt-get install -y \
    build-essential \
    wget \
    unzip \
    libx264-dev \
    libvpx-dev \
    libpcre3 \
    libpcre3-dev \
    libssl-dev 

RUN mkdir /home/src
WORKDIR /home/src
RUN wget https://github.com/arut/nginx-rtmp-module/archive/master.zip && \
    unzip master.zip && rm master.zip

RUN wget http://nginx.org/download/$nginx.tar.gz && \
    tar xvzf $nginx.tar.gz && mv $nginx/ nginx/ 

RUN wget http://ffmpeg.org/releases/$ffmpeg.tar.bz2 && \
    tar -xf $ffmpeg.tar.bz2 && mv $ffmpeg/ ffmpeg/


# Compile ffmpeg

WORKDIR /home/src/ffmpeg
RUN ./configure --enable-gpl --enable-libx264 --enable-libvpx --disable-yasm && \
    make && make install

# Compile nginx with rtmp

WORKDIR /home/src/nginx
RUN ./configure --add-module=../nginx-rtmp-module-master && \
    make && make install

# Copy the configuration file into container image
ADD nginx.conf /usr/local/nginx/conf/nginx.conf 

EXPOSE 554 80 1935

CMD ["/bin/bash"]
CMD ["/usr/local/nginx/sbin/nginx"]