###############################
## DOCKER-VERSION 1.8.2
## Erlang docker image
###############################

FROM ubuntu:latest
MAINTAINER Jun HU <junhufr@gmail.com>

## essential pkgs
RUN DEBIAN_FRONTEND=noninteractive apt-get update && apt-get install -y openssl emacs24-nox curl

## add the erlang repe,key and install
RUN echo "deb http://packages.erlang-solutions.com/ubuntu trusty contrib" >> /etc/apt/sources.list
RUN curl -O http://packages.erlang-solutions.com/ubuntu/erlang_solutions.asc | apt-key add -
RUN DEBIAN_FRONTEND=noninteractive apt-get update && apt-get install -y erlang-nox rebar && apt-get autoclean
