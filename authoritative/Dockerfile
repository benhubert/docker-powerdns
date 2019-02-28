FROM alpine:latest

RUN sed -i -e 's#alpine/v[0-9.]*/#alpine/edge/#g' /etc/apk/repositories \
    && apk --update --no-cache add \
        tini \
        py2-pip \
        pdns \
        pdns-backend-bind \
        pdns-backend-pgsql \
        pdns-backend-ldap \
        pdns-backend-mysql \
        pdns-backend-sqlite3 \
        pdns-backend-pipe \
    && pip install envtpl

COPY pdns.conf.tpl /etc/pdns/pdns.conf.tpl
COPY start.sh /

ENV PDNS_AUTH_LOCAL_ADDRESS=0.0.0.0
ENV PDNS_AUTH_DISABLE_SYSLOG=yes

ENTRYPOINT [ "tini", "-vv", "/start.sh" ]
CMD [ "/usr/sbin/pdns_server", "--daemon=no" ]
