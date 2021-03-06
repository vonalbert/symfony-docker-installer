FROM composer:1.5 AS composer
FROM node:9.2.0-alpine AS nodejs
FROM php:7.1-fpm-alpine

WORKDIR /srv/app


# --------------------------------------
# System setup
# --------------------------------------
ENV ENV /root/.ashrc
RUN echo "alias sf='bin/console'" >> /root/.ashrc \
    && echo "alias ll='ls -lah'"  >> /root/.ashrc

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


# --------------------------------------
# PHP/Composer setup
# --------------------------------------
ENV COMPOSER_ALLOW_SUPERUSER 1
COPY php.ini /usr/local/etc/php/php.ini
COPY --from=composer /usr/bin/composer /usr/bin/composer


# --------------------------------------
# Setup nodejs from the node image
# --------------------------------------
COPY --from=nodejs /usr/local/bin/node /usr/local/bin/node
COPY --from=nodejs /usr/local/lib/node_modules /usr/local/lib/node_modules
COPY --from=nodejs /opt/yarn /opt/yarn
RUN ln -s /usr/local/lib/node_modules/npm/bin/npm-cli.js /usr/local/bin/npm \
	&& ln -s /usr/local/lib/node_modules/npm/bin/npx-cli.js /usr/local/bin/npx \
	&& ln -s /opt/yarn/bin/yarn /usr/local/bin/yarn \
	&& ln -s /opt/yarn/bin/yarn /usr/local/bin/yarnpkg


COPY appinit /usr/local/bin/appinit
RUN chmod +x /usr/local/bin/appinit
