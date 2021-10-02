# dockerize existing wordpress

select your versions


```bash
docker pull wordpress:5.2.2-php7.2-apache
docker pull mariadb:10.4
```

run wordpress container to figure out where is wordpress instalation to replace with a volume


```
docker run --name mariadb-container-name -e MYSQL_ROOT_PASSWORD=secret -p 3306:3306 -d mariadb:10.4



docker run --name wp \
 --rm
 -e WORDPRESS_DB_HOST=127.0.0.1 \
 -e WORDPRESS_DB_USER=developer \
 -e WORDPRESS_DB_PASSWORD=secret \
 -e WORDPRESS_DB_NAME=db565962610 \
 wordpress:5.2.2-php7.2-apache

docker exec -it wp /bin/bash


# wp install are into folder /var/www/html
```


duplicate files check file wordpress-installation/wp-content/wp-config.php to get database name

```bash
cp wordpress-installation/wp-content/wp-config.php wordpress-installation/wp-content/wp-config.ori.php
vi wordpress-installation/wp-content/wp-config.php
```



```php
define('DB_NAME', 'XXXXXXXXXXX');
/** MySQL database username */
define('DB_USER', 'XXXXXXXXXXX');
/** MySQL database password */
define('DB_PASSWORD', 'XXXXXXXXXXX');
/** MySQL hostname */
define('DB_HOST', 'XXXXXXXXXXX');
```




# using docker to mount wordpress


1. choose your version  at [https://wordpress.org/download/releases/](https://wordpress.org/download/releases/)

2. build dockerfile

```dockerfile
```


3. use docker-compose


build your docker-compose.yml


```yml
version: '3.7'

services:
  db:
    image: mariadb:10.4
    environment:
      MYSQL_ROOT_PASSWORD: secret_pass
      MYSQL_DATABASE: testdb
      MYSQL_USER: developer
      MYSQL_PASSWORD: secret
    ports:
      - 3306:3306
    volumes:
      - ~/wp/backups/:/var/sql/
  wp:
    depends_on:
      - db
    image: wordpress:5.2.2-php7.2-apache
    environment:
      WORDPRESS_DB_HOST: db:3306
      WORDPRESS_DB_USER: developer
      WORDPRESS_DB_PASSWORD: secret
      WORDPRESS_DB_NAME: testdb
    ports:
      - '80:80'
      - '443:443'
    volumes:
      - ~/work/project/wordpress:/var/www/html
#      - ./wordpress:/var/www/html
# echo "ServerName localhost" >> /etc/apache2/apache2.conf
# echo "ServerName domain.com" >> /etc/apache2/apache2.conf

```


enable root connection from outside of docker compose network

```bash
docker exec -ti container /bin/bash
# root'@'172.26.0.1

mysql -u root -p

GRANT ALL PRIVILEGES ON *.* TO 'root'@'%' IDENTIFIED BY 'password';
CREATE DATABASE testdb

exit


docker-compose restart db
```



connect to mysql and load database

```bash
mysql -u root  --host 127.0.0.1 -p dbuser < /home/XXXX/XXX/XXXX.sql
```





use `/etc/hosts` to set final domain name

```
127.0.0.1 YOURFINALDOMAIN.EXAMPLE
```





# ISSUES

1. `apache2: Could not reliably determine the server's fully qualified domain name`