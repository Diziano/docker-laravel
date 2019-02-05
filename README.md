# Laravel in Docker containers

## How to use

### Get the files and run the containers
```bash
# Get docker files
git clone https://github.com/diziano/docker-laravel.git
cd docker-laravel

# Start the application by running the background containers
docker-compose up -d

# See containers running
docker ps

# A similar output is expected with:
CONTAINER ID        IMAGE                 COMMAND                  CREATED              STATUS              PORTS                                      NAMES
3707fc552bcc        nginx:alpine          "nginx -g 'daemon of…"   About a minute ago   Up About a minute   0.0.0.0:80->80/tcp, 0.0.0.0:443->443/tcp   webserver
897303f58c81        postgres:9.3-alpine   "docker-entrypoint.s…"   About a minute ago   Up About a minute   0.0.0.0:5432->5432/tcp                     db
7b22e39501a0        diziano/php-nginx     "docker-php-entrypoi…"   About a minute ago   Up About a minute   9000/tcp                                   app

```
### Create a Laravel application (in app container)
```bash
# Install Laravel
docker exec app composer create-project laravel/laravel laravel
docker exec app mv laravel/* ./; mv laravel/.* ./; rm -rf larave
```



