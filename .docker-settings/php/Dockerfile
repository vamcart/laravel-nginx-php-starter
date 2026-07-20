# Dockerfile
FROM php:8.5-fpm-alpine

RUN apk update && apk add \
    curl \
    linux-headers \
    libpng-dev \
    libxml2-dev \
    unzip

# Install persistent dependencies and build dependencies
RUN apk add --no-cache \
        libpng \
        libjpeg-turbo \
        freetype \
    && apk add --no-cache --virtual .build-deps \
        $PHPIZE_DEPS \
        libpng-dev \
        libjpeg-turbo-dev \
        freetype-dev \
    && docker-php-ext-configure gd --with-freetype --with-jpeg \
    && docker-php-ext-install -j$(nproc) gd pdo_mysql \
    && pecl install xdebug \
    && docker-php-ext-enable xdebug \
    && apk del --no-cache .build-deps

# Устанавливаем рабочую директорию, куда примонтирован Laravel
WORKDIR /var/www/html