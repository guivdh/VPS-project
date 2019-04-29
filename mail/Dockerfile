FROM ubuntu:latest

RUN apt-get update && apt-get install -y postfix

COPY configuration/main.cf /etc/postfix/main.cf

RUN postmap /etc/postfix/virtual
RUN /etc/init.d/postfix restart
