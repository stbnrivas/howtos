

# postgresql installation

## install packages
dnf install postgresql-server postgresql-contrib
postgresql-setup initdb


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
