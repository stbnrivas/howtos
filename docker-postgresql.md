# postgreSQL into docker

```bash
docker pull postgres:11.1
```

postgres 11 use by default the /var/lib/postgresql/data

using volumes
```powershell
docker run -p 5432:5432 --name pg11.1_instance_1 -v ${PWD}\DeveloperDocker\postgres_instance1:/var/lib/postgresql/data -e POSGRES_PASSWORD=secret -d postgres:11.1
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
```



```bash
docker container ps
docker container stop pg11.1_instance_1
docker container start pg11.1_instance_1
```


