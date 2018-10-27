FROM redis:alpine
MAINTAINER GuHao <378999587@qq.com>

ENV TZ "Asia/Shanghai"

COPY redis.conf /etc/redis/redis.conf
#CMD [ "chmod" "-R" "777" "/var/log" ]
CMD ["redis-server", "/etc/redis/redis.conf"]