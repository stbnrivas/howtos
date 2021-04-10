


```bash
docker run --name mariadb-container-name -e MYSQL_ROOT_PASSWORD=secret -p 3306:3306 -d mariadb:10.4

# using volumes to persist data
docker run --name mariadb-container-name -e MYSQL_ROOT_PASSWORD=secret -p 3306:3306 -v ~/mysql-data:/var/lib/mysql -d mariadb:10.4

docker exec -it $container_name /bin/bash
```


import

```bash
mysql -u username -p database_name < file.sql
mysql -u root  --host 127.0.0.1 -p db565962610 < ~/work/project/db565962610_db_1and1_com.sql
```


```sql
show databases
use $database

show tables

SELECT * FROM sometable\G


```




