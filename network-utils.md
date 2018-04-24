# Network Manager for Shell

	nmtui

	nmcli

# show ip for diferent interfaces

	ip addr show


# scan lan network for another machines

	nmap -sn 192.168.1.0/24

	nmap -sP 192.168.1.0/24


	arp-scan --interface=wlp3s0 --localnet

# scan ports of IP

	nmap $IP

# nmap by default scan only ports lower than 1024

	nmap -p 1025-4000 $IP

# quiet scan mode not loggable scan

	nmap -PS20 192.168.1.0/24