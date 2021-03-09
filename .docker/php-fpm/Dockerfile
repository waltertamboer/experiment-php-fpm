FROM php:8.0-fpm-alpine

COPY .docker/php-fpm/usr/local/etc/php/conf.d/90-experiment.ini /usr/local/etc/php/conf.d/90-experiment.ini

RUN addgroup -Sg 101 nginx; \
    adduser -H -h /dev/null -u 101 -G nginx -S -s /sbin/nologin -g nginx nginx; \
    adduser www-data nginx; \
    apk add --no-cache \
        libpq \
        libzip \
        postgresql-client \
        tzdata; \
    apk --update add --no-cache --virtual .build-deps \
        autoconf \
        build-base \
        libzip-dev \
        postgresql-dev; \
    docker-php-ext-install opcache pdo_mysql pdo_pgsql zip; \
    apk del .build-deps; \
    docker-php-source delete; \
    rm -r /usr/local/bin/docker-php-source /usr/local/bin/docker-php-ext-* /usr/local/bin/php-config /usr/local/bin/pecl /usr/local/bin/pear /usr/local/bin/peardev /usr/local/bin/phpdbg /usr/local/bin/phpize /usr/local/lib/php/*.php /usr/local/lib/php/Archive /usr/local/lib/php/Console /usr/local/lib/php/OS /usr/local/lib/php/PEAR /usr/local/lib/php/Structures /usr/local/lib/php/XML /usr/local/lib/php/build /usr/local/lib/php/data /usr/local/lib/php/doc /usr/local/lib/php/test;
