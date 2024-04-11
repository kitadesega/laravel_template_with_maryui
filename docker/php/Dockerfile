FROM php:8.3-fpm as base

RUN cd /usr/bin && curl -s http://getcomposer.org/installer | php && ln -s /usr/bin/composer.phar /usr/bin/composer
RUN apt-get update \
    && apt-get install -y \
       git \
       zip \
       unzip \
       vim \
       curl \
       libzip-dev \
       libpng-dev \
       libjpeg-dev \
       libgif-dev \
       libicu-dev \
       iputils-ping \
       libfreetype6-dev \
       net-tools \
       npm \
       libonig-dev \
       sendmail
RUN docker-php-ext-install pdo_mysql bcmath opcache \
    && docker-php-ext-configure gd --with-freetype=/usr/include/ --with-jpeg=/usr/include/ \
    && docker-php-ext-install -j$(nproc) gd \
    && docker-php-ext-configure intl \
    && docker-php-ext-install zip intl

COPY docker/php/php.ini /usr/local/etc/php/php.ini


