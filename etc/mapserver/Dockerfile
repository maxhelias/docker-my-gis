FROM debian:jessie

MAINTAINER Maxime HELIAS <maximehelias16@gmail.com>

RUN groupadd -g 8080 mapserver && \
	useradd -r -d /home/mapserver -m -g mapserver -u 8080 mapserver

# Update & Install dependency
RUN apt-get update && \
	apt-get install -y cgi-mapserver \
	mapserver-bin \
	spawn-fcgi

# Startup script
COPY scripts/mapserver /mapserver
RUN chmod 0755 /mapserver

EXPOSE 8080

VOLUME ["/usr/local/share/mapserver"]

# User-configurable parameters
ENV FCGI_LISTEN_ADDRESS=0.0.0.0 \
	FCGI_LISTEN_PORT=8080 \
	FCGI_NPROC=1 \
	FCGI_BACKLOG=1024 \
	FCGI_UID=mapserver \
	FCGI_GID=mapserver \
	MS_ERRORFILE=stderr

CMD ["/mapserver"]
