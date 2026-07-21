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
* Try to open http://localhost:8084 . You must see 404 nginx page. It's fine.

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

XHProf + Buggregator
``
composer require --dev maantje/xhprof-buggregator-laravel
``
Buggregator Web UI: http://localhost:8000

All requests to laravel app http://localhost:8084 will be available in Buggregator Profile tab.

## Bugs

If Profiler tab in Buggregator is empty, and laravel log at /storage/logs/ has - 400 bad request error.

You need to fix spiral profiler file.

/src/vendor/spiral-packages/profiler/src/storage/WebStorage.php

Change:
``
    public function store(string $appName, array $tags, \DateTimeInterface $date, array $data): void
    {
        $this->options['json'] = [
            'profile' => $this->converter->convert($data),
            'tags' => $tags,
            'app_name' => $appName,
            'hostname' => \gethostname(),
            'date' => $date->getTimestamp(),
        ];
``        
to:
``
    public function store(string $appName, array $tags, \DateTimeInterface $date, array $data): void
    {
        $this->options['json'] = [
            'profile' => $this->converter->convert($data),
            //'tags' => $tags,
            'app_name' => $appName,
            'hostname' => \gethostname(),
            'date' => $date->getTimestamp(),
        ];
``

After that Profiler tab is working fine at Buggregator.