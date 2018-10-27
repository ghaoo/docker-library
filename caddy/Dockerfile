FROM golang:alpine
MAINTAINER GuHao <378999587@qq.com>

ENV TZ=Asia/Shanghai

RUN sed -i 's/dl-cdn.alpinelinux.org/mirrors.aliyun.com/g' /etc/apk/repositories

RUN apk add --no-cache tini curl git ca-certificates \
    && apk add --no-cache --virtual .build_tools wget tar bash \
    && curl https://getcaddy.com \
      | bash -s personal docker,http.cors,http.git,http.ipfilter,http.jwt,http.login,http.upload \
    && apk del --purge .build_tools \
    && rm -rf \
      /etc/ssl \
      /usr/share/doc \
      /usr/share/man \
      /tmp/* \
      /var/cache/apk/*

COPY ./Caddyfile /etc/Caddyfile

EXPOSE 80 443

ENTRYPOINT ["/sbin/tini"]

CMD ["caddy", "-quic", "--conf", "/etc/Caddyfile"]
