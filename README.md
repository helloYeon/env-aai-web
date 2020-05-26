
# env-aai-web
This is a basic LAMP environment built using Docker Compose. It consists following.

- php7.3
- centos7
- apache2.4
- mysql8.0
- composer
- node js

## Constitution
```
env-aai-web/

├── docker
│   ├── db
│   │   └── my.cnf       # Sync to /etc/mysql/conf.d/my.cnf
│   └── web
│       ├── Dockerfile
│       ├── docker.conf  # Copy to /etc/httpd/conf.d/docker.conf
│       ├── php.ini      # Sync to /etc/php.ini
│       └── php73.conf   # Copy to /etc/httpd/conf.d/php73.conf
├── docker-compose.yml
├── logs
│   ├── access_log
│   ├── error_log
│   ├── mysql-error.log
│   ├── mysql-query.log
│   ├── mysql-slow.log
│   └── php-error.log
└── src

```


## Installation

### 1.clone this repository
```bash
git clone git@github.com:yeon444/env-aai-web.git
cd env-aai-web
```
### 2.run docker
```
$docker-compose up -d --build
```

### 3.initialization
```
# access to container
$docker-compose exec web bash

# install composer
[root@5f2582e9f467 html]# composer install

# create .env
[root@5f2582e9f467 html]# cp .env.example  .env

# exit to Host OS
[root@5f2582e9f467 html]# exit

# restart
$docker-compose restart

# access to container & migrate
$docker-compose exec web bash
[root@5f2582e9f467 html]# php artisan migrate

# create key
[root@5f2582e9f467 html]# php artisan key:generate
```

### 4.Confirm
> `Access to http://127.0.0.1:10080/`

![aa](https://github.com/yeon444/docker-lamp-laravel-centos7/blob/images/env_setting_ok.png)


## TODO
1. add php Xdebug
1. add phpMyAdmin


