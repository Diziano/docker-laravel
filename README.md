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
docker exec app mv laravel/* ./; mv laravel/.* ./; rm -rf laravel
```
### Configure Laravel application
```bash
# Configure database pparameters in Laravel Environment file
nano .env

# Parameters of database:
DB_CONNECTION=pgsql
DB_HOST=127.0.0.1
DB_PORT=5432
DB_DATABASE=your_database_name
DB_USERNAME=your_database_username
DB_PASSWORD=your_database_password

# Generate a key and copy it to your .env file
docker exec app php artisan key:generate

# Generates configuration caching to increase performance
docker exec app php artisan config:cache
```
This is ready, go to http://localhost or http://your_server_ip to see the Laravel screen runnin

```
### Configure database
```bash
# Log in to your database (the PostgreSQL client must be installed on your machine)
psql -Upostgres -h localhost

# Create database (with the name defined in the .env file)
CREATE DATABASE your_database_name;
```
Note: The database user and password have been defined in docker-compose.yml

```

### Migrate Laravel

```bash
# Run the Laravel artisan migrate command, which creates a table of migrations in the database
docker exec app php artisan migrate
```

### Useful commands
```bash
# Open terminal interative in App container
docker exec -it app /bin/bash
```


