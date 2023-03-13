FROM php:8.2-cli-alpine

COPY --from=composer:2 /usr/bin/composer /usr/bin/composer

RUN apk add --no-cache unzip

ADD https://github.com/mlocati/docker-php-extension-installer/releases/latest/download/install-php-extensions /usr/local/bin/
RUN chmod +x /usr/local/bin/install-php-extensions

# xdebug, pcov are installed, but aren't enabled by default
RUN IPE_DONT_ENABLE=1 install-php-extensions intl gd pdo_mysql pdo_pgsql zip redis-5.3.7 xdebug-3.2.0 pcov-1.0.11
RUN docker-php-ext-enable redis

RUN mv "$PHP_INI_DIR/php.ini-development" "$PHP_INI_DIR/php.ini"
COPY ./php-ini-overrides.ini "$PHP_INI_DIR/conf.d/99-overrides.ini"

WORKDIR /app
