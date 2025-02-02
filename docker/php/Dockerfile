FROM php:8.3-fpm

RUN apt-get -y update && apt-get upgrade -y
RUN apt-get update && apt-get install -y libpq-dev \
    && docker-php-ext-install pdo pdo_pgsql

CMD ["php-fpm"]
