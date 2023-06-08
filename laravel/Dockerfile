FROM php:7.4-cli  AS builder

RUN useradd -G www-data,root -u 1000 -d /home/admin admin

RUN mkdir -p /home/admin/.composer && \
    chown -R admin:admin /home/admin

RUN apt-get clean && rm -rf /var/lib/apt/lists/*

RUN apt-get update && \
    apt-get install libzip-dev -y && \
    apt-get install libonig-dev -y && \
    apt-get install libxml2-dev -y && \
    apt-get install libcurl4-openssl-dev -y && \
    docker-php-ext-install zip && \
    docker-php-ext-install mysqli && \
    docker-php-ext-install mbstring && \
    docker-php-ext-install xml && \
    docker-php-ext-install intl && \
    docker-php-ext-install curl && \
    docker-php-ext-install json && \
    docker-php-ext-install xmlrpc


RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');" && \
    php composer-setup.php && \
    php -r "unlink('composer-setup.php');"

EXPOSE 9000 

WORKDIR /var/www
USER admin

CMD [ "php-fpm" ]

###########################################################################
# FROM php:7.4-fpm-alpine

# WORKDIR /var/www

# 

# COPY --from=builder /var/www/ .



# CMD [ ]

