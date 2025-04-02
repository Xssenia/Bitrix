FROM php:8.1-fpm

RUN apt-get update && apt-get install -y \
    libpng-dev \
    libjpeg-dev \
    libfreetype6-dev \
    libzip-dev \
    zip unzip \
  && docker-php-ext-configure gd --with-freetype --with-jpeg \
  && docker-php-ext-install -j$(nproc) gd mysqli pdo pdo_mysql \
  && pecl install redis \
  && docker-php-ext-enable redis

COPY php.ini /usr/local/etc/php/

COPY bitrix_archive.tar.gz /tmp/bitrix_archive.tar.gz

RUN mkdir -p /var/www/html && \
    tar -xzf /tmp/bitrix_archive.tar.gz -C /var/www/html && \
    rm /tmp/bitrix_archive.tar.gz && \
    chown -R www-data:www-data /var/www/html

RUN apt-get clean && rm -rf /var/lib/apt/lists/*

CMD ["php-fpm"]