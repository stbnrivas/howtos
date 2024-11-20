# from [beej's guide to network programming using internet sockets]

thanks and don't forget check the source: [https://beej.us/guide/bgnet/](https://beej.us/guide/bgnet/)


sockets in unix everything is a file whe a unix program do things use a descriptor that is an integer associated with network connection, a fifo , a pipe a disk file... you can use read() and write() but... send() and recv() oofer much greather control over data transmission...


there are a lot of kind of sockets but we focus on internet sockets, there are two types (there are more like raw sockets):

- `SOCK_STREAM` TCP and reliables connection oriented
- `SOCK_DGRAM`  UDP non reilable and connectionless


## Data Encapsulation of messages

- build a packet with a header, payload and rarely a footer by the first protocol
- this packet will be encapsulated by next protocol {TCP,UDP}
- again is encapsulated by next protocol IP
- again is encapsulated by next protocol Ethernet

whe a computer receive this packet undo the previous process in reverse order

- again is unencapsulated by next protocol Ethernet
- again is unencapsulated by next protocol IP
- again is unencapsulated by next protocol {TCP,UDP}
- the computer get the package with header and payload and rarely footer


this network model aka OSI have the advanteage that you can write sockets programs without care of the phisical transmission protocol, network protocol  or topology... doing transparente for socket programmer.

## IP (Internet Protocol)
IPv4 it's a  32 bits => 4 octecs 
	=>     0..255 .     0..255 .    0..255 .     0..255
	=>        127 .          0 .         0 .          1
	=>        192 .        168 .         1 .          1
IPv4 it's a 128 bits => 8 hex    
	=> 0000..FFFF : 0000..FFFF : 0000..FFFF : 0000..FFFF : 0000..FFFF : 0000..FFFF : 0000..FFFF : 0000..FFFF
	=>       2607 : f0d0 : 4545 :    3 :  200 : f8ff : fe21 : 67cf
	=>       0000 : 0000 : 0000 : 0000 : 0000 : 0000 : 0000 : 0001


## subnetting

ip / submask
127.0.0.1
0000:0000:0000:0000:0000:0000:0000:0001 / 128
::1 / 128  a shortcut

## port numbers

port number are a 16bit number => 0..65535
port from 0 .. 1024 are special OS privilegues to use

## byte order

No one wanted to have to tell you... but probably your computer might have been storing bytes  in reverse order ... it's about bit-endian or little-endian.

The Big-Endian is also called Network Byte Order because that's is the order preferred by networks... we will need to make sure your byte order rightly. The good new is you can use special functions to do.

```c
htons(); // HOST TO NETWORK SHORT
htonl(); // HOST TO NETWORK LONG 
ntohs(); // NETWORK TO HOST SHORT
ntohl(); // NETWORK TO HOST LONG
```

## struct used in network interface

```c
struct addrinfo{
	int              ai_flags;        // AI_PASSIVE, AI_CANONNAME, etc
	int              ai_family;       // AF_INET, AF_INET6, AF_UNSPEC
	int              ai_socktype;     // SOCK_STREAM, SOCK_DGRAM
	int              ai_protocol;     // use 0 for "any"
	size_t           ai_addrlen;      // size of ai_addr in bytes
	struct sockaddr *ai_addr;         // struct sockaddr_in or in6
	char             ai_cannonname;   // full cannonical hostname
	struct addrinfo *ai_next;         // linked list, next node
}
```

`sockaddr` 

```c
struct sockaddr {
	unsigned short sa_family;         // address family, AF_xxx
	char           sa_data[14];       // 14 bytes of protocol address
}
```

`sockaddr_in` internet socket keeping the addresses IPv4 

```c
struct sockaddr_in {
	short int          sin_family;    // addres family: AF_INET, AF_UNIX, AF_NS, AF_IMPLINK
	unsigned short int sin_port;      // 16 bit port number 
	struct in_addr     sin_addr;      // 32 bits internet address
	unsigned char      sin_zero[8];   // same size as struct sockaddr, not used
}
```


```c
struct in_addr {
	uint32_t s_addr; // that's 32 bit int 4 bytes
}

struct sockaddr_in6 {
	u_int16_t       sin6_family;    // address family, AF_INET6
	u_int16_t       sin7_port;      // port number, network byte order
	u_int32_t       sin6_flowinfo;  // ipv6 address
	struct in6_addr sin6_addr;      // ipv6 address
	u_int32_t       sin6_scope_id;  // scope id
}

struct in6_addr {
	unsigned char   s6_addr[16];
}
```


```c
struct sockaddr_storage {
	sa_family_t ss_family;      // address family
	char        __pad1[__SS_PAD1SIZE];
	int64_t     __ss_align;
	char        __ss_pad2[_SS_PAD2SIZE];
}
```



```c
// IPv4
struct sockaddr_in sa;
inet_pton(AF_INET, "10.12.110.57", &(sa.sin_addr));

// IPv6
struct sockaddr_in6 sa6;
inet_pton(AF_INET6, "2001:db8:63b3:1:3490", &(sa6.sin6_addr));
```


## functions

```c
int socket(int domain, int type, int protocol);

void menset(void *ptr, int v, size_t n);

uint32_t htonl(uint32_t hostlong);
uint16_t htons(uint16_t hostshort);

int bind(int fdsock, const struct sockaddr *structaddr, socklent_t lenaddr);

int listen(int sockfd, int lengue);

int accept(int socket, struct sockaddr *address, socklen_t *len);

ssize_t send(int fdsock, const void *buf, size_t length, int flags);

```



## example to translate from domain to ip


```c
/*
** showip.c -- show IP addresses for a host given on the command line
*/

#include <stdio.h>
#include <string.h>
#include <sys/types.h>
#include <sys/socket.h>
#include <netdb.h>
#include <arpa/inet.h>
#include <netinet/in.h>

int main(int argc, char *argv[])
{
	struct addrinfo hints, *res, *p;
	int status;
	char ipstr[INET6_ADDRSTRLEN];

	if (argc != 2) {
	    fprintf(stderr,"usage: showip hostname\n");
	    return 1;
	}

	memset(&hints, 0, sizeof hints);
	hints.ai_family = AF_UNSPEC; // AF_INET or AF_INET6 to force version
	hints.ai_socktype = SOCK_STREAM;

	if ((status = getaddrinfo(argv[1], NULL, &hints, &res)) != 0) {
		fprintf(stderr, "getaddrinfo: %s\n", gai_strerror(status));
		return 2;
	}

	printf("IP addresses for %s:\n\n", argv[1]);

	for(p = res;p != NULL; p = p->ai_next) {
		void *addr;
		char *ipver;

		// get the pointer to the address itself,
		// different fields in IPv4 and IPv6:
		if (p->ai_family == AF_INET) { // IPv4
			struct sockaddr_in *ipv4 = (struct sockaddr_in *)p->ai_addr;
			addr = &(ipv4->sin_addr);
			ipver = "IPv4";
		} else { // IPv6
			struct sockaddr_in6 *ipv6 = (struct sockaddr_in6 *)p->ai_addr;
			addr = &(ipv6->sin6_addr);
			ipver = "IPv6";
		}

		// convert the IP to a string and print it:
		inet_ntop(p->ai_family, addr, ipstr, sizeof ipstr);
		printf("  %s: %s\n", ipver, ipstr);
	}

	freeaddrinfo(res); // free the linked list

	return 0;
}
```




## basic process of connection server and client


|     client    |     |     server     |
|--           --|-- --|--            --|
|               |     | getaddrinfo()  |
|               |     | socket()       |
|               |     | bind()         |
| getaddrinfo() |     | listen()       |
| socket()      |     | accept()       |
| connect()     |     |                |
| send()        |     | recv()         |
| recv()        |     | send()         |
| close()       |     | close()        |




## a client source


```c
#
```