FROM ubuntu:latest

RUN apt-get update && apt-get install -y postfix

COPY configuration/main.cf /etc/postfix/

EXPOSE 25

CMD service postfix start
