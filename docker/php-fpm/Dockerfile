FROM php:7.3-fpm-alpine
MAINTAINER Patrick Mosch <info@xuad.net>

ENV TERM=xterm \
    TZ=Europe/Berlin \
    PHP_XDEBUG_REMOTE_HOST=docker.for.win.localhost \
    PHP_XDEBUG_IDE_KEY=docker-xdebug \
    PHP_XDEBUG_REMOTE_PORT=9001 \
    PHP_XDEBUG_REMOTE_ENABLE=1

RUN apk update && apk add --no-cache \
    bash \
    git \
    mysql-client \
    curl \
    mc \
    libintl \
    icu \
    icu-dev \
    libxml2-dev \
    libmcrypt \
    libmcrypt-dev \
    freetype \
    freetype-dev \
    libpng \
    libpng-dev \
    libjpeg-turbo \
    libjpeg-turbo-dev \
    g++ \
    make \
    autoconf \
    openssh

RUN docker-php-ext-configure gd \
        --with-freetype-dir=/usr/include/ \
        --with-png-dir=/usr/include/ \
        --with-jpeg-dir=/usr/include/ && \
    docker-php-ext-install gd

RUN pecl install xdebug && \
    docker-php-ext-install pdo_mysql intl && \
    docker-php-ext-configure intl

# enable logging - https://ypereirareis.github.io/blog/2017/02/20/php-fpm-cli-error-log/
RUN set -x \
    && sed -i '/^;php_flag\[display_errors\]/cphp_flag[display_errors] = off' "/usr/local/etc/php-fpm.d/www.conf" \
    && sed -i '/^;access.log/caccess.log = /var/log/php/fpm-access.log' "/usr/local/etc/php-fpm.d/www.conf" \
    && sed -i '/^;catch_workers_output/ccatch_workers_output = yes' "/usr/local/etc/php-fpm.d/www.conf" \
    && sed -i '/^;php_admin_value\[error_log\]/cphp_admin_value[error_log] = /var/log/php/fpm-error.log' "/usr/local/etc/php-fpm.d/www.conf" \
    && sed -i '/^;php_admin_flag\[log_errors\]/cphp_admin_flag[log_errors] = on' "/usr/local/etc/php-fpm.d/www.conf"

COPY conf/*.ini /usr/local/etc/php/conf.d/

WORKDIR /app
EXPOSE 9000
CMD ["php-fpm"]
