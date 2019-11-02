FROM php:7.3-cli-alpine

ENV TERM=xterm \
    TZ=Europe/Berlin

RUN echo http://nl.alpinelinux.org/alpine/edge/testing >> /etc/apk/repositories && \
    apk update && apk add  --no-cache \
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

RUN docker-php-ext-configure gd \
        --with-freetype-dir=/usr/include/ \
        --with-png-dir=/usr/include/ \
        --with-jpeg-dir=/usr/include/ && \
    docker-php-ext-install gd

RUN docker-php-ext-install pdo_mysql intl && \
    docker-php-ext-configure intl

COPY conf/*.ini /usr/local/etc/php/conf.d/

WORKDIR '/app'
CMD ["-"]
#ENTRYPOINT ["composer", "--ansi"]
#ENTRYPOINT ["php", "--ansi"]
