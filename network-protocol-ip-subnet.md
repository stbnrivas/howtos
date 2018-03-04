# IPv4

IPv4 uses 32-bits for addresses; there are only 4.3 billion unique addresses available.


A 32-bit IPv4 address is divided into four 8-bit sections called octets that is just another word for byte.


Network addresses are divided into five classes: A, B, C, D, and E

Classes A, B, and C are classified into two parts: Network addresses (Net ID) and Host address (Host ID). The Net ID is used to identify the network, while the Host ID is used to identify a host in the network.


Class D is used for special multicast applications (information is broadcast to multiple computers simultaneously) and Class E is reserved for future use.
		Octet 1		Octet 2		Octet 3 	Octet 4

Class A		NetworkID	HostID		HostID		HostID

Class B		NetworkID	NetworkID	HostID		HostID

Class C		NetworkID	NetworkID	NetworkID	HostID

Class D		Multicast addresses

Class E		Reserved for future


## Network of Class A	

The first bit of the first octet is always set to zero. So you can use only 7-bits for unique network numbers. As a result, there are a maximum of 126 Class A networks available. Each Class A network can have up to 16.7 million unique hosts on its network. The range of host address is from 1.0.0.0 to 127.255.255.255.	


## Network of Class B

The first two bits of the first octet are always set to binary 10, so there are a maximum of 16,384 (14-bits) Class B networks. The first octet of a Class B address has values from 128 to 191.


## Network of Class C

 The first three bits of the first octet are set to binary 110, so almost 2.1 million (21-bits) Class C networks are available. The first octet of a Class C address has values from 192 to 223. These are most common for smaller networks which don't have many unique hosts.




# IPv6

IPv6 uses 128-bits for addresses; this allows for 3.4 X 1038 unique addresses


TODO: research
