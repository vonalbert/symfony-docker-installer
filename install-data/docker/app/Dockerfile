FROM composer:1.5
FROM php:7.1-fpm-alpine

WORKDIR /srv/app


# --------------------------------------
# Install Dependencies
# --------------------------------------
RUN apk add --no-cache --virtual .persistent-deps \
		git \
		icu-libs \
		zlib

ENV APCU_VERSION 5.1.8
RUN set -xe \
	&& apk add --no-cache --virtual .build-deps \
		$PHPIZE_DEPS \
		icu-dev \
		zlib-dev \
	&& docker-php-ext-install \
		intl \
		zip \
		pdo \
		pdo_mysql \
	&& pecl install \
		apcu-${APCU_VERSION} \
	&& docker-php-ext-enable --ini-name 20-apcu.ini apcu \
	&& docker-php-ext-enable --ini-name 05-opcache.ini opcache \
	&& apk del .build-deps

RUN apk add --no-cache --virtual nodejs


# --------------------------------------
# PHP ini Setup
# --------------------------------------
COPY php.ini /usr/local/etc/php/php.ini


# --------------------------------------
# Composer Setup
# --------------------------------------
ENV COMPOSER_ALLOW_SUPERUSER 1
COPY --from=0 /usr/bin/composer /usr/bin/composer


# --------------------------------------
# Setup ash environment / aliases
# --------------------------------------
ENV ENV /root/.ashrc
RUN echo "alias sf='bin/console'" >> /root/.ashrc \
    && echo "alias ll='ls -lah'"  >> /root/.ashrc
