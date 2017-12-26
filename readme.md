# A Docker for your WebGIS application [![Build Status](https://travis-ci.org/maxhelias/docker-my-gis.svg?branch=master)](https://travis-ci.org/maxhelias/docker-my-gis) [![MIT licensed](https://img.shields.io/badge/license-MIT-blue.svg)](https://github.com/maxhelias/docker-my-gis/blob/master/LICENSE)


This repository allows the creation of a Docker environment that meets WebGIS requirements.

## Architecture

|     Containers      |                                 Original                                  |                                             Override                                             |
| ------------------- | :-----------------------------------------------------------------------: | -----------------------------------------------------------------------------------------------: |
|     `workspace`     | [phusion/baseimage:latest](https://hub.docker.com/r/phusion/baseimage/)   | [Dockerfile](https://github.com/maxhelias/docker-my-gis/blob/master/etc/workspace/Dockerfile-56) |
|      `php` 5.6      | [php:5.6.31-fpm](https://hub.docker.com/_/php/)                           | [Dockerfile](https://github.com/maxhelias/docker-my-gis/blob/master/etc/php/Dockerfile-56)       |
|       `nginx`       | [nginx:alpine](https://hub.docker.com/_/nginx/)                           | [Dockerfile](https://github.com/maxhelias/docker-my-gis/blob/master/etc/nginx/Dockerfile)        |
|      `db` 9.5       | [mdillon/postgis:9.5-alpine](https://hub.docker.com/r/mdillon/postgis/)   | [Dockerfile](https://github.com/maxhelias/docker-my-gis/blob/master/etc/db/Dockerfile)           |
|  `mapserver` 6.4.1  | [debian:jessie](https://hub.docker.com/_/debian/)                         | [Dockerfile](https://github.com/maxhelias/docker-my-gis/blob/master/etc/mapserver/Dockerfile)    |
|       `redis`       | [redis:latest](https://hub.docker.com/_/redis/)                           | [Dockerfile](https://github.com/maxhelias/docker-my-gis/blob/master/etc/redis/Dockerfile)        |
|     `rabbitmq`      | [rabbitmq](https://hub.docker.com/_/rabbitmq/)                            | [Dockerfile](https://github.com/maxhelias/docker-my-gis/blob/master/etc/rabbitmq/Dockerfile)     |
|`elasticsearch` 5.6.3| [elasticsearch:5.6.3](https://www.docker.elastic.co/#elasticsearch-5-6-3) | [Dockerfile](https://github.com/maxhelias/docker-my-gis/blob/master/etc/elasticsearch/Dockerfile)|
|   `kibana` 5.6.3    | [kibana:5.6.3](https://www.docker.elastic.co/#kibana-5-6-3)               | [Dockerfile](https://github.com/maxhelias/docker-my-gis/blob/master/etc/kibana/Dockerfile)       |
|  `logstash` 5.6.3   | [logstash:5.6.3](https://www.docker.elastic.co/#logstash-5-6-3)           | [Dockerfile](https://github.com/maxhelias/docker-my-gis/blob/master/etc/logstash/Dockerfile)     |
|      `maildev`      | [djfarrelly/maildev:latest](https://hub.docker.com/r/djfarrelly/maildev/) | [Dockerfile](https://github.com/maxhelias/docker-my-gis/blob/master/etc/maildev/Dockerfile)      |

_All containers are in the **./etc/** folder_

## Additional Features
Since this environment is designed for a local usage, it comes with features helping the development workflow.

## Installation
This process assumes that [Docker Engine](https://www.docker.com/docker-engine) and [Docker Compose](https://docs.docker.com/compose/) are installed.
Otherwise, you should have a look to [Install Docker Engine](https://docs.docker.com/engine/installation/) before proceeding further.

### Clone the repository
```bash
$ git clone https://github.com/maxhelias/docker-my-gis.git
```

### Define the environment variables
```bash
$ cp env-example .env
```


### Run your containers
```bash
$ docker-compose up -d
```

_You can specify some container to run by adding their current name to the docker-compose.yml file_

### Open your browser and visit localhost
* `http://localhost` for access to your application
 OR
* `http://localhost/mapserver/` for access to your MapServer instance

```bash
That's it! Enjoy :)
```

You will then be able to access the following sample MapServer URLs :

* <http://localhost/mapserver/?map=example1-1.map&layers=all&mode=map>
* <http://localhost/mapserver/?map=example1-2.map&layers=all&mode=map>
* <http://localhost/mapserver/?map=example1-3.map&layers=all&mode=map>
* <http://localhost/mapserver/?map=example1-4.map&layers=all&mode=map>
* <http://localhost/mapserver/?map=example1-5.map&layers=all&mode=map>
* <http://localhost/mapserver/?map=example1-6.map&layers=all&mode=map>
* <http://localhost/mapserver/?map=example1-7.map&layers=all&mode=map>

## By default

* The application folder mounted on the workspace instance is **./usr/www/**. It can be defined in the configuration file with the variable **APPLICATION**
* The sites available folder mounted on the Nginx instance is **./etc/nginx/sites/**. It can be defined in the configuration file with the variable **NGINX_SITES_PATH**
* The data folder mounted on the MapServer instance is **./usr/geo/mapserver/**. It can be defined in the configuration file with the variable **MAPSERVER_DATA**
* Also, you can define any variable in the configuration file to adapt it to your needs