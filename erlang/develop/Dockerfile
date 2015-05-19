# DOCKER-VERSION 1.6.0
# Erlang docker image

FROM ubuntubase:v1
MAINTAINER Jun HU <junhufr@gmail.com>


# add the erlang repo and key
RUN echo "deb http://packages.erlang-solutions.com/ubuntu trusty contrib" >> /etc/apt/sources.list
RUN DEBIAN_FRONTEND=noninteractive apt-get install wget -y
RUN wget http://packages.erlang-solutions.com/ubuntu/erlang_solutions.asc
RUN apt-key add erlang_solutions.asc

RUN apt-get update
RUN DEBIAN_FRONTEND=noninteractive apt-get install -y \
    erlang-nox \
    rebar