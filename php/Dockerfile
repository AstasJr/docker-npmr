FROM php:8.2.10-fpm

USER root

WORKDIR /var/www

RUN apt-get update && apt-get install -y \
    build-essential \
    libzip-dev \
    locales \
    zip \
    nano \
    unzip \
    git \
    curl \
    procps && \
    apt-get clean && rm -rf /var/lib/apt/lists/*

RUN docker-php-ext-install pdo_mysql exif pcntl && \
    pecl install -f redis xdebug && \
    docker-php-ext-enable redis xdebug && \
    curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

COPY . /var/www

USER www-data

EXPOSE 9000
CMD ["php-fpm"]
