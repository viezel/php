FROM ubuntu:20.04

MAINTAINER Mads Møller

ENV DEBIAN_FRONTEND=noninteractive
ENV TZ=UTC

RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

RUN apt-get update \
    && apt-get upgrade -yq \
    && apt-get install -yq --no-install-recommends \
       apt-utils apt-transport-https ca-certificates \
       curl git unzip software-properties-common \
    && LC_ALL=C.UTF-8 add-apt-repository ppa:ondrej/php \
    && apt-get remove --purge -y software-properties-common \
    && apt-get update \
    && apt-get install -y php8.0 php8.0-fpm php8.0-dev \
       php8.0-gd php8.0-curl php8.0-bz2 php8.0-bcmath \
       php8.0-imap php8.0-mysql php8.0-mbstring \
       php8.0-xml php8.0-zip php8.0-soap \
       php8.0-intl php8.0-readline \
       php8.0-msgpack php8.0-igbinary php8.0-ldap \
       php8.0-redis \
    && php -r "readfile('http://getcomposer.org/installer');" | php -- --install-dir=/usr/bin/ --filename=composer \
    && apt-get -y autoremove \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

RUN mkdir -p /run/php && chown www-data:www-data /run/php

COPY conf /etc/php/8.0/fpm/pool.d/
COPY php.ini /etc/php/8.0/fpm/php.ini

RUN mkdir -p /var/www/html
WORKDIR /var/www/html

EXPOSE 9000
CMD ["php-fpm8.0"]
