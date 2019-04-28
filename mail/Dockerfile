FROM ubuntu:16.04

RUN apt-get update && apt-get install -y libsasl2-modules postfix && apt-get -y install rsyslog; \
rm -rf /var/lib/apt/lists/*;

CMD touch /dev/xconsole && chgrp syslog /dev/xconsole && chmod 664 /dev/xconsole

# RUN service rsyslog restart

RUN echo "[smtp.gmail.com]:587 email@gmail.com:password" > /etc/postfix/sasl_passwd

RUN postmap /etc/postfix/sasl_passwd

RUN sed -i '/relayhost*/c\relayhost = [smtp.gmail.com]:587' /etc/postfix/main.cf

RUN sed -i '/smtp_sasl_auth_enable*/c\smtp_sasl_auth_enable = yes' /etc/postfix/main.cf

RUN sed -i '/smtp_sasl_security_options*/c\smtp_sasl_security_options = noanonymous' /etc/postfix/main.cf

RUN sed -i '/smtp_sasl_password_maps*/c\smtp_sasl_password_maps = hash:/etc/postfix/sasl_passwd' /etc/postfix/main.cf

RUN sed -i '/smtp_tls_security_level*/c\smtp_tls_security_level = encrypt' /etc/postfix/main.cf

RUN sed -i '/smtp_tls_CAfile*/c\smtp_tls_CAfile = /etc/ssl/certs/ca-certificates.crt' /etc/postfix/main.cf

# CMD /etc/init.d/postfix restart && tail -f /var/log/syslog

EXPOSE 25

# CMD service rsyslog start && service postfix start && tail -f /var/log/mail.log
CMD touch /dev/xconsole && chgrp syslog /dev/xconsole && chmod 664 /dev/xconsole && service rsyslog start && service postfix start && tail -f /var/log/mail.log
