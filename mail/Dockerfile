FROM ubuntu:latest

RUN apt-get update && apt-get install -y postfix

COPY configuration/main.cf /etc/postfix/main.cf

RUN /etc/init.d/postfix restart
