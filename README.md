# Docker Nginx PHP-FPM

Docker-compose and Dockerfiles for building Nginx along with PHP-FPM over TCP

## What is it good for?

Development of a Laravel application. The NGinx templates are specifially set as per LAravel's standards. The stack should include every PHP module and component which you should need.

## What is included in this project?

* Nginx
* PHP 7.1, 7.2 and 7.3
* MySQL
* phpMyAdmin
* Composer (along with binary)

## Prerequisites [`mandatory`]

* Install docker and docker-compose.
* Configure your environment variables in the .env file.
* Upload your PHP project in the ./web directory.

## Configurable vars [`optional`]

* `HOME_DIR` - Used to configure where your project will live inside the Docker containers. You may not need to configure this additionally.
* `NGINX_HOST` -  Hostname which will be set in Nginx configuration.
* `PHP_VERSION` - PHP version which you wish to use. Check https://hub.docker.com/repository/docker/vdzhorov/php-fpm/tags for available PHP versions.
* `PMA_HOST` - Where phpMyAdmin should connect to. You do not need to configure this in order to work correctly.
* `PMA_ARBITRARY` - Set this value to 1 if you want to input which MySQL host your PMA should use. Set this value to 0 if you want this value to be set already for you (defaults to `PMA_HOST`).
* `COMPOSER_ALLOW_SUPERUSER` - If set to 1, this env disables the warning about running commands as root/super user. It also disables automatic clearing of sudo sessions, so you should really only set this if you use Composer as super user at all times like in docker containers.
* `MYSQL_VERSION` - Which MySQL version you wish to use for your project.
* `MYSQL_HOST` - You do not need to change this. This is your hostname where your apps and PMA should connect to.
* `MYSQL_DATABASE` - This will create an empty MySQL database with the value which you input.
* `MYSQL_ROOT_USER` - MySQL root user name. You may want to leave this as root.
* `MYSQL_ROOT_PASSWORD` - Your MySQL root password.
* `MYSQL_USER` - MySQL user which you will use for your apps.
* `MYSQL_PASSWORD` - MySQL password which you will use for your apps.

## Default ports and hosts

* `http://localhost` - Default host
* `mysql` - Default mysql host. Use this in your application configuration.
* `php` - Default PHP-FPM host. You do not need to configure this.
* `8000` - Default http port. Use http://localhost:8000 in order to check on your project.
* `8080` - Default phpMyAdmin access port. Use http://localhost:8080 to access it.

## SSL Certificate [`optional`]

If you wish to have an SSL certificate for your project, you should upload the certificate + bundle and the certificate key in ./etc/ssl directory. Their naming should be ./etc/ssl/server.pem (combined certificate + bundle) and  ./etc/ssl/server.key (certificate key file). ***Do not edit ./etc/nginx/default.conf directly. Edit ./etc/nginx/default.template.conf instead*** 

### Deployment

Run ```docker-compose up```. You should be able to visit http://<YOUR_ENV_ADDRESS>:8000 which will have Nginx and PHP-FPM running.

### Uploading your project

The local directory ./web/public acts as a document root for your project. Your index.php file should live inside this directory.

### Running composer inside running containers

The default composer path is /usr/local/bin/composer.

1. Run ```docker container ls``` and locate the ID of the container which is set for PHP-FPM.
2. Run ```docker exec <ID> composer <OPTIONS> <PATH>```
