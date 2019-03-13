# nc 

ncat implementation of nmap, we love nmap so much

```bash
# Ncat 7.70 ( https://nmap.org/ncat )
# Usage: ncat [options] [hostname] [port]
# 
# Options taking a time assume seconds. Append 'ms' for milliseconds,
# 's' for seconds, 'm' for minutes, or 'h' for hours (e.g. 500ms).
#   -4                         Use IPv4 only
#   -6                         Use IPv6 only
#   -U, --unixsock             Use Unix domain sockets only

#   -c, --sh-exec <command>    Executes the given command via /bin/sh
#   -e, --exec <command>       Executes the given command
#   -m, --max-conns <n>        Maximum <n> simultaneous connections
#   -d, --delay <time>         Wait between read/writes
#   -i, --idle-timeout <time>  Idle read/write timeout
#   -p, --source-port port     Specify source port to use
#   -s, --source addr          Specify source address to use (doesn't affect -l)
#   -l, --listen               Bind and listen for incoming connections
#   -k, --keep-open            Accept multiple connections in listen mode
#   -n, --nodns                Do not resolve hostnames via DNS

#   -u, --udp                  Use UDP instead of default TCP
#       --sctp                 Use SCTP instead of default TCP
#   -v, --verbose              Set verbosity level (can be used several times)
#   -w, --wait <time>          Connect timeout
#   -z                         Zero-I/O mode, report connection status only
#       --append-output        Append rather than clobber specified output files
#       --send-only            Only send data, ignoring received; quit on EOF
#       --recv-only            Only receive data, never send anything
#       --allow                Allow only given hosts to connect to Ncat
#       --allowfile            A file of hosts allowed to connect to Ncat
#       --deny                 Deny given hosts from connecting to Ncat
#       --denyfile             A file of hosts denied from connecting to Ncat
#       --broker               Enable Ncat's connection brokering mode
#       --chat                 Start a simple Ncat chat server
#       --proxy <addr[:port]>  Specify address of host to proxy through
#       --proxy-type <type>    Specify proxy type ("http" or "socks4" or "socks5")
#       --proxy-auth <auth>    Authenticate with HTTP or SOCKS proxy server
#       --ssl                  Connect or listen with SSL
#       --ssl-cert             Specify SSL certificate file (PEM) for listening
#       --ssl-key              Specify SSL private key (PEM) for listening
#       --ssl-verify           Verify trust and domain name of certificates
#       --ssl-trustfile        PEM file containing trusted SSL certificates
#       --ssl-ciphers          Cipherlist containing SSL ciphers to use
#       --ssl-alpn             ALPN protocol list to use.
#       --version              Display Ncat's version information and exit

```


## transfer file 

```bash
ip a
# 192.168.1.222
```
write first the command into receptor (destination)

```bash
nc -vl 12345 > $path_file
```
write then the command into sender

```bash
cat $path_file | nc 192.168.1.122 12345 
```

## transfer folder

```bash
ip a
# 192.168.1.222
```
write first the command into receptor (destination)

```bash
nc -vl 12345 > folder.tar
```
write then the command into sender

```bash
tar czp $path_folder | nc 192.168.1.122 12345 
```

now untar de folder

```bash
tar xf folder.tar
```