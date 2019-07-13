FROM php:7.3-fpm

LABEL maintainer="Jose Carlos Gallo <josecgallo@jjsoft.com.ar>"

ENV DEBIAN_FRONTEND noninteractive

RUN apt-get update && apt-get install -y \
    openssl \
    net-tools \
    locales \
    git \
    unzip \
    mariadb-client \
    zlib1g-dev \
    libjpeg-dev\
    libpng-dev\
    libfreetype6-dev \
    libpq-dev \
    libicu-dev g++ && \
    locale-gen es_AR.UTF-8

# Add add-apt-repository command
RUN apt-get update && \
    apt-get install -y software-properties-common

ENV LANGUAGE=es_AR:es_ES:es
RUN echo America/Argentina/Buenos_Aires > /etc/timezone && dpkg-reconfigure --frontend noninteractive tzdata

# Add Repo ppa:ondrej/php
# Install php common extension
# zip and unzip is essential component for composer to run 
RUN LC_ALL=es_AR.UTF-8 add-apt-repository && \
    add-apt-repository ppa:ondrej/php && \
    apt-get update && \
    apt-get install -y \
    php7.3-fpm \
    php7.3-common \
    php7.3-mysql \
    php7.3-pdo \
    php7.3-xml \
    php7.3-xmlrpc \
    php7.3-curl \
    php7.3-gd \
    php7.3-imagick \
    php7.3-cli \
    php7.3-dev \
    php7.3-imap \
    php7.3-mbstring \
    php7.3-opcache \
    php7.3-soap \
    php7.3-imap \
    php7.3-zip \
    zip \
    unzip -y

ENV COMPOSER_ALLOW_SUPERUSER=1
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer
RUN composer --version

RUN docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ && \
    docker-php-ext-configure imap --with-imap-ssl --with-kerberos 

RUN docker-php-ext-install pdo pdo_mysql mysqli zip gd intl imap

COPY php.ini /etc/php/7.3/fpm/php.ini

WORKDIR /var/www