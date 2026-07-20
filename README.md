# Стартовый набор для laravel приложения

Nginx + PHP 8.5 + xDebug

## Установка nginx, php в docker окружении:

* Выгружаем репозиторий:
``
git clone git@github.com:vamcart/laravel-nginx-php-starter.git
``
* Переходим в папку:
``
cd laravel-nginx-php-starter
``
* Копируем .env файл
``
cp .env.dist .env
``
* Запускаем веб-сервер, php в докер окружении
``
docker compose up -d
``
* Открываем в браузере http://localhost:8084 . Должна открыться 404 страница nginx.

## Установка laravel

* Подключаемся в контейнер:
``
sudo docker exec -it laravel-app-php /bin/sh
``
* Устанавливаем laravel
``
composer create-project laravel/laravel ./
``
* Устанавливаем права доступа на папки
``
chmod -R 777 storage database
``
* Всё, laravel проект готов, открываем в браузере http://localhost:8084,должна появиться приветственная страница Laravel.