https://bencane.com/2012/09/17/iptables-linux-firewall-rules-for-a-basic-web-server/

# iptables

```
iptables
ip6tables
```

chain   | behaviour
--------|-----
INPUT   | Used to control the behavior of INCOMING connections.
FORWARD | Used to control the behavior of connections that aren't delivered locally but sent immediately out. (i.e.: router)
OUTPUT  | Used to control the behavior of OUTGOING connections.

what do with input output o forward

what do  | ...
---------|---------
ACCEPT   | Allow the connection
DROP     | Drop the connection (as if no connection was ever made; useful if you want the system to 'disappear' on the network)
REJECT   | Don't allow the connection but send an error back.




## rule LIST|FLUSH|CHECK|APPEND|DELETE|POLICY

you can flush(delete all), check, append or delete rule

```
iptables -L ...
iptables --list

iptables -F ...
iptables --flush ...

iptables -C ...
iptables --check ...

iptables -A ...
iptables --append ...

iptables -D ...
iptables --delete ...

iptables -P ...
iptables --policy ...
```



## list

```
iptables -L
iptables -L | grep {INPUT,OUTPUT,ACCEPT,DROP,FORWARD}
```

to dump a file

```
sudo iptables -S | tee ~/firewalld_iptables_rules
sudo ip6tables -S | tee ~/firewalld_ip6tables_rules
```

## quick and dirty accept

If we want to ACCEPT all connections

```
iptables --policy INPUT ACCEPT
iptables --policy OUTPUT ACCEPT
iptables --policy FORWARD ACCEPT
```

or drop

```
iptables --policy INPUT DROP
iptables --policy OUTPUT DROP
iptables --policy FORWARD DROP
```


## parameters


```
source:

-s=10.0.0.1
-s=10.0.0.0/8

destination:

-d=10.0.0.1
-d=10.0.0.0/8

protocol:

-p --proto  tcp,udp,icmp


-j --jump

-i  --in-interface
```
## NAT (network address translation)


| PREROUTING | allow modify incoming packets before of routing |
| OUTPUT |  allow modify packets generated for same machine after routing  |
| POSTROUTING | allow modify packets jusf before to sending out to the same machine |



### source NAT (change source)

```
change source ip to 1.2.3.4

iptables -t nat -A POSTROUTING -o eth0 -j SNAT --to 1.2.3.4

change source ip to 1.2.3.4, 1.2.3.5 o 1.2.3.6

iptables -t nat -A POSTROUTING -o eth0 -j SNAT --to 1.2.3.4-1.2.3.6

change source ip to 1.2.3.4, ports 1-1023

iptables -t nat -A POSTROUTING -p tcp -o eth0 -j SNAT --to 1.2.3.4:1-1023
```

### destination NAT (change destination)







# firewalld: firewall-cmd
============================

```
firewall-cmd --permanent --add-service=http
firewall-cmd --permanent --add-service=https
```

