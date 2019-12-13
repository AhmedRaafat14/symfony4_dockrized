# Symfony 4.4 on Docker
Install Symfony 4.4 on containers.


### Requirements:
* Docker

### Usage:
* Clone this repository:
```bash
$ git clone https://github.com/AhmedRaafat14/symfony4_dockrized.git
```

* If you already have a symfony project you want to use, just comment the following lines and update the paths in all files from `/var/www/dashboard` to `/var/www/your_project_name`. OR just change from `website-skeleton` to normal `symfony` package.
```docker
# docker/php-fpm/Dockerfile
WORKDIR /var/www
RUN composer create-project symfony/website-skeleton:^4.4 dashboard
# RUN composer create-project symfony/skeleton:^4.4 dashboard
```
* You can also add volumes for your project folder in the `docker-compose` file.
```docker
# docker-compose.yml
php:
    volumes:
      - ./your_project_name:/var/www/your_project_name
```
```docker
# docker-compose.yml
nginx:
    volumes:
      - ./your_project_name:/var/www/your_project_name

```
> files to change the relative path in is: `docker/nginx/{Dockerfile, sites}` & `docker/php-fpm/Dockerfile`

* Go to the repo directory and run `docker-compose`. (Make sure you have docker up & running).
```bash
$ cd symfony4_dockrized
$ docker-compose up -d --build
```

* You can check the up & running containers if everything went fine:
```bash
$ docker ps
```

* To check your application is up and running go to http://localhost/, you will see there a the welcome page.

### Usfual commands:
* Clear the cache of the application, specially when you change the twig templates (make sure you inside the symfony4_dockrized directory)
```bash
$ docker-compose exec php bin/console cache:clear -e prod
$ docker-compose exec php chmod 777 -R var/cache
```
* Install a new package:
```bash
$ docker-compose exec php composer require symfony/maker-bundle --dev
```

#### Now Enjoy Developing :dancer:
