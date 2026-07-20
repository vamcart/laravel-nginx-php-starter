# Laravel Starter Pack - Nginx, PHP 8.5, xDebug

Simple to use Laravel Starter Pack.

## Start nginx, php with Docker Compose:

* Download repo:
``
git clone git@github.com:vamcart/laravel-nginx-php-starter.git
``
* Go to files:
``
cd laravel-nginx-php-starter
``
* Copy .env
``
cp .env.dist .env
``
* Start nginx, php with docker compose
``
docker compose up -d
``
* Try to open http://localhost:8084 . You muse ses 404 nginx page. It's fine.

## Laravel install

* Connect to container:
``
sudo docker exec -it laravel-app-php /bin/sh
``
* Install laravel
``
composer create-project laravel/laravel ./
``
* Set permissions
``
chmod -R 777 public storage database
``
* Ths't all, your laravel copy ready to develop. Open http://localhost:8084 , you must see Laravel welcome page.