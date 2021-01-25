# Docker Squash to reduce the size of the final Docker image for PHP + Nginx

Carefully crafted Docker Squash to reduce the size of the final Docker image for PHP + Nginx with PHP 7.3, PHP 7.2, PHP 7.1, PHP 7.0, Nginx.

* Fast and simple PHP extensions installation
* Alpine base image with [PHP.earth PHP repositories](https://docs.php.earth/linux/alpine)
* Multiple PHP versions
* [runit](http://smarden.org/runit/) for running multiple services without overhead
* Optional Composer installation
* Optional PHP installation
* Optimized Docker image sizes


## Docker tags

The following list contains all current Docker tags and what is included in each.

| System | Docker Tag | Features | Size |
| ------ | ---------- | -------- | ---- |
| **PHP 7.0.33**@Alpine 3.7.3 | [`7.0-nginx`](https://github.com/phpearth/docker-php/tree/master/docker/7.0-nginx.Dockerfile) | Nginx 1.12.2, FPM | [![](https://images.microbadger.com/badges/image/phpearth/php:7.0-nginx.svg)](https://microbadger.com/images/phpearth/php:7.0-nginx "Image size") |
| **PHP 7.1.28**@Alpine 3.9.3 | [`7.1-nginx`](https://github.com/phpearth/docker-php/tree/master/docker/7.1-nginx.Dockerfile) | Nginx 1.14.2, FPM | [![](https://images.microbadger.com/badges/image/phpearth/php:7.1-nginx.svg)](https://microbadger.com/images/phpearth/php:7.1-nginx "Image size") |
| **PHP 7.2.17**@Alpine 3.9.3 | [`7.2-nginx`](https://github.com/phpearth/docker-php/tree/master/docker/7.2-nginx.Dockerfile) | Nginx 1.14.2, FPM | [![](https://images.microbadger.com/badges/image/phpearth/php:7.2-nginx.svg)](https://microbadger.com/images/phpearth/php:7.2-nginx "Image size") |
| **PHP 7.3.4**@Alpine 3.9.3 | [`7.3-nginx`](https://github.com/phpearth/docker-php/tree/master/docker/7.3-nginx.Dockerfile) | Nginx 1.14.2, FPM | [![](https://images.microbadger.com/badges/image/phpearth/php:7.3-nginx.svg)](https://microbadger.com/images/phpearth/php:7.3-nginx "Image size") |
| **PHP 7.4.0alpha1**@Alpine 3.9.4 | [`7.4-nginx`](https://github.com/phpearth/docker-php/tree/master/docker/7.4-nginx.Dockerfile) | Nginx 1.14.2, FPM | [![](https://images.microbadger.com/badges/image/phpearth/php:7.4-nginx.svg)](https://microbadger.com/images/phpearth/php:7.4-nginx "Image size") |


## Quick usage

### Nginx

`Dockerfile` for running Nginx HTTP server with PHP FPM:

```Dockerfile
FROM dockerstacks/nginx_php:v{PHP version}


### Composer

To install Composer:

```Dockerfile
FROM dockerstacks/nginx_php:v{PHP version}

RUN apk add --no-cache composer
```

### PHPUnit

To install PHPUnit:

```Dockerfile
FROM dockerstacks/nginx_php:v{PHP version}

RUN apk add --no-cache phpunit
```

```Dockerfile
FROM dockerstacks/nginx_php:v{PHP version}

RUN apk add --no-cache php7.3-sodium php7.3-intl php7.3-pdo_mysql
```

or install them with `pecl`:

```bash
apk add --no-cache php7.3-dev gcc g++
pecl install {extension-name}
```

### PHP ini settings
create application specific `php.ini` and copy the file into docker image:


```ini
# php.ini
memory_limit = 512M
```

```Dockerfile
FROM dockerstacks/nginx_php:v{PHP version}

COPY php.ini $PHP_INI_DIR/conf.d/my-app.ini
```

### Docker Stack

Docker Stack is way of orchestration of Docker services and simplifies running multiple services of your application. In this example we'll run an Nginx web server with PHP 7.3 FPM with `docker-compose.yml` file. In a new project directory create a `Dockerfile`:

```Dockerfile
FROM dockerstacks/nginx_php:v{PHP version}
```

The `docker-compose.yml` file:

```yml
version: '3'

services:
  app:
    image: dockerstacks/nginx_php:v{PHP version}
    volumes:
      - .:/var/www/html
    ports:
      - mode: host
        target: 80
        published: 80
```

The `index.php` file:

```php
<?php

phpinfo();
```

And there should be `phpinfo()` output visible on `http://localhost`. Make sure there isn't any other service listening on port 80 before running above command.

### PHP 7.0, 7.1, PHP 7.2

To use older versions PHP 7.0, 7.1, or 7.2 use Docker images with `7.0`, `7.1`, or `7.2`:

```Dockerfile
FROM dockerstacks/nginx_php:v{PHP version}

RUN apk add --no-cache composer
```



