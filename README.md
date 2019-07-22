# Docker Nginx PHP-FPM

Docker-compose and Dockerfiles for building Nginx along with PHP-FPM over TCP

## Prerequisites

* Install docker and docker-compose.
* Configure your environment variables in the .env file.
* Upload your PHP project in the ./web directory.

### Deployment

Run ```docker-compose up```. You should be able to visit http://<YOUR_ENV_ADDRESS>:8000 which will have Nginx and PHP-FPM running.
