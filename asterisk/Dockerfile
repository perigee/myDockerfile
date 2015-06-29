# DOCKER-VERSION 1.6.0
# Asterisk 13 Docker images

FROM ubuntubase:v1 # based on ubuntu:14.04.2 with upgraded system
MAINTAINER Jun HU <junhufr@gmail.com>


# compile pj-project

# Dependencies
RUN apt-get update
RUN DEBIAN_FRONTEND=noninteractive apt-get install -y \
    build-essential \
    git \
    subversion \
    wget \
    libsrtp-dev \
    libjansson-dev \
    libncurses-dev \
    uuid-dev \
    libgnutls-dev \
    libneon27-gnutls-dev \
    libsnmp-dev \
    libsqlite3-dev \
    sqlite3 \
    libspeex-dev \
    libgsm1-dev \
    nginx

RUN mkdir /home/src
WORKDIR /home/src


RUN git clone https://github.com/asterisk/pjproject.git
RUN svn checkout http://svn.asterisk.org/svn/asterisk/branches/13 asterisk-13


WORKDIR	/home/src/pjproject
RUN git checkout tags/pjproject-2.3
RUN ./configure --prefix=/usr --enable-shared --disable-sound \
    			      --disable-resample --disable-video \
			      --disable-opencore-amr    
RUN make dep && make && make install && ldconfig

WORKDIR /home/src/asterisk-13
RUN ./configure --with-crypto --with-ssl --with-srtp
RUN ./contrib/scripts/install_prereq install
RUN ./contrib/scripts/install_prereq install-unpackaged
RUN make && make install
RUN make samples


## define asterisk UDP call ports 
RUN sed -i "s/rtpstart=10000/rtpstart=16384/g" /etc/asterisk/rtp.conf
RUN sed -i "s/rtpend=20000/rtpend=16394/g" /etc/asterisk/rtp.conf

## copy the configurations files




## Install demo package
WORKDIR /usr/share/nginx/html
RUN svn checkout http://sipml5.googlecode.com/svn/trunk/ phone

RUN mkdir /etc/asterisk/keys


EXPOSE 80 5060 16384-16394 # expose a range of 10 ports for 10 simultaneously calls

CMD ["/bin/asterisk"]
CMD ["/usr/sbin/nginx"]