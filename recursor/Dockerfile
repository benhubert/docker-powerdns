FROM alpine:latest

RUN sed -i -e 's#alpine/v[0-9.]*/#alpine/edge/#g' /etc/apk/repositories \
    && apk --update --no-cache add \
        tini \
        py2-pip \
        pdns-recursor \
    && pip install envtpl

COPY recursor.conf.tpl /etc/pdns/recursor.conf.tpl
COPY start.sh /

ENV PDNS_RECURSOR_LOCAL_ADDRESS=0.0.0.0
ENV PDNS_RECURSOR_DISABLE_SYSLOG=yes

ENTRYPOINT [ "tini", "-vv", "/start.sh" ]
CMD [ "/usr/sbin/pdns_recursor", "--daemon=no" ]
