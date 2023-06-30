FROM php:8.1-fpm

ENV HOME /www-data
USER root

RUN apt-get update && apt-get install -y apt-utils git zip zlib1g-dev libpng-dev

RUN docker-php-source extract \
    && docker-php-ext-install pdo_mysql gd zip\
    && docker-php-source delete
RUN pecl channel-update pecl.php.net

RUN apt-get update && apt-get install -y zlib1g-dev libzip-dev apt-utils git zip 

RUN pecl install redis\
    && docker-php-ext-enable redis \
    && docker-php-ext-install mysqli \
    && docker-php-ext-install zip

RUN apt-get install -y nodejs yarn


COPY config/php-redis.ini  /usr/local/etc/php/
#add php user
RUN useradd -ms /bin/bash php
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

RUN chown -R www-data /www-data/.composer
USER www-data
RUN composer global require sebastian/phpcpd && \
    composer global require phpmd/phpmd && \
    composer global require squizlabs/php_codesniffer

RUN setsebool -P httpd_can_network_connect on

USER www-data
WORKDIR /var/www
EXPOSE 9004

USER www-data

WORKDIR /var/www/

