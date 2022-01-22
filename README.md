# Nginx stack

> Docker-compose project with Alpine linux, Nginx and PHP. Super easy to get started and running in a few mins

## Install

### Using DECK

Install nginx-stack from the DECK marketplace and follow the instructions on the GUI

### From terminal with Docker

```
git clone https://github.com/deck-app/nginx-stack/
cd nginx-stack
```

Edit `.env` file to change any settings before installing like php, nginx versions etc

```
docker-compose up -d
```
### Modifying project settings
From the DECK app, go to stack list and click on project's `More > configure > Advanced configuration`
Follow the instructions below and restart your stack from the GUI

#### Edit Nginx configuration

default.conf is located at `./nginx/default.conf`

#### Editing php.in

PHP ini file is located at `./nginx/php_ini/php{YOUR.PHP.VERSION}.ini`

#### Installing / removing PHP extensions

Add / remove PHP extensions from `./nginx/Dockerfile-{YOUR.PHP.VERSION}`

```
ARG DEPS="\
        nginx \
        nginx-mod-http-headers-more \
        php7.4 \
        php7.4-phar \
        ...
        php7.4-{extension name here}
```

#### Rebuilding from terminal

You have to rebuild the docker image after you make any changes to the project configuration, use the snippet below to rebuild and restart the stack

```
docker-compose stop && docker-compose up --build -d
```
