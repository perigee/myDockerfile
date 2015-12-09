###############################
## DOCKER-VERSION 1.8.2
## Erlang docker image
###############################

FROM ubuntu:latest
MAINTAINER Jun HU <junhufr@gmail.com>

RUN DEBIAN_FRONTEND=noninteractive apt-get update && apt-get install -y curl

## add the erlang repe,key and install
RUN curl -O http://packages.erlang-solutions.com/erlang-solutions_1.0_all.deb \
    && sudo dpkg -i erlang-solutions_1.0_all.deb
RUN DEBIAN_FRONTEND=noninteractive apt-get update \
    && apt-get install -y openssl emacs24-nox \
       erlang-nox rebar3 \
    && apt-get autoremove

WORKDIR /home/erlang
