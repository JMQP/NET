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
 	Management - Switch and router mgmt
  	Native - Untagged switch and router traffic
