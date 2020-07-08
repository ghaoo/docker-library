FROM php:7.1-fpm
MAINTAINER GuHao <378999587@qq.com>

ENV TZ=Asia/Shanghai

#COPY ./ustc.list /etc/apt/sources.list
#RUN sed -i 's/deb.debian.org/mirrors.ustc.edu.cn/g' /etc/apt/sources.list
RUN sed -i 's/deb.debian.org/mirrors.aliyun.com/g' /etc/apt/sources.list && sed -i 's/security.debian.org/mirrors.aliyun.com/g' /etc/apt/sources.list

ADD ./pecl /usr/local/etc/php/pecl

RUN apt-get update -qq && \
    apt-get install --no-install-recommends -y \
        git \
        zip \
        libxml2-dev \
        libfreetype6-dev \
        libpng-dev \
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

RUN docker-php-ext-install -j$(nproc) iconv \
  && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
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
#  && pecl install redis \
#  && pecl install xdebug \
#  && pecl install mcrypt \
#  && pecl install swoole \
#  && docker-php-ext-enable redis mcrypt xdebug swoole \
  && rm -rf /tmp/pear

#ADD ./laravel.ini /usr/local/etc/php/conf.d
#ADD ./laravel.pool.conf /usr/local/etc/php-fpm.d/

ADD ./shopnc/shopnc.so /usr/local/lib/php/extensions/no-debug-non-zts-20160303/
ADD ./shopnc/docker-php-ext-shopnc.ini /usr/local/etc/php/conf.d/

RUN cd /usr/local/etc/php \
    && mv php.ini-development php.ini

WORKDIR /data/www

CMD ["php-fpm"]

EXPOSE 9000
