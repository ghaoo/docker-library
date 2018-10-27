FROM php:fpm
MAINTAINER GuHao <378999587@qq.com>

ENV TZ=Asia/Shanghai

COPY ./sources.list /etc/apt/sources.list

RUN apt-get update && apt-get install -y --no-install-recommends\
        libcurl4-openssl-dev \
        libjpeg62-turbo-dev \
        libfreetype6-dev \
        libsqlite3-dev \
        libmcrypt-dev \
        libcurl3-dev \
        libxml2-dev \
        libpng-dev \
        libbz2-dev \
        libssl-dev \
        libtool \
    && docker-php-ext-install -j$(nproc) iconv \
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install -j$(nproc) gd \
    && docker-php-ext-install \
        curl \
        mbstring \
        mysqli \
        pdo \
        pdo_mysql \
        pdo_sqlite \
        pcntl \
        tokenizer \
        xml \
        zip \
    && pecl install -o -f redis \
    && pecl install mongodb \
    && pecl install xdebug \
    && pecl install swoole \
    && docker-php-ext-enable redis mongodb xdebug swoole \
    && rm -rf /tmp/pear

#ADD ./laravel.ini /usr/local/etc/php/conf.d
#ADD ./laravel.pool.conf /usr/local/etc/php-fpm.d/

ADD ./shopnc/shopnc.so /usr/local/lib/php/extensions/no-debug-non-zts-20170718/
ADD ./shopnc/shopnc.ini /usr/local/etc/php/conf.d/

#RUN cd /usr/local/etc/php \
#    && mv php.ini-development php.ini

WORKDIR /data/www

CMD ["php-fpm"]

EXPOSE 9000
