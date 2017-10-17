FROM debian:jessie

MAINTAINER Maxime HELIAS <maximehelias16@gmail.com>

ENV GDAL_VERSION 2.2.1
ENV GEOS_VERSION 3.6.2
ENV PROJ_VERSION 4.9.3
ENV HARFBUZZ_VERSION 1.5.1

# Add content for mapserver
COPY . /usr/local/docker
RUN chmod -R 777 /usr/local/docker

# Update & Install dependency
RUN apt-get update && \
	apt-get install -y wget \
		curl \
		libcurl4-gnutls-dev \
		libssl-dev \
		openssl \
		software-properties-common \
		g++ \
		make \
		cmake \
		git \
		build-essential \
		bzip2 \
		unzip \
		tar \
		libfreetype6-dev \
		zlib1g-dev \
		libpng-dev \
		libjpeg-dev \
		libproj-dev \
		proj-data \
		shapelib \
		libxml2-dev \
		libxslt1-dev \
		libcairo2-dev \
		libpixman-1-dev \
		librsvg2-dev \
		libgif-dev \
		libmysqlclient-dev \
        libpq-dev \
		libtiff5-dev \
		libfcgi-dev \
		libfribidi-dev \
		libharfbuzz-dev \
		libgdal-dev \
		libgeos-dev

# Install OGR

# Install libharfbuzz from source as it is not in a repository
# RUN cd /tmp && wget http://www.freedesktop.org/software/harfbuzz/release/harfbuzz-$HARFBUZZ_VERSION.tar.bz2 && \
    tar xjf harfbuzz-$HARFBUZZ_VERSION.tar.bz2 && \
    cd harfbuzz-$HARFBUZZ_VERSION && \
    ./configure && \
    make && \
    make install && \
    ldconfig

# Install Mapserver
RUN git clone https://github.com/mapserver/mapserver/ /usr/local/src/mapserver

# Compile Mapserver
RUN mkdir /usr/local/src/mapserver/build && \
	cd /usr/local/src/mapserver/build && \
	cmake ../ -DWITH_THREAD_SAFETY=1 \
		-DWITH_PROJ=1 \
		-DWITH_KML=1 \
		-DWITH_SOS=1 \
		-DWITH_FRIBIDI=1 \
		-DWITH_HARFBUZZ=1 \
		-DWITH_ICONV=1 \
		-DWITH_CAIRO=1 \
		-DWITH_CAIROSVG=1 \
		-DWITH_RSVG=1 \
		-DWITH_MYSQL=0 \
		-DWITH_GEOS=1 \
		-DWITH_POSTGIS=1 \
		-DWITH_GDAL=1 \
		-DWITH_OGR=1 \
		-DWITH_CURL=1 \
		-DWITH_CLIENT_WMS=1 \
		-DWITH_CLIENT_WFS=1 \
		-DWITH_WMS=1 \
		-DWITH_WFS=1 \
		-DWITH_WCS=1 \
		-DWITH_LIBXML2=1 \
		-DWITH_GIF=1 \
		-DWITH_XMLMAPFILE=1 \
		-DWITH_PHP=1 \
		-DWITH_FCGI=1 && \
		make && \
		make install && \
		ldconfig

# Link to cgi-bin executable
#RUN chmod o+x /usr/local/bin/mapserv
#RUN ln -s /usr/local/bin/mapserv /usr/lib/cgi-bin/mapserv
#RUN chmod 755 /usr/lib/cgi-bin

# Install the test mapfile
RUN mkdir /usr/local/share/mapserver/mapfile
COPY test.map /usr/local/share/mapserver/mapfile/

# Install MapCache

EXPOSE 80

WORKDIR /usr/local/share/mapserver
