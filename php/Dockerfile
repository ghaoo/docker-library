FROM php:fpm
MAINTAINER GuHao <378999587@qq.com>

ENV TZ=Asia/Shanghai

#COPY ./ustc.list /etc/apt/sources.list
#RUN sed -i 's/deb.debian.org/mirrors.ustc.edu.cn/g' /etc/apt/sources.list
RUN sed -i 's/deb.debian.org/mirrors.aliyun.com/g' /etc/apt/sources.list && sed -i 's/security.debian.org/mirrors.aliyun.com/g' /etc/apt/sources.list

ADD ./pecl /usr/local/etc/php/pecl

RUN apt-get update && apt-get install -y \
        git \
        zip \
        libxml2-dev \
        libfreetype6-dev \
        libjpeg62-turbo-dev \
        libpng-dev \
        libonig-dev \
        libjpeg-dev \
        libz-dev \
        libssl-dev \
        libnghttp2-dev \
        libpcre3-dev \
        libsqlite3-dev \
        libmcrypt-dev \
        libcurl3-dev \
        libzip-dev \
    && apt-get clean -y \
    && apt-get autoremove -y


RUN docker-php-ext-configure gd --with-freetype --with-jpeg \
  && docker-php-ext-install -j$(nproc) gd \
  && docker-php-ext-install \
    mbstring \
    mysqli \
    pdo \
    pdo_mysql \
    pcntl \
    tokenizer \
    xml \
    zip \
  && pecl install redis \
  && pecl install xdebug \
  && pecl install mcrypt \
  && docker-php-ext-enable redis mcrypt xdebug \
  && git clone https://github.com/swoole/swoole-src.git \
  && cd swoole-src \
  && /usr/local/bin/phpize && ./configure && make && make install \
  && cd .. && rm -rf swoole-src \
  && docker-php-ext-enable swoole \
  && rm -rf /tmp/pear

RUN cd /usr/local/etc/php \
    && mv php.ini-development php.ini

WORKDIR /data/www

CMD ["php-fpm"]

EXPOSE 9000
