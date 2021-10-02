# SSH tunneling


## Forward tunneling `-L`

Specifies that connections to the given TCP port or Unix socket on the local (client) host,
which are to be forwarded to the given host and port, or Unix socket, on the remote side.


example: use a port forwarding to connect remote postgrest

```bash
ssh -L 54320:localhost:5432 user@db_server
ssh -L 54320:localhost:5432 host_defined_into_ssh_config

psql -p 54320 -d db_name -U user -h localhost
```




## Reverse tunneling `-R`

Specifies that connections to the given TCP port or Unix socket on the remote (server) host are to be forwarded to the local side.

```bash
ssh -R 8080:localhost:80 $user@$host


```

example: use a port of remote server to access my localhost web server, like publish a server


```language
ssh -R 8080:localhost:80 $user@$remote_server

curl -Is remote_server
```