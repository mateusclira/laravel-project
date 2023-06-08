FROM php:7.4-cli  AS builder

WORKDIR /var/www

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

RUN php composer.phar create-project --prefer-dist laravel/laravel laravel

ENTRYPOINT [ "php","laravel/artisan","serve" ]

CMD [ "--host=0.0.0.0" ]

###########################################################################
FROM php:7.4-fpm-alpine

WORKDIR /var/www

RUN rm -rf /var/www/html

COPY --from=builder /var/www/laravel .

RUN chown -R www-data:www-data /var/www

EXPOSE 9000 

CMD [ "php-fpm" ]