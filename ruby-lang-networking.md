# ruby networking programming

# ruby networking programming


```ruby
require 'socket'

socket = Socket.new(Socket::INET, Socket::STREAM)  # TCP socket
socket = Socket.new(Socket::INET, Socket::DGRAM)   # UDP socket
socket = Socket.new(Socket::INET6, Socket::STREAM) # TCP IPv6 socket
socket = Socket.new(Socket::INET6, Socket::DGRAM)  # UDP IPv6 socket
socket = Socket.new(Socket::UNIX, Socket::STREAM)  # UNIX stream socket
socket = Socket.new(Socket::UNIX, Socket::DGRAM)   # UNIX datagram sock


socket_ip_v6 = Socket.new(:INET6, :STREAM)
```

## Server or Client role

Every socket has to assume one of two role:

1. initiator (client)
2. listener  (server)


## server

1. the server lifecycle

- create
- bind
- listen
- accept
- close


2. low level aka the hard way


```ruby
require 'socket'
socket = Socket.new(Socket::PF_INET, Socket::STREAM)
addr = Socket.pack_sockaddr_in(4481, '0.0.0.0') # 0.0.0.0 can be specific interface
socket.bind(addr)
queue_size_incoming_connections = 4
socket.listen(queue_size_incoming_connections)
connection, _ = server.accept
```
3.

the client lifecycle