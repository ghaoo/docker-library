FROM nginx:alpine

MAINTAINER GuHao <378999587@qq.com>

ENV TZ "Asia/Shanghai"

#COPY nginx.conf /etc/nginx/nginx.conf
COPY conf.d /etc/nginx/conf.d

#VOLUME ["/data/www","/data/www"]
#VOLUME ["./logs","/var/log"]

EXPOSE 80 443

CMD ["nginx", "-g", "daemon off;"]
