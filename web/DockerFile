FROM php:7.3-apache

RUN apt-get update -y \
    && apt-get upgrade -y \
    && apt-get install -y libfreetype6-dev libjpeg62-turbo-dev libpng-dev libmcrypt-dev libicu-dev libxml2-dev libzip-dev zip libssl-dev openssl ssl-cert \
    && docker-php-ext-configure zip --with-libzip \
    && docker-php-ext-install intl gd mbstring mysqli pdo_mysql soap zip

RUN pecl install mcrypt-1.0.2 && docker-php-ext-enable mcrypt

RUN pecl install xdebug \
  && docker-php-ext-enable xdebug

ADD ./conf/000-default.conf /etc/apache2/sites-enabled/000-default.conf
ADD ./conf/ssl.conf /etc/apache2/sites-available/ssl.conf
ADD ./key/server.key /etc/apache2/server.key
ADD ./key/server.csr /etc/apache2/server.csr
ADD ./key/server.crt /etc/apache2/server.crt

#change server name and docment root
ARG DOCUMENT_ROOT
RUN sed -ri -e "s!/var/www/html!${DOCUMENT_ROOT}!g" /etc/apache2/sites-available/*.conf
RUN sed -ri -e "s!/var/www/!${DOCUMENT_ROOT}!g" /etc/apache2/apache2.conf /etc/apache2/conf-available/*.conf

RUN a2enmod ssl
RUN a2ensite ssl
RUN service apache2 restart
