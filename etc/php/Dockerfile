FROM php:5.6.31-fpm

MAINTAINER Maxime HELIAS <maximehelias16@gmail.com>

# Add content for php
COPY . /usr/local/docker
RUN chmod -R 777 /usr/local/docker

# Update & Install
RUN apt-get update && \
	apt-get install -y wget \
		curl \
		libz-dev \
		libpq-dev \
		libjpeg-dev \
		libpng12-dev \
		libfreetype6-dev \
		libssl-dev \
		libmcrypt-dev && \
	docker-php-ext-configure gd \
		--enable-gd-native-ttf \
		--with-jpeg-dir=/usr/include/ \
		--with-freetype-dir=/usr/include/freetype2 && \
	docker-php-ext-install -j$(nproc) \
		gd \
		mcrypt \
		mbstring \
		pdo_pgsql && \
	yes | pecl install xdebug && \
	docker-php-ext-enable xdebug && \
	rm -rf /var/lib/apt/lists/*

ADD php.ini /usr/local/etc/php/conf.d/
ADD php-fpm.conf /usr/local/etc/php-fpm-custom.conf

#####################################
# xDebug:
#####################################

ENV HOST_IP = `/sbin/ip route | awk '/default/ { print $3}'`
ADD xdebug.ini /usr/local/etc/php/conf.d/
RUN echo "xdebug.remote_host="$HOST_IP >> /usr/local/etc/php/conf.d/xdebug.

#####################################
# Blackfire:
#####################################

#####################################
# PHP REDIS EXTENSION FOR PHP 5
#####################################

#####################################
# Opcache:
#####################################

#####################################
# Image optimizers:
#####################################

#####################################
# ImageMagick:
#####################################

RUN usermod -u 1000 www-data

WORKDIR /var/www

CMD ["php-fpm"]

EXPOSE 9000
