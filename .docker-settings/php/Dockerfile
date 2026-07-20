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
    && apk del --no-cache .build-deps

RUN apk add --no-cache \
    $PHPIZE_DEPS \
    openssl-dev \
    icu \
    icu-dev \
    zlib-dev 

# Install Node.js and npm    
RUN apk --no-cache add nodejs npm

# Install Composer
COPY --from=composer:latest /usr/bin/composer /usr/local/bin/composer

# Install xdebug
RUN pecl install xdebug && \
    docker-php-ext-enable xdebug && \
    mkdir /var/log/xdebug

# xhprof    
RUN pecl install xhprof && \
    docker-php-ext-enable \  
    xhprof 

# Устанавливаем расширение opentelemetry для PHP
RUN pecl install opentelemetry \
    && docker-php-ext-enable opentelemetry

# Устанавливаем рабочую директорию, куда примонтирован Laravel
WORKDIR /var/www/html