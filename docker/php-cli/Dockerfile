FROM php:7.3-cli-alpine

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
    openssh \
    && rm /var/cache/apk/*

RUN pecl install xdebug && \
    docker-php-ext-configure gd \
        --with-freetype-dir=/usr/include/ \
        --with-png-dir=/usr/include/ \
        --with-jpeg-dir=/usr/include/ && \
    docker-php-ext-install gd

RUN docker-php-ext-install pdo_mysql intl && \
    docker-php-ext-configure intl

COPY conf/*.ini /usr/local/etc/php/conf.d/

WORKDIR '/app'
CMD ["-"]
