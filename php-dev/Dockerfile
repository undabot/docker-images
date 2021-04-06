ARG PHP_VERSION=8.0.3

FROM php:$PHP_VERSION-fpm-alpine

ARG USER_ID=1000
ARG GROUP_ID=1000

# Create app user and group with UID same as provided argument to avoid permission issues and conflicts
RUN addgroup -g "$GROUP_ID" -S app
RUN adduser -S app -D -u $USER_ID -G app

# Install dependencies and utils
ENV RUNTIME_DEPS="icu-dev bash nano vim git libzip-dev zip unzip libpng-dev"
RUN apk add --update --no-cache $RUNTIME_DEPS

RUN docker-php-ext-install intl pdo pdo_mysql zip gd 

RUN pecl install xdebug
RUN docker-php-ext-enable xdebug

# Install composer
RUN apk add --update --no-cache composer
RUN composer self-update

# create app directory
RUN mkdir -p /opt/app && chown app /opt/app

USER app
WORKDIR /opt/app

RUN composer global require maglnet/composer-require-checker