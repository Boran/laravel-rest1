## Laravel REST Example

Laravel Framework version 4.1.24
See http://code.tutsplus.com/tutorials/laravel-4-a-start-at-a-restful-api-updated--net-29785

REST api with two tables: user and url.

### Creating this example

This example was created from scrath on ubuntu 12.04 with apache as follows.

  cd /var/www
  wget http://laravel.com/laravel.phar
  mv laravel.phar /usr/local/bin/laravel
  chmod 755 /usr/local/bin/laravel
  apt-get install php5-curl php5-mcrypt
  a2enmod rewrite
  service apache2 restart

 mysql
 mysql> create database rest1;
 use rest1;
 grant all on rest1.* to rest1@localhost identified by 'rest1pw';

 # create app
  laravel new rest1
  cd rest1
  chown -R www-data app/storage/

 # for the editing, see the URL to the example above
  php artisan key:generate
  vi app/config/app.php
  vi app/config/database.php
  php artisan migrate:make create_users_table --table=users --create
  php artisan migrate:make create_urls_table --table=urls --create
  vi app/database/migrations/*_create_users_table.php
  vi app/database/migrations/*_create_urls_table.php
  vi app/database/seeds/UserTableSeeder.php
  vi app/database/seeds/DatabaseSeeder.php

  php artisan migrate
  php artisan db:seed
  mysql rest1
        mysql> select * from users;
        mysql> select * from urls;

  vi app/models/Url.php
  vi app/filters.php
  vi app/routes.php
  cp app/views/hello.php app/views/authtest.php
  vi app/routes.php app/views/authtest.php
  vi app/views/authtest.php

  curl localhost/rest1/public/index.php
  curl localhost/rest1/public/index.php/foo
  curl -i localhost/rest1/public/index.php/authtest
     HTTP/1.1 401 Unauthorized
  curl --user firstuser:first_password -i localhost/rest1/public/index.php/authtest

 
  php artisan controller:make UrlController
  vi app/routes.php
  vi app/controllers/UrlController.php    # index()
  curl --user firstuser:first_password localhost/rest1/public/index.php/api/v1/url
  vi app/controllers/UrlController.php    # add store()
  curl --user firstuser:first_password -d 'url=http://google.com&description=A Search Engine' localhost/rest1/public/index.php/api/v1/url
  curl --user firstuser:first_password -d 'url=http://fideloper.com&description=A Great Blog' localhost/rest1/public/index.php/api/v1/url
  curl --user firstuser:first_password -d 'url=http://digitalsurgeons.com&description=A Marketing Agency' localhost/rest1/public/index.php/api/v1/url
  curl --user firstuser:first_password -d 'url=http://www.poppstrong.com/&description=I feel for him' localhost/rest1/public/index.php/api/v1/url

  vi app/controllers/UrlController.php    # index() show() destroy()
  curl --user firstuser:first_password localhost/rest1/public/index.php/api/v1/url
  curl --user firstuser:first_password localhost/rest1/public/index.php/api/v1/url/1
  curl -i -X DELETE --user firstuser:first_password localhost/rest1/public/index.php/api/v1/url/1
  curl -i -X PUT --user firstuser:first_password -d 'url=http://yahoo.com' localhost/rest1/public/index.php/api/v1/url/4
  curl --user firstuser:first_password localhost/rest1/public/index.php/api/v1/url


