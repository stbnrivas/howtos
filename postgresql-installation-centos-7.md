# fedora intallation to use with rails

## install packages

```
dnf install postgresql-server postgresql-contrib 
dnf install pgadmin3

systemctl enable postgresql
systemctl start postgresql
postgresql-setup initdb


initdb /usr/local/var/postgres -E utf8
initdb -D $HOME/pg-data/ -E utf8

postgres -D $HOME/tuts/pg-data
or
pg_ctl -D $HOME/tuts/pg-data -l logfile start

export PGDATA=/Users/tuts/pg-data
postgres

postgresql-setup initdb tuts

su - root
su - postgres
psql 

```

```sql
\password postgres
\q
createuser developer -P
createdb --owner=developer tuts

vi /var/lib/pgsql/data/pg_hba.conf
replace ident to md5

$ psql -h localhost -U developer tuts


\h [COMMAND]	help about command
\h delete


\?  		list all commands
\conninfo	info about connection
\c [DBNAME]	connect to database
\l		list all databases
\d
\dt 		list all tables current schema
\e
export EDITOR="subl -w"
\q 		quit



psql
```

```sql
CREATE DATABASE database_name;
CREATE USER my_username WITH PASSWORD 'my_password';
GRANT ALL PRIVILEGES ON DATABASE "database_name" to my_username;
ALTER USER postgres with encrypted password 'your_password';


ALTER DATABASE database_name OWNER TO new_owner;


drop database [databaseName]

```



# postgresql installation






## installation at fedora to development

dnf install postgresql postgresql-server postgresql-contrib libpqxx-devel
postgresql-setup --initdb --unit postgresql
services start postgresql

## change configuration

vi /var/lib/pgsql/data/pg_hba.conf

pg_hba.conf excerpt (original)

host    all             all             127.0.0.1/32            ident
host    all             all             ::1/128                 ident

Then replace "ident" with "md5", so they look like this:
pg_hba.conf excerpt (updated)

host    all             all             127.0.0.1/32            md5
host    all             all             ::1/128                 md5

host    all     all     192.168.1.0/24  md5


## enable listen port and listen address

vi /var/lib/pgsql/data/postgresql.conf

listen_addresses = '*'
port = 5432

service postgresql restart

## create user password

su postgres -

bash-4.2$ psql
psql (9.4.4)
Type "help" for help.

postgres=# \password
Enter new password:
Enter it again:
postgres=# \q
exit


## allow remote connections

vi /var/lib/pgsql/data/pg_hba.conf


## create database


##open port at firewall

$ sudo firewall-cmd --zone=public --add-port=5432/tcp --permanent
$ sudo firewall-cmd --reload 
