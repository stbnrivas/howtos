# Nmap scan network

nmap -sP 192.168.1.0/24
nmap -Pn 192.168.1.1



# Nmap Target Selection

Scan a single IP 	nmap 192.168.1.1
Scan a host 	nmap www.testhostname.com
Scan a range of IPs 	nmap 192.168.1.1-20
Scan a subnet 	nmap 192.168.1.0/24
Scan targets from a text file 	nmap -iL list-of-ips.txt


# Nmap Port Selection
Scan a single Port 	nmap -p 22 192.168.1.1
Scan a range of ports 	nmap -p 1-100 192.168.1.1
Scan 100 most common ports (Fast) 	nmap -F 192.168.1.1
Scan all 65535 ports 	nmap -p- 192.168.1.1


# Nmap Port Scan types
Scan using TCP connect 	nmap -sT 192.168.1.1
Scan using TCP SYN scan (default) 	nmap -sS 192.168.1.1
Scan UDP ports 	nmap -sU -p 123,161,162 192.168.1.1
Scan selected ports - ignore discovery 	nmap -Pn -F 192.168.1.1