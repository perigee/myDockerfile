# DOCKER-VERSION 1.6.0
# Asterisk 13 Docker images

FROM ubuntubase:v1 # based on ubuntu:14.04.2 with upgraded system
MAINTAINER Jun HU <junhufr@gmail.com>


# compile pj-project

# Dependencies
RUN apt-get update
RUN DEBIAN_FRONTEND=noninteractive apt-get install -y \
    build-essential git subversion wget \

RUN mkdir /home/src
WORKDIR /home/src
RUN git clone https://github.com/asterisk/pjproject.git
WORKDIR	/home/src/pjproject
RUN git checkout tags/pjproject-2.3
RUN ./configure --prefix=/usr --enable-shared --disable-sound \
    			      --disable-resample --disable-video \
			      --disable-opencore-amr    
RUN make dep && make && make install && ldconfig




EXPOSE 80

CMD ["asterisk"]
CMD ["asterisk -r"]