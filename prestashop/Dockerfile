#
# Dockerfile for prestashop
#

FROM php:5.6-apache
MAINTAINER kev <noreply@easypi.pro>

RUN a2enmod rewrite

RUN set -xe \
    && apt-get update \
    && apt-get install -y libicu-dev libpng-dev libjpeg-dev libmcrypt-dev unzip \
    && rm -rf /var/lib/apt/lists/* \
    && docker-php-ext-configure intl \
    && docker-php-ext-configure gd --with-png-dir=/usr --with-jpeg-dir=/usr \
    && docker-php-ext-install intl gd mbstring mcrypt opcache pdo pdo_mysql zip

WORKDIR /var/www/html

ENV PS_VER 1.7.2.4
ENV PS_MD5 19c374fd4e65e2a0d978c619781686bc
ENV PS_URL https://download.prestashop.com/download/releases/prestashop_${PS_VER}.zip
ENV PS_FILE prestashop_${PS_VER}.zip

RUN set -xe \
    && echo "short_open_tag=off" >> /usr/local/etc/php/php.ini \
    && curl -sSL ${PS_URL} -o ${PS_FILE} \
    && echo "${PS_MD5}  ${PS_FILE}" | md5sum -c \
    && unzip ${PS_FILE} \
    && rm ${PS_FILE} \
    && chown -R www-data:www-data /var/www
