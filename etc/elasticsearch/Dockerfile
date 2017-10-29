FROM docker.elastic.co/elasticsearch/elasticsearch:5.6.3

MAINTAINER Maxime HELIAS <maximehelias16@gmail.com>

# Add config elasticsearch
ADD ./config/elasticsearch.yml /usr/share/elasticsearch/config/

# Change privilege
USER root
RUN chown elasticsearch:elasticsearch config/elasticsearch.yml
USER elasticsearch

EXPOSE 9200 9300