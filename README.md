# Docker for Laravel (docker-nginx-php7.2-pgsql-pgadmin4)
Docker environment with NGINX, PHP 7.2 (with XDebug), PgSQL and PgAdmin4

## Getting Started
Clone this repo and follow the instructions to get up a docker environment for your Laravel app

### Run containers
With docker and docker-compose installed enter in the cloned path and run:
```
docker-compose up -d
```

### Create Laravel project
If you want to create a project with different name, set the correct volume in the docker-compose.yml for php-fpm container
```
- ./myapp:/var/www/html
```
to
```
- ./mynamedapp:/var/www/html
```
and restart containers

With containers running, run:
```
docker exec myapp-php composer create-project --prefer-dist laravel/laravel myapp
```

### Initialize Laravel project
With containers running, run the commands necessary to laravel initialization in the container:
```
docker exec myapp-php composer install
docker exec myapp-php php artisan key:generate
docker exec myapp-php php artisan migrate
docker exec myapp-php php artisan passport:install
...
```

### Enable Xdebug in VSCode
Insert this config in your launch.json
```
{
    "version": "0.2.0",
    "configurations": [
        {
            "name": "Listen for XDebug",
            "type": "php",
            "request": "launch",
            "port": 9000,
            "pathMappings": {
                "/var/www/html": "${workspaceRoot}/myapp"
            }
        },
        {
            "name": "Launch currently open script",
            "type": "php",
            "request": "launch",
            "program": "${file}",
            "cwd": "${fileDirname}",
            "port": 9000
        }
    ]
}
```
