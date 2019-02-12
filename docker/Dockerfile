FROM php:7-fpm

RUN apt-get -qy update && \
    apt-get -qy dist-upgrade && \
    apt-get -qy install \
    gettext \
    libpq-dev \
    postgresql-client

RUN apt-get update && apt-get install -y \
        libfreetype6-dev \
        libjpeg62-turbo-dev \
        libmcrypt-dev \
        libpng12-dev \
    && docker-php-ext-install -j$(nproc) iconv mcrypt mbstring pdo_mysql pdo_pgsql zip \
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install -j$(nproc) gd

RUN curl -sS https://getcomposer.org/installer | php && \
    mv composer.phar /usr/local/bin/composer && \
    composer self-update && \
    apt-get remove --purge curl -y && \
    apt-get clean

ENV COMPOSER_HOME /root/.composer
ENV PATH vendor/bin:$COMPOSER_HOME/vendor/bin:$PATH

RUN composer global require "laravel/installer"

RUN mkdir -p /code
WORKDIR /code