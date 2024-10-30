# Net Traffic

## Capture Libraries

Libpcap - https://www.tcpdump.org/

WinPcap - https://www.winpcap.org/

NPcap - https://nmap.org/npcap/ (Most windows devices use a flavor of this)

## THE USE OF SNIFFING TOOLS AND METHODS

### Practical Uses:

Network troubleshooting

	Diagnosing improper routing or switching

	Identifying port/protocol misconfigurations

	Monitor networking consumption

	Intercepting usernames and passwords

	Eavesdrop on network communications

### Disadvantages:

	Requires elevate permissions

	Can only capture what NIC can see

	Cannot capture local traffic

	Can consume massive amounts of system resources

	Lost packets on busy networks

 ### Ways of Capture

 	Hardware(Dedicated sniffing device directly connected to device being captured)

  	Software (Wireshark)


# Sockets

	How your device will interact with net traffic, each door in a location

 User Space Sockets

 	Stream Socket (TCP)
    Datagram Socket (UDP)

 Kernel Space Sockets
 
 	RAW Sockets 


## Capture Library

![capture](https://github.com/user-attachments/assets/3d109b71-f5b6-44e7-b07d-b36708fdfa6e)

Promiscious Mode capptures all traffic

Requires root for :
	
  	Promicious Mode (Listen on all NICs)

	All captured packets are created as RAW Sockets

 ### Types of Sniffing 

 	Active 

  	Passive 

Sniffing itself is a passive. It becomes active when you are sending traffic out of your back in search of a certain response

## Popular Software PCAP Prog


tcpdump *

Wireshark *

tshark

p0f

NetworkMiner

NetMiner

SolarWinds

BetterCap

EtterCap
	

## Interface Naming

Traditional

	eth0,eth1

 Consistent

 	eno1,ens3

# TCDUMP Primitives

User firendly cap expressions to make life easier, preinstalled macros

 		src or dst

   		host or net

  		tcp or udp



 ### TCPDUMP PRIMITIVE QUALIFIERS
type - the 'kind of thing' that the id name or number refers to

	host, net, port, or portrange

dir - transfer direction to and/or from

	src or dst

proto - restricts the match to a particular protocol(s)

	ether, arp, ip, ip6, icmp, tcp, or udp


### TCPDUMP OPTIONS

-A = print payload in ASCII

-D = list interfaces

-d = (debug)dump the compiled packet-matching code in human readable format

-i = specify capture interface

-e = print data-link headers

-X or XX = print payload in HEX and ASCII

 	Hex on the left, ascii equivalent on the right

-w = write to pcap

-r = read from pcap

-v, vv, or vvv = verbosity

	increases verbosity with each additional "v"
 
-n = no inverse lookups

	no translations of hostnames or port num to svc

###  LOGICAL OPERATORS
Primitives may be combined using:

	Concatenation: 'and' ( && )

	Alteration: 'or' ( || )

	Negation: 'not' ( ! )

### RELATIONAL OPERATORS

< or < =

> or >=

= or == or !=


### Examples 

	If you do not specify an interface, it'll default to the first interface

Simple

	sudo tcpdump ether

	sudo tcpdump icmp 'icmp[icmptype] = icmp-echo'

 	sudo tcpdump 'tcp src port 22'

  			will see what ssh server is responding back with

Complex

	sudo tcpdump 'host 192.168.1.1 and (10.1.1.1 or 10.1.1.2)'

 		If you receive error, it's probably a bash error, add single quotes or escaping parenthesis

# THE FUNCTION OF A BERKLEY PACKET FILTER (BPF)

	Similar in function to primitives

	Reduces redudant computations

	More complex expressions

## COMPARE PRIMITIVES AND BPFS
Primitives (macros)

Not Very Efficient for large number of packets

Will do more computations than necessary

	CMU/Stanford Packet Filter (CSPF) Model commonly called Boolean Expression Tree

	Simple and easy filter expressions

	First user-level packet filter model

	Memory-stack-based filter machine which can create bottlenecks on model CPUs
	
	can have redundant computations of the same information

Berkley Packet Filters (BPF)

	Control Flow Graph (CFG) Model
	
 	Uses a simple (non-shared) buffer model which can make it 1.5 to 20 times faster than CSPF

	Can be more complex to create expressions but offer far more precision


# Contruct API

## KERNEL API
TCPDUMP requests a RAW Socket creation

Filters are set using the SO_ATTACH_FILTER

SO_ATTACH_FILTER allows us to attach a Berkley Packet Filter to the socket to capture incoming packets.

Control Flow Graph (CFG) Model

Uses a simple (non-shared) buffer model which can make it 1.5 to 20 times faster than CSPF

Can be more complex to create expressions but offer far more precision

CONSTRUCT A BPF
KERNEL API
TCPDUMP requests a RAW Socket creation

Filters are set using the SO_ATTACH_FILTER

SO_ATTACH_FILTER allows us to attach a Berkley Packet Filter to the socket to capture incoming packets.

## BERKLEY PACKET FILTERS
```
tcpdump {A} [B:C] {D} {E} {F} {G}

A = Protocol (ether | arp | ip | ip6 | icmp | tcp | udp)
B = Header Byte offset
C = optional: Byte Length. Can be 1, 2 or 4 (default 1) (CANNOT GO LARGER THAN 4)
D = optional: Bitwise mask ( & )
E = Relational operator ( = | == | > | < | <= | >= | != | () | << | >> )
F = Result of Expression
G = optional: Logical Operator ( && || ) to bridge expressions
```

### BPF EXAMPLES

```
tcpdump -i eth0 'ether[12:2] = 0x0806'
tcpdump -i eth1 'ip[9] = 0x06'
tcpdump -i eth0 'tcp[0:2] = 53 || tcp[2:2] = 53'
tcpdump 'ether[12:2] = 0x0800 && (tcp[2:2] != 22 && tcp[2:2] != 23)'
```


## BITWISE MASKING
BPFs can read 1 (byte), 2 (half-word) or 4 (word)

BPFs alone will only filter to the byte level

Bit-wise masking allow filtering precision to the bit level

Binary (0) to ignore bit

Binary (1) to match bit

CAN ONLY USE 'AND' OPERATOR, NOT 'OR'

### BITWISE MASKING EXAMPLES
```
tcpdump 'ether[12:4] & 0xffff0fff = 0x81000abc'
tcpdump 'ip[1] & 252 = 32'
tcpdump 'ip[6] & 224 != 0'
tcpdump 'tcp[13] & 0x11 = 0x11'
tcpdump 'tcp[12] & 0xf0 > 0x50'
```

All bits on is 'F' in hex 

All bits off is '0' in hex

So in "tcp[12] & 0xf0 > 0x50" above, the " tcp[12] indicates byte offset 12 of tcp header, "& 0xF0" is saying to just look at all bits in the 
first field of 12th byte offset" and the "> 0x50", tells us to look at packets greater than 0x50 in this field


### FILTER LOGIC - MOST EXCLUSIVE

![most-bpf](https://github.com/user-attachments/assets/74db1094-81df-4d91-b0de-39324db44749)

![most-bpf2](https://github.com/user-attachments/assets/190dee3c-850d-4918-bf84-4ffa3be2a595)


```
tcp[13] = 0x11
--assumes this--
tcp[13] & 0xFF = 0x11
```



### FILTER LOGIC - LESS EXCLUSIVE
![less-bpf](https://github.com/user-attachments/assets/e3edab4f-5e81-42a0-aee6-efcd197c5b64)

```
tcp[13] & 0x11 = 0x11
```

### FILTER LOGIC - LEAST EXCLUSIVE
![least-bpf](https://github.com/user-attachments/assets/65765344-6da9-4255-a508-0303162bbcb7)

```
tcp[13] & 0x11 > 0
tcp[13] & 0x11 !=0
```

#  BPFS AT THE DATA-LINK LAYER

Search for the destination broadcast MAC address.

	'ether[0:4] = 0xffffffff && ether[4:2] = 0xffff'
	'ether[0:2] = 0xffff && ether[2:2]= 0xffff && ether[4:2] = 0xffff'
Search for the source MAC address of fa:16:3e:f0:ca:fc.

	'ether[6:4] = 0xfa163ef0 && ether[10:2] = 0xcafc'
	'ether[6:2] = 0xfa16 && ether[8:2] = 0x3ef0 && ether[10:2] = 0xcafc'

Search for unicast (0x00) or multicast (0x01) MAC address.

	'ether[0] & 0x01 = 0x00'
	'ether[0] & 0x01 = 0x01'
	'ether[6] & 0x01 = 0x00'
	'ether[6] & 0x01 = 0x01'
	BPFS AT THE DATA-LINK LAYER
 
Search for IPv4, ARP, VLAN Tag, and IPv6 respectively.

	ether[12:2] = 0x0800
	ether[12:2] = 0x0806
	ether[12:2] = 0x8100
	ether[12:2] = 0x86dd


Search for 802.1Q VLAN 100.

	'ether[12:2] = 0x8100 && ether[14:2] & 0x0fff = 0x0064'
	'ether[12:4] & 0xffff0fff = 0x81000064'
 
Search for double VLAN Tag.

	'ether[12:2] = 0x8100 && ether[16:2] = 0x8100'

# BPFS AT THE NETWORK LAYER
Search for IHL greater than 5.

	'ip[0] & 0x0f > 0x05'
	'ip[0] & 15 > 5'
Search for ipv4 DSCP value of 16.

	'ip[1] & 0xfc = 0x40'
	'ip[1] & 252 = 64'
	'ip[1] >> 2 = 16'

 use ">> #" for bit shift
 
 or
 
 utilize calculator "programming mode" to see bit shift
 
Search for traffic class in ipv6 having a value.

	'ip6[0:2] & 0x0ff0 != 0'

 Search for ONLY the RES flag set. DF and MF must be off.

	'ip[6] & 0xE0 = 0x80'
	'ip[6] & 224 = 128'
Search for RES bit set. The other 2 flags are ignored so they can be on or off.

	'ip[6] & 0x80 = 0x80'
	'ip[6] & 128 = 128'
Search for ONLY the DF flag set. RES and MF must be off.

	'ip[6] & 0xE0 = 0x40'
	'ip[6] & 224 = 64'
Search for DF bit set. The other 2 flags are ignored so they can be on or off.

	'ip[6] & 0x40 = 0x40'
	'ip[6] & 64 = 64'

 Search for ONLY the MF flag set. RES and DF must be off.

	'ip[6] & 0xe0 = 0x20'
	'ip[6] & 224 = 32'
Search for MF bit set. The other 2 flags are ignored so they can be on or off.
	
	'ip[6] & 0x20 = 0x20'
	'ip[6] & 32 = 32'

 Search for offset field having any value greater than zero (0).

	'ip[6:2] & 0x1fff > 0'
	'ip[6:2] & 8191 > 0'
Search for MF set or offset field having any value greater than zero (0).

	'ip[6] & 0x20 = 0x20 || ip[6:2] & 0x1fff > 0'
	'ip[6] & 32 = 32 || ip[6:2] & 8191 > 0'

OFFSET VALUES GREATER THAN ZERO WILL BE USED WHEN LOOKING AT ANYTHING AFTER FIST PACKET

 Search for TTL in ipv4(6) packet.

	'ip[8] = 128'
	'ip[8] < 128'
	'ip[8] >= 128'
	'ip6[7] = 128'
	'ip6[7] < 128'
	'ip6[7] >= 128'
Search for ICMPv4(6), TCP, or UDP encapsulated within an ipv4(6) packet.

	'ip[9] = 0x01'
	'ip[9] = 0x06'
	'ip[9] = 0x11'
	'ip6[6] = 0x3A'
	'ip6[6] = 0x06'
	'ip6[6] = 0x11'

 Search for ipv4 source or destination address of 10.1.1.1.

	'ip[12:4] = 0x0a010101'
	'ip[16:4] = 0x0a010101'
Search for ipv6 source or destination address starting with FE80.

	'ip6[8:2] = 0xfe80'
	'ip6[24:2] = 0xfe80'

 Every 2 values represent each octet

 
 # BPFS AT THE TRANSPORT LAYER
Search for TCP with options.

	'tcp[12] & 0xF0 > 0x50'
	'tcp[12] & 240 > 80'
Search for TCP Reserve field with a value.

	'tcp[12] & 0x0F != 0'
	'tcp[12] & 15 > 0'

Search for TCP Flags set to ACK+SYN. No other flags can be set.

	'tcp[13] = 0x12'
Search for TCP Flags set to ACK+SYN. The other flags are ignored.

	'tcp[13] & 0x12 = 0x12' 

 Search for TCP Flags ACK and SYN (both or 1 must be on).

	'tcp[13] & 0x12 != 0'
	'tcp[13] & 0x12 > 0'

 Search for TCP Urgent Pointer having a value.

	'tcp[18:2] != 0'
	'tcp[18:2] > 0'

 # WIRESHARK

 ## DISPLAY FILTERS VS CAPTURE FILTERS
 
Capture filters - used to specify which packets should be saved to disk while capturing.

Display filters - allow you to change the view of what packets are displayed of those that are captured.  Does not actually exclude from total capture.
 
## Capture Filters 
 
 ![wcapture](https://github.com/user-attachments/assets/020d63ce-db5d-46ab-9189-a5ec8e95382a)
Can use most primitives and/or BPFs

## DISPLAY FILTERS
Protocol Headers

Addresses/Ports

Header Fields

Follow Streams

Apply as Filter

## MENUS
Colorize Traffic

Protocol Hierarchy

Firewall Rules

Exporting Objects

Decrypt Traffic

Conversations

Endpoints

I/O Graph

ipv4 and ipv6 statistics

Expert Information

Geo Location

## COLORIZE TRAFFIC
![w12](https://github.com/user-attachments/assets/9313a6d8-ffb0-47d7-a93a-5b56d2811442)
Menu → View → Coloring Rules

## FIREWALL RULES
![w13](https://github.com/user-attachments/assets/86978db0-c70a-4f4f-aa17-d61df881aacc)
Menu → Tools → Firewall ACL Rules


## DECRYPT TRAFFIC

![w15](https://github.com/user-attachments/assets/69403786-aaee-4e40-a136-81391b68c3ee)


Menu → Edit → Preference → Protocols → SSL

## Geo LOCATION
![w14](https://github.com/user-attachments/assets/2a578c6e-4897-42c6-8556-f2c99b2d01e5)
Menu → Edit → preferences → name resolution → GeoIP database directories "Edit"

# Passive OS Finger Printing (P0F)

Similar to tcpdump except it only captures traffic that matches signatures in its database file.

## OS

Searches for specific signatures in:

	Most Operating Systems

	Most Browsers

	Search Robots
	
	Command Line Tools

## P0F SIGNATURE DATABASE

```
less /etc/p0f/p0f.fp
```


## RUN P0F ON INTERFACE
```
p0f -i eth0
```

## RUN P0F ON A PCAP
```
p0f -r capture.pcap
```

## OUTPUT TO GREPPABLE LOG FILE
```
p0f -r wget.pcap -o /var/log/p0f.log
cat /var/log/p0f.log | grep {expression}
```




 

