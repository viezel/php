FROM ubuntu:22.04

MAINTAINER Mads Møller

ENV DEBIAN_FRONTEND=noninteractive
ENV TZ=UTC

RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

RUN apt-get update \
    && apt-get install -y gnupg gosu curl ca-certificates zip unzip git supervisor sqlite3 libcap2-bin libpng-dev python2 \
    && mkdir -p ~/.gnupg \
    && chmod 600 ~/.gnupg \
    && echo "disable-ipv6" >> ~/.gnupg/dirmngr.conf \
    && apt-key adv --homedir ~/.gnupg --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys E5267A6C \
    && apt-key adv --homedir ~/.gnupg --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys C300EE8C \
    && echo "deb http://ppa.launchpad.net/ondrej/php/ubuntu hirsute main" > /etc/apt/sources.list.d/ppa_ondrej_php.list \
    && apt-get update \

    && apt-get install -y php8.1 php8.1-fpm php8.1-dev \
       php8.1-gd php8.1-curl php8.1-bz2 php8.1-bcmath \
       php8.1-imap php8.1-mysql php8.1-mbstring \
       php8.1-xml php8.1-zip php8.1-soap \
       php8.1-intl php8.1-readline \
       php8.1-msgpack php8.1-igbinary php8.1-ldap \
       php8.1-redis \
    && php -r "readfile('http://getcomposer.org/installer');" | php -- --install-dir=/usr/bin/ --filename=composer \
    && apt-get -y autoremove \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

RUN mkdir -p /run/php && chown www-data:www-data /run/php

COPY conf /etc/php/8.1/fpm/pool.d/
COPY php.ini /etc/php/8.1/fpm/php.ini

RUN mkdir -p /var/www/html
WORKDIR /var/www/html

EXPOSE 9000
CMD ["php-fpm8.1"]
