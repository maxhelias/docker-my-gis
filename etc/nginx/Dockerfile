FROM nginx

MAINTAINER Maxime HELIAS <maximehelias16@gmail.com>

# Add content for nginx
COPY . /usr/local/docker
RUN chmod -R 777 /usr/local/docker

# Update & Install
RUN apt-get update && apt-get install -y wget curl

# For Fastcgi cache
RUN chown -R www-data:www-data /var/cache/nginx

# Delete default config
RUN rm /etc/nginx/conf.d/default.conf
RUN rm /etc/nginx/nginx.conf

# Add config
ADD default.conf /etc/nginx/conf.d/
ADD nginx.conf /etc/nginx/
	
EXPOSE 443 80

WORKDIR /var/www/html

CMD ["nginx"]
