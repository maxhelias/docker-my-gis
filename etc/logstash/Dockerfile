FROM docker.elastic.co/logstash/logstash:5.6.3

MAINTAINER Maxime HELIAS <maximehelias16@gmail.com>

# Add config logstash
ADD ./config/logstash.yml /usr/share/logstash/config/

# Change privilege
USER root
RUN chown logstash:logstash config/logstash.yml
USER logstash

EXPOSE 5000
