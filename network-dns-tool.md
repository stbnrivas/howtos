# add an ip to resolv without external dns server

adding an entry at /etc/hosts you can ignore propation time for a migration of server
	
	cat /etc/hosts

	192.168.1.x  dbb8 dbb8.gzk
	
	ip	hostname	alias

# host

	host google.es
	google.es has address 216.58.210.163
	google.es has IPv6 address 2a00:1450:4003:808::2003
	google.es mail is handled by 20 alt1.aspmx.l.google.com.
	google.es mail is handled by 10 aspmx.l.google.com.
	google.es mail is handled by 40 alt3.aspmx.l.google.com.
	google.es mail is handled by 50 alt4.aspmx.l.google.com.
	google.es mail is handled by 30 alt2.aspmx.l.google.com


# nslookup

	nslookup google.es
	Server:		87.216.1.65
	Address:	87.216.1.65#53

	Non-authoritative answer:
	Name:	google.es
	Address: 216.58.210.163


# dig

	dig A google.es
	dig NS google.es
	dig MX google.es
	dig ANY google.es
	
	dig -x IP

