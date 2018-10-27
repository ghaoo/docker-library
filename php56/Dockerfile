FROM php:5.6-fpm-alpine
MAINTAINER GuHao <378999587@qq.com>

ENV TZ=Asia/Shanghai

#更改国内镜像源
RUN echo -e "https://mirrors.ustc.edu.cn/alpine/v3.7/main\nhttps://mirrors.ustc.edu.cn/alpine/v3.7/community\n" > /etc/apk/repositories

#安装拓展
RUN apk update && apk add --no-cache \
            $PHPIZE_DEPS \
	    freetype \
	    libjpeg-turbo \
	    freetype-dev \
	    libjpeg-turbo-dev \
        libpng \
        libpng-dev \
        libxml2 \
        libxml2-dev \
        libxslt \
        libxslt-dev \
        icu \
        icu-dev \
        libmcrypt \
        libmcrypt-dev \
    && pecl install xdebug-2.5.0 \
    && docker-php-ext-enable xdebug \
	&& pecl install redis \
	&& docker-php-ext-enable redis

RUN  docker-php-ext-configure gd \
	    --with-gd \
	    --with-freetype-dir=/usr \
	    --with-png-dir=/usr \
	    --with-jpeg-dir=/usr && \
	NPROC=$(grep -c ^processor /proc/cpuinfo 2>/dev/null || 1) \
	&& docker-php-ext-install -j${NPROC} gd \
	&& docker-php-ext-install mysqli \
	&& docker-php-ext-install mysql \
	&& docker-php-ext-install pdo_mysql \
	&& docker-php-ext-install zip \
	&& docker-php-ext-install mcrypt

ADD ./shopnc/shopnc.so /usr/local/lib/php/extensions/no-debug-non-zts-20131226/

RUN cd /usr/local/include \
    && curl -LO http://downloads.zend.com/guard/7.0.0/zend-loader-php5.6-linux-x86_64.tar.gz \
    && tar zxvf zend-loader-php5.6-linux-x86_64.tar.gz \
    && cd zend-loader-php5.6-linux-x86_64 \
    && mv ZendGuardLoader.so /usr/local/lib/php/extensions/no-debug-non-zts-20131226/ \
    && cd .. && rm -rf zend-loader-php5.6*

ADD ./shopnc/shopnc.ini /usr/local/etc/php/conf.d/

RUN cd /usr/local/etc/php \
    && mv php.ini-development php.ini

WORKDIR /data/www

CMD ["php-fpm"]

EXPOSE 9000
