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

### FILTER LOGIC - MOST EXCLUSIVE

![most-bpf](https://github.com/user-attachments/assets/74db1094-81df-4d91-b0de-39324db44749)

![most-bpf2](https://github.com/user-attachments/assets/190dee3c-850d-4918-bf84-4ffa3be2a595)


```
tcp[13] = 0x11
--assumes this--
tcp[13] & 0xFF = 0x11
```

