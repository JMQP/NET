# Socket Types
## User Space Sockets
Stream 

	attempts to build a session with TCP, STCP and Bluetooth

Datagram sockets

	connectionless, quickly send and receive, UDP


 The most common sockets that do not require elevated privileges to perform actions on behalf of user applications.
## Kernel Space Sockets
  RAW

    Direct sending and receiving of IP packets without automatic protocol-specific formatting.

Attempts to access hardware directly on behalf of a user application to either prevent encapsulation/decapsulation or to create packets from scratch, which requires elevated privileges.


 ## USER SPACE APPLICATIONS/SOCKETS

 Using tcpdump or wireshark to read a file

Using nmap with no switches

Using netcat to connect to a listener

Using netcat to create a listener above the well known port range (1024+)

Using /dev/tcp or /dev/udp to transmit data

## Kenrenl Space Apps/Sockets

Using tcpdump or wireshark to capture packets on the wire

Using nmap for OS identification or to set specific flags when scanning

Using netcat to create a listener in the well known port range (0 - 1023)

Using Scapy to craft or modify a packet for transmission

Using Python to craft or modify RAW Sockets for transmission

Network devices using routing protocols such as OSPF

Any Traffic without Transport Header (ICMP)

# Python Terms
## Libraries (Standard Python Library)

 Modules (_import module)

	Functions (module.function)

	Exceptions (try:)

	Constants (AF_INET)
	
	Objects ()

	List [] vs Tuple ()

## STRING VS INTEGER
String

	my_string = "Hello World"

Number

	int = 1234

	float = 3.14

	hex = 0x45

## BUILT-IN FUNCTIONS
	int()

	len()

	str()

	sum()

	print()


## BUILT-IN METHODS
	my_string.upper()

	my_string.lower()
	
	my_string.split()

	my_list.append()

	my_list.insert()


 ## How Imports Work

	import {module}

	import {module} as {name} (if you use a name that already exists you will overwrite previous name)

	from {module} import *

	from {module} import {function}

	from {module} import {function} as {name}
# NETWORK PROGRAMMING WITH PYTHON3
![tcp-socket](https://github.com/user-attachments/assets/0f33e57f-e2d3-4346-9167-1220fc0a7e00)
￼
Network sockets primarily use the Python3 Socket library and socket.socket function.
```
import socket
  s = socket.socket(socket.FAMILY, socket.TYPE, socket.PROTOCOL)
```


## THE SOCKET.SOCKET FUNCTION
Inside the socket.socket. function, you have these arguments, in order:

	socket.socket( *family*, *type*, *proto* )
 
family: AF_INET*, AF_INET6, AF_UNIX

type: SOCK_STREAM*, SOCK_DGRAM, SOCK_RAW

proto: 0*, IPPROTO_TCP, IPPROTO_UDP, IPPROTO_IP, IPPROTO_ICMP, IPPROTO_RAW



## PYTHON3 LIBRARIES AND REFERENCES
Socket

Errors

Struct

Exceptions

Sys


# STREAM AND DGRAM SOCKET DEMO

## DEMO Stream Socket
```
#!/usr/bin/python3
import socket
s = socket.socket(socket.AF_INET, socket.SOCK_STREAM, 0)
ip_addr = '127.0.0.1'
port = 1111
s.connect((ip_addr, port))
message = b"Message"
s.send(message)
data, conn = s.recvfrom(1024)
print(data.decode('utf-8'))
s.close()
```

IP address and port
s.connect tells to connect what was specified

"b" designates a bytes like object to be sent, because it must be 

data, conn, will accept the connection and save it as a variable


## Stream Socket Receiver DEMO

```
#!/usr/bin/python3
import socket
import os
port = 1111
message = b"Connected to TCP Server on port %i\n" % port
s = socket.socket(socket.AF_INET, socket.SOCK_STREAM, 0)
s.setsockopt(socket.SOL_SOCKET, socket.SO_REUSEADDR, 1)
s.bind(('', port))
s.listen(1)
os.system("clear")
print ("Waiting for TCP connections\n")
while 1:
    conn, addr = s.accept()
    connect = conn.recv(1024)
    address, port = addr
    print ("Message Received - '%s'" % connect.decode())
    print ("Sent by -", address, "port -", port, "\n")
    conn.sendall(message)
    conn.close()

 ```

# Datagram Socket Sender 
DEMO (UDP)

```
#!/usr/bin/python3
import socket
s = socket.socket(socket.AF_INET, socket.SOCK_DGRAM, 0)
ip_addr = '127.0.0.1'
port = 2222
message = b"Message"
s.sendto(message, (ip_addr, port))
data, addr = s.recvfrom(1024)
print(data.decode())

```


Differences

	.SOCK_DGRAM

	s.sendto


 ## Datagram Socket Receiver


```
#!/usr/bin/python3
import socket
import os
port = 2222
s = socket.socket(socket.AF_INET, socket.SOCK_DGRAM,0)
s.bind(('', port))
os.system("clear")
print ("Awaiting UDP Messages")
while True:
    data, addr = s.recvfrom(1024)
    address, port = addr
    print ("\nMessage Received: '%s'" % data.decode())
    print ("Sent by -", address, "port", port)
    s.sendto(b"Message received by the UDP Message Server!", addr)
```
 ### BONUS
-lup 

	specifies UDP listener
