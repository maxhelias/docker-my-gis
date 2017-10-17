FROM nginx:alpine

MAINTAINER Maxime HELIAS <maximehelias16@gmail.com>

# Add content for nginx
COPY . /usr/local/docker
RUN chmod -R 777 /usr/local/docker

# Update & Install
RUN apk update \
	&& apk upgrade \
	&& apk add --no-cache bash \
	&& adduser -D -H -u 1000 -s /bin/bash www-data

# For Fastcgi cache
RUN chown -R www-data:www-data /var/cache/nginx

# Delete default config
RUN rm /etc/nginx/conf.d/default.conf
RUN rm /etc/nginx/nginx.conf

# Add config
ADD default.conf /etc/nginx/conf.d/
ADD nginx.conf /etc/nginx/

# Set upstream conf and remove the default conf
RUN echo "upstream php-upstream { server ${PHP_UPSTREAM_CONTAINER}:${PHP_UPSTREAM_PORT}; }" > /etc/nginx/conf.d/upstream.conf \
    && rm /etc/nginx/conf.d/default.conf
	
EXPOSE 443 80

CMD ["nginx"]
