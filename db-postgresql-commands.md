# postgresql client

```bash
psql -h localhost -u user database

psql postgres://${USER}:${PASSWORD}@${HOST}:${PORT}/${DATABASE}
```
## shortcut into client

`\?`				help
`\q` 				quit
`\h ALTER TABLE`

`\c db user`		connect
`\l` 				list databases

`\x`                expanded mode to improve legibility into cli

`\dt` 				list tables
`\d table` 			show table

`\dn`				list schemas
`\df`				list functions
`\dv`				list views
`\du` 				list users

`\g`				previous command
`\s`				command history
`\s file`			execute from file

## create database

```sql
CREATE DATABASE test_db;
CREATE USER myuser WITH encrypted password 'mypass';
GRANT ALL PRIVILEGES ON DATABASE test_db TO myuser;
GRANT ALL PRIVILEGES ON DATABASE weride_test TO developer;

ALTER DATABASE weride_test OWNER TO developer;
```
```sql
CREATE TABLE test_table (id smallint,text varchar(100));
```


## example connection

```
psql -h localhost -u user [db_name*]

# if user only has access some database need explicit


\l                       # list databases
\c database              # connect database
\x                       # enable expand mode
\x on
\dt                      # list tables if exist else `no relation` but required `\c database`
\d table                 # describe table

select * from table;
```



## create database from cli no sql


```
createdb -h 127.0.0.1 -p  5432 $database -U postgres
```


## create a backup database using connection string

```
pg_dump postgres://${USER}:${PASSWORD}@${HOST}:${PORT}/${DATABASE} > ${DUMP_FILE_NAME}


pg_dump -U postgres -f pg_mibd.sql mibd
pg_dump -U postgres -f gobierto_staging.sql gobierto_staging

```


## restore a backup database using connection string

```
psql -U username -d dbname < filename.sql

pg_restore -U postgres -h 127.0.0.1 -p 5432 --file=../db.dump
```



## drop database

```
docker exec -it $(container_name) psql -U postgres

SELECT * FROM pg_stat_activity WHERE pg_stat_activity.datname='mydb';
SELECT pg_terminate_backend(pid) FROM pg_stat_activity WHERE datname = 'mydb'
DROP DATABASE mydb;
```



## backup of database

```bash
pg_dump -U usuario -W -h host dbname > dbname.sql
pg_dump -U usuario -W -h host dbname > dbname.sql

```



## rename database

```sql

psql -h localhost -u user [db_name*]

ALTER DATABASE db RENAME TO newdb;

```