FROM docker.elastic.co/kibana/kibana:5.6.3

MAINTAINER Maxime HELIAS <maximehelias16@gmail.com>

# Add config kibana
ADD ./config/kibana.yml /usr/share/kibana/config/

# Change privilege
USER root
RUN chown kibana:kibana config/kibana.yml
USER kibana

EXPOSE 5601
