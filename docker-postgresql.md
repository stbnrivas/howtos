# postgreSQL into docker




## into a single docker command

```bash
docker pull postgres:12.1
```

simple
```bash
docker run -p 5432:5432 --name pgdb -e POSTGRES_PASSWORD=secret -d postgres:12.1
```

with extra config
```bash
docker run -p 5432:5432 \
    --name pg_container_name \
    -e 'POSTGRES_USER=dev' -e 'POSTGRES_PASSWORD=secret'  -e 'POSTGRES_DB=pg_database' \
    -d postgres:12.1
```

```bash
# check client was installed
pg_config --version

# connect
psql -h localhost -U postgres
```









```bash
docker pull postgres:11.1
```

postgres 11 use by default the /var/lib/postgresql/data

using volumes
```powershell
```


```powershell
docker run -p 5432:5432 --name pg11.1_instance_2 --mount type=bind,source=${PWD}\DeveloperDocker\postgres_instance1,destination=/var/lib/postgresql/data -e POSGRES_PASSWORD=secret -d postgres:11.1
```


```bash
# access to bash
docker exec -it pg11.1_instance_2 /bin/bash
ls /var/lib/postgresql/data/
# access to psql
docker exec -it pg11.1_instance_1 psql -U postgres
```

```sql
CREATE DATABASE test_db;
CREATE TABLE test_table (id smallint,text varchar(100));
\d
INSERT INTO test_table (id, text) VALUES (1,'hello world');
SELECT * FROM test_table;
\q


CREATE USER youruser WITH ENCRYPTED PASSWORD 'yourpass';
GRANT ALL PRIVILEGES ON DATABASE yourdbname TO youruser;
```



```bash
docker container ps
docker container stop pg11.1_instance_1
docker container start pg11.1_instance_1
```






```
SELECT datname FROM pg_database;
```


```
SHOW max_connections;
select count(*) from pg_stat_activity;


SELECT pg_terminate_backend(pg_stat_activity.pid)
FROM pg_stat_activity
WHERE datname = current_database()
  AND pid <> pg_backend_pid();
```



```bash
docker exec -it  $container_id psql -U postgres
```