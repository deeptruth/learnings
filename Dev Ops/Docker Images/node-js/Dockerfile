FROM ubuntu:latest

Maintainer Joshua Clifford Reyes <reyesjoshuaclifford@gmail.com>

RUN apt-get update -y
RUN apt-get install curl -y
RUN cd ~
RUN curl -sL https://deb.nodesource.com/setup_6.x -o nodesource_setup.sh
RUN bash nodesource_setup.sh
RUN apt-get install nodejs -y
RUN apt-get install build-essential -y
RUN mkdir /var/www
RUN mkdir /var/lib/mongodb

EXPOSE 80
