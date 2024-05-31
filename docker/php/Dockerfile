FROM php:8.3.7-fpm

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
    procps \
    && docker-php-ext-install pdo pdo_mysql mysqli exif pcntl \
    && pecl install -f redis xdebug \
    && docker-php-ext-enable pdo_mysql mysqli exif pcntl redis xdebug \
    && apt-get clean && rm -rf /var/lib/apt/lists/*

RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

COPY /docker/php/php.ini /usr/local/etc/php/conf.d/php.ini

COPY . /var/www

USER www-data

EXPOSE 9000
CMD ["php-fpm"]
