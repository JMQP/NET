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
# RAW IPV4 SOCKETS


Must include;

	the Ip header 

 	Next Headers

Requires guidance from the "Request for Comments" (RFC) to follow header structure properly.

	RFCs contain technical and organizational documents about the Internet, including specifications and policy documents.

See RFC 791, Section 3 - Specification for details on how to construct an IPv4 header.


## RAW USES

	Testing specific defense mechanisms - such as triggering and IDS for an effect, or filtering

	Avoiding defense mechanisms(Can add a single CHAR to get past defenses)

	Obfuscating data during transfer

	Manually crafting a packet with the chosen data in header fields


# Encoding and Decoding


Encoding

	The process of taking bits and converting them using a specified cipher.

Decoding

	Reverse of the conversion process used by the specified cipher for encoding.

Common encoding schemes
	
	UTF-8, Base64, Hex

DOES NOT actually change value, just changes how its seen


# ENCODING VS ENCRYPTION
Encoding - converts data into a different format

Encryption - scrambles data to make it unreadable without a secret key


# HEX ENCODING AND DECODING
Encode text to Hex:

	echo "Message" | xxd
 
Encode file to Hex:

	xxd file.txt file-encoded.txt

Decode file from Hex:

	xxd -r file-encoded.txt file-decoded.txt

# PYTHON HEX ENCODING
```
import binascii
message = b'Message'
hidden_msg = binascii.hexlify(message)
```

# BASE64 ENCODING AND DECODING
Encode text to base64:

	echo "Message" | base64
 
Endode file to Base64:

	base64 file.txt > file-encoded.txt
 
Decode file from Base64:

	base64 -d file-encoded.txt > file-decoded.txt

CAN ALSO THROW THESE INO CYBERCHEF



# RAW IPV4 AND TCP SOCKET DEMOS

## ipraw.py shell
```
#!/usr/bin/python3
# For building the socket
import socket
# For system level commands
import sys
# For establishing the packet structure (Used later on), this will allow direct access to the methods and functions in the struct module
from struct import pack
# For encoding
import base64    # base64 module
import binascii    # binascii module
# Create a raw socket.
try:
    s = socket.socket(socket.AF_INET, socket.SOCK_RAW, socket.IPPROTO_RAW)
except socket.error as msg:
    print(msg)
    sys.exit()
#0 or IPPROTO_TCP for STREAM and 0 or IPPROTO_UDP for DGRAM. (man ip7). For SOCK_RAW you may specify a valid IANA IP protocol defined in RFC 1700 assigned numbers.
# IPPROTO_IP creates a socket that sends/receives raw data for IPv4-based protocols (TCP, UDP, etc). It will handle the IP headers for you, but you are responsible for processing/creating additional protocol data inside the IP payload.
# IPPROTO_RAW creates a socket that sends/receives raw data for any kind of protocol. It will not handle any headers for you, you are responsible for processing/creating all payload data, including IP and additional headers. (link)
packet = ''
src_ip = "127.0.0.1"
dst_ip = "127.0.0.1"

##################
##Build Packet Header##
##################
# Lets add the IPv4 header information
# This is normally 0x45 or 69 for Version and Internet Header Length
ip_ver_ihl = 69
# This combines the DSCP and ECN feilds.  Type of service/QoS
ip_tos = 0
# The kernel will fill in the actually length of the packet
ip_len = 0
# This sets the IP Identification for the packet. 1-65535
ip_id = 12345
# This sets the RES/DF/MF flags and fragmentation offset
ip_frag = 0
# This determines the TTL of the packet when leaving the machine. 1-255
ip_ttl = 64
# This sets the IP protocol to 16 (CHAOS) (reference IANA) Any other protocol it will expect additional headers to be created.
ip_proto = 16
# The kernel will fill in the checksum for the packet
ip_check = 0
# inet_aton(string) will convert an IP address to a 32 bit binary number
ip_srcadd = socket.inet_aton(src_ip)
ip_dstadd = socket.inet_aton(dst_ip)

#################
## Pack the IP Header ##
#################
# This portion creates the header by packing the above variables into a structure. The ! in the string means 'Big-Endian' network order, while the code following specifies how to store the info. Endian explained. Refer to link for character meaning.
ip_header = pack('!BBHHHBBH4s4s' , ip_ver_ihl, ip_tos, ip_len, ip_id, ip_frag, ip_ttl, ip_proto, ip_check, ip_srcadd, ip_dstadd)

##########
##Message##
##########
# Your custom protocol fields or data. We are going to just insert data here. Add your message where the "?" is. Ensure you obfuscate it though...don't want any clear text messages being spotted! You can encode with various data encodings. Base64, binascii
message = b'last_name'                  #This should be the student's last name per the prompt
hidden_msg = binascii.hexlify(message)  #Students can choose which encodeing they want to use.
# final packet creation
packet = ip_header + hidden_msg
# Send the packet. Sendto is used when we do not already have a socket connection. Sendall or send if we do.
s.sendto(packet, (dst_ip, 0))
# socket.send is a low-level method and basically just the C/syscall method send(3) / send(2). It can send less bytes than you requested, but returns the number of bytes sent.
# socket.sendall is a high-level Python-only method that sends the entire buffer you pass or throws an exception. It does that by calling socket.send until everything has been sent or an error occurs.
```
 

## tcpraw.py shell
```
#!/usr/bin/python3
# For building the socket
import socket
# For system level commands
import sys
# For doing an array in the TCP checksum
import array
# For establishing the packet structure (Used later on), this will allow direct access to the methods and functions in the struct module
from struct import pack
# For encoding
import base64    # base64 module
import binascii    # binascii module
# Create a raw socket.
try:
    s = socket.socket(socket.AF_INET, socket.SOCK_RAW, socket.IPPROTO_RAW)
except socket.error as msg:
    print(msg)
    sys.exit()
# 0 or IPPROTO_TCP for STREAM and 0 or IPPROTO_UDP for DGRAM. (man ip7). For SOCK_RAW you may specify a valid IANA IP protocol defined in RFC 1700 assigned numbers.
# IPPROTO_IP creates a socket that sends/receives raw data for IPv4-based protocols (TCP, UDP, etc). It will handle the IP headers for you, but you are responsible for processing/creating additional protocol data inside the IP payload.
# IPPROTO_RAW creates a socket that sends/receives raw data for any kind of protocol. It will not handle any headers for you, you are responsible for processing/creating all payload data, including IP and additional headers. (link)

src_ip = "127.0.0.1"
dst_ip = "127.0.0.1"

##################
##Build Packet Header##
##################
# Lets add the IPv4 header information
# This is normally 0x45 or 69 for Version and Internet Header Length
ip_ver_ihl =
# This combines the DSCP and ECN feilds.  Type of service/QoS
ip_tos =
# The kernel will fill in the actually length of the packet
ip_len = 0
# This sets the IP Identification for the packet. 1-65535
ip_id =
# This sets the RES/DF/MF flags and fragmentation offset
ip_frag =
# This determines the TTL of the packet when leaving the machine. 1-255
ip_ttl =
# This sets the IP protocol to 16 (CHAOS) (reference IANA) Any other protocol it will expect additional headers to be created.
ip_proto =
# The kernel will fill in the checksum for the packet
ip_check = 0
# inet_aton(string) will convert an IP address to a 32 bit binary number
ip_srcadd = socket.inet_aton(src_ip)
ip_dstadd = socket.inet_aton(dst_ip)

#################
## Pack the IP Header ##
#################
# This portion creates the header by packing the above variables into a structure. The ! in the string means 'Big-Endian' network order, while the code following specifies how to store the info. Endian explained. Refer to link for character meaning.

ip_header = pack('!BBHHHBBH4s4s' , ip_ver_ihl, ip_tos, ip_len, ip_id, ip_frag, ip_ttl, ip_proto, ip_check, ip_srcadd, ip_dstadd)

################
##Build TCP Header##
################
# source port. 1-65535
tcp_src =
# destination port. 1-65535
tcp_dst =
# sequence number. 1-4294967296
tcp_seq =
# tcp ack sequence number. 1-4294967296
tcp_ack_seq =
# can optionaly set the value of the offset and reserve. Offset is from 5 to 15. RES is normally 0.
#tcp_off_res =
# data offset specifying the size of tcp header * 4 which is 20
tcp_data_off =
# the 3 reserve bits + ns flag in reserve field
tcp_reserve =
# Combine the left shifted 4 bit tcp offset and the reserve field
tcp_off_res = (tcp_data_off << 4) + tcp_reserve
# can optionally just set the value of the TCP flags
#tcp_flags =
# Tcp flags by bit starting from right to left
tcp_fin = 0                    # Finished
tcp_syn = 0                    # Synchronization
tcp_rst = 0                    # Reset
tcp_psh = 0                    # Push
tcp_ack = 0                    # Acknowledgement
tcp_urg = 0                    # Urgent
tcp_ece = 0                    # Explicit Congestion Notification Echo
tcp_cwr = 0                    # Congestion Window Reduced
# Combine the tcp flags by left shifting the bit locations and adding the bits together
tcp_flags = tcp_fin + (tcp_syn << 1) + (tcp_rst << 2) + (tcp_psh << 3) + (tcp_ack << 4) + (tcp_urg << 5) + (tcp_ece << 6) + (tcp_cwr << 7)
# maximum allowed window size reordered to network order. 1-65535 (socket.htons is deprecated)
tcp_win =
# tcp checksum which will be calculated later on
tcp_chk =
# urgent pointer only if urg flag is set
tcp_urg_ptr =

# The ! in the pack format string means network order
tcp_hdr = pack('!HHLLBBHHH', tcp_src, tcp_dst, tcp_seq, tcp_ack_seq, tcp_off_res, tcp_flags, tcp_win, tcp_chk, tcp_urg_ptr)

##########
##Message##
##########

# Your custom protocol fields or data. We are going to just insert data here.
# Ensure you obfuscate it though...don't want any clear text messages being spotted!
# You can encode various data encodings. Base64, binascii

message = b'last_name'                                    # This should be the student's last name per the prompt
hidden_msg = base64.b64encode(message)                    # base64.b64encode will encode the message to Base 64

######################
##Create the Pseudo Header##
######################

# After you create the tcp header, create the pseudo header for the tcp checksum.

src_address = socket.inet_aton(src_ip)
dst_address = socket.inet_aton(dst_ip)
reserved = 0
protocol = socket.IPPROTO_TCP
tcp_length = len(tcp_hdr) + len(hidden_msg)

#####################
##Pack the Pseudo Header##
#####################

ps_hdr = pack('!4s4sBBH', src_address, dst_address, reserved, protocol, tcp_length)
ps_hdr = ps_hdr + tcp_hdr + hidden_msg

#########################
##Define the Checksum Function##
#########################

def checksum(data):
        if len(data) % 2 != 0:
                data += b'\0'
        res = sum(array.array("H", data))
        res = (res >> 16) + (res & 0xffff)
        res += res >> 16
        return (~res) & 0xffff

tcp_chk = checksum(ps_hdr)

##############
##Final TCP Pack##
##############

# Pack the tcp header to fill in the correct checksum - remember checksum is NOT in network byte order
tcp_hdr = pack('!HHLLBBH', tcp_src, tcp_dst, tcp_seq, tcp_ack_seq, tcp_off_res, tcp_flags, tcp_win) + pack('H', tcp_chk) + pack('!H', tcp_urg_ptr)

# Combine all of the headers and the user data
packet = ip_header + tcp_hdr + hidden_msg

# s.connect((dst_ip, port)) # typically used for TCP
# s.send(packet)

# Send the packet. Sendto is used when we do not already have a socket connection. Sendall or send if we do.
s.sendto(packet, (dst_ip, 0))

# socket.send is a low-level method and basically just the C/syscall method send(3) / send(2). It can send fewer bytes than you requested, but returns the number of bytes sent.
#socket.sendall ﻿is a high-level Python-only method that sends the entire buffer you pass or throws an exception. It does that by calling socket.send ﻿ until everything has been sent or an error occurs.
```




















