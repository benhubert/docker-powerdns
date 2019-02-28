FROM alpine:latest

ARG PDNS_AUTH_VERSION=4.1.6

RUN sed -i -e 's#alpine/v[0-9.]*/#alpine/edge/#g' /etc/apk/repositories \
    && apk --update --no-cache add \
        tini \
        py2-pip \
        pdns~=${PDNS_AUTH_VERSION} \
        pdns-backend-bind~=${PDNS_AUTH_VERSION} \
        pdns-backend-pgsql~=${PDNS_AUTH_VERSION} \
        pdns-backend-ldap~=${PDNS_AUTH_VERSION} \
        pdns-backend-mysql~=${PDNS_AUTH_VERSION} \
        pdns-backend-sqlite3~=${PDNS_AUTH_VERSION} \
        pdns-backend-pipe~=${PDNS_AUTH_VERSION} \
    && pip install envtpl

COPY pdns.conf.tpl /etc/pdns/pdns.conf.tpl
COPY start.sh /

ENV PDNS_AUTH_LOCAL_ADDRESS=0.0.0.0
ENV PDNS_AUTH_DISABLE_SYSLOG=yes

ENTRYPOINT [ "tini", "-vv", "/start.sh" ]
CMD [ "/usr/sbin/pdns_server", "--daemon=no" ]
