FROM php:8.1-fpm  AS builder

RUN useradd -G www-data,root -u 1000 -d /home/admin admin

RUN mkdir -p /home/admin/.composer && \
    chown -R admin:admin /home/admin

RUN apt-get update && apt-get install -y \
    git \
    curl \
    libpng-dev \
    libonig-dev \
    libxml2-dev \
    zip \
    nano \
    unzip

RUN set -eux; \
    apt-get update; \
    apt-get upgrade -y; \
    apt-get install -y --no-install-recommends \
    curl \
    libmemcached-dev \
    libz-dev \
    libpq-dev \
    libjpeg-dev \
    libpng-dev \
    libfreetype6-dev \
    libssl-dev \
    libwebp-dev \
    libxpm-dev \
    libmcrypt-dev \
    libonig-dev; \
    rm -rf /var/lib/apt/lists/*

RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');" && \
    php composer-setup.php && \
    php -r "unlink('composer-setup.php');"

RUN rm -rf /var/www/html

WORKDIR /var/www
USER admin

# RUN php composer.phar create-project --prefer-dist laravel/laravel:5.4.* laravel

# ENTRYPOINT [ "php","laravel/artisan","serve" ]

# 15:47 - CRD - Custom Resource Definition

# 32:57 - annotation = metadado para o k8s interpretar

# CREATE TABLE people(id int not null auto_increment, name varchar(255) not null, primary key(id));