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
    && apt-get install -y php7.4 php7.4-fpm php7.4-dev \
       php7.4-gd php7.4-curl php7.4-bz2 php7.4-bcmath \
       php7.4-imap php7.4-mysql php7.4-mbstring \
       php7.4-xml php7.4-zip php7.4-soap \
       php7.4-intl php7.4-readline \
       php7.4-msgpack php7.4-igbinary php7.4-ldap \
       php7.4-redis \
    && php -r "readfile('http://getcomposer.org/installer');" | php -- --install-dir=/usr/bin/ --filename=composer \
    && apt-get -y autoremove \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

RUN mkdir -p /run/php && chown www-data:www-data /run/php

COPY conf /etc/php/7.4/fpm/pool.d/
COPY php.ini /etc/php/7.4/fpm/php.ini

RUN mkdir -p /var/www/html
WORKDIR /var/www/html

EXPOSE 9000
CMD ["php-fpm7.4"]
