# postgresql client

```bash
psql -h localhost -u user database
```
## shortcut into client

`\?`				help
`\q` 				quit
`\h ALTER TABLE`

`\c db user`		connect
`\l` 				list databases
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
```
```sql
CREATE TABLE test_table (id smallint,text varchar(100));
```