# ACCESS CONTROLS - HOST

## DIFFERENCES AMONG TRAFFIC FILTERING METHODS AND TECHNOLOGIES

## WHY FILTER TRAFFIC?
Block malicious traffic

Decrease load on network infrastructure

Ensure data flows in an efficient manner

Ensure data gets to intended recipients and only intended recipients

Obfuscate network internals

## PRACTICAL APPLICATIONS FOR FILTERING
Network Traffic - allow or block traffic to/from remote locations.

Email addresses - to block unwanted email to reduce risk or increase productivity

Computer applications in an organization environment - for security from vulnerable software

MAC filtering - also for security to allow only specific computers access to a network

# NETWORK TRAFFIC FILTERING CONCEPTS

Protocols Operation

Header Analysis

Network Reconnaissance

Tunnel Analysis

IOA and IOC

Malware Analysis


## DEFENSE IN DEPTH
Perimeter Security

Network Security

Endpoint Security

Application and OS Security

Data Security


## DEFAULT POLICIES
Explicit - precisely and clearly expressed

Implicit - implied or understood

## BLOCK-LISTING VS ALLOW-LISTING
Block-Listing (Formerly Black-List)

Implicit ACCEPT

Explicit DENY

Allow-Listing (Formerly White-List)

Implicit DENY

Explicit ACCEPT


## FILTERING DEVICE TYPES


![T1_Filtering_Devices_Mechanisms Layer](https://github.com/user-attachments/assets/60c39154-06d2-4c58-a696-57f786d3c6d6)


## OPERATION MODES

![r-t_mode](https://github.com/user-attachments/assets/5c113f26-6877-42a1-b0d9-d537da60d27b)


## FIREWALL FILTERING METHODS
Stateless (Packet) Filtering (L3+4)

Stateful Inspection (L4)

Circuit-Level (L5)

Application Layer (L7)

Next Generation (NGFW) (L7)

## SOFTWARE VS HARDWARE VS CLOUD FIREWALLS
Software - typically host-based

Hardware - typically network-based

Cloud - provided as a service

### TRAFFIC DIRECTIONS
A to B

Traffic originating from the localhost to the remote-host

You (the client) are the client sending traffic to the server.

Return traffic from that remote-host back to the localhost.

The server is responding back to you (the client).

### B to A

Traffic originating from the remote-host to the localhost.

A client is trying to connect to you (the server)

Return traffic from the localhost back to the remote-host.

You (the server) are responding back to the client.

## BASIC FILTERING INTENT


![Filter_intentv4](https://github.com/user-attachments/assets/272cd7ad-514c-425e-a3af-76586942d615)


![Filter_intent_example](https://github.com/user-attachments/assets/4cd6cd5c-4336-4689-a3ba-9b6d51a95d77)


# UNDERSTAND HOST BASED FILTERING

## WINDOWS, LINUX, OR MAC
Windows - Norton, Mcafee, ZoneAlarm, Avast, etc.

Linux - iptables, nftables, UFW, firewalld.

MAC - Little Snitch, LuLu, Vallum, etc.

## NETFILTER FRAMEWORK
Made to provide:

packet filtering

stateless/stateful Firewalls

network address and port translation (NAT and PAT)

other packet manipulation

## NETFILTER HOOKS - > CHAIN
NF_IP_PRE_ROUTING → PREROUTING

NF_IP_LOCAL_IN → INPUT

NF_IP_FORWARD → FORWARD

NF_IP_LOCAL_OUT → OUTPUT

NF_IP_POST_ROUTING → POSTROUTING

## CHAIN FLOW

![IPtables](https://github.com/user-attachments/assets/d62af333-403a-4b55-846d-ff2ce5844756)


## NETFILTER PARADIGM
tables - contain chains

chains - contain rules

rules - dictate what to match and what actions to perform on packets when packets match a rule

## SEPARATE APPLICATIONS
Netfilter created several (separate) applications to filter on different layer 2 or layer 3+ protocols.

iptables - IPv4 packet administration

ip6tables - IPv6 packet administration

ebtables - Ethernet Bridge frame table administration

arptables - arp packet administration


# CONFIGURE IPTABLES FILTERING RULES

## TABLES OF IPTABLES
filter - default table. Provides packet filtering.

nat - used to translate private ←→ public address and ports.

mangle - provides special packet alteration. Can modify various fields header fields.

raw - used to configure exemptions from connection tracking.

security - used for Mandatory Access Control (MAC) networking rules.

## CHAINS OF IPTABLES
PREROUTING - packets entering NIC before routing

INPUT - packets to localhost after routing

FORWARD - packets routed from one NIC to another. (needs to be enabled)

OUTPUT - packets from localhost to be routed

POSTROUTING - packets leaving system after routing

## CHAINS ASSIGNED TO EACH TABLE
filter - INPUT, FORWARD, and OUTPUT

nat - PREROUTING, POSTROUTING, INPUT, and OUTPUT

mangle - All chains

raw - PREROUTING and OUTPUT

security - INPUT, FORWARD, and OUTPUT

## COMMON IPTABLE OPTIONS

-t - Specifies the table. (Default is filter)

-A - Appends a rule to the end of the list or below specified rule

-I - Inserts the rule at the top of the list or above specified rule

-R - Replaces a rule at the specified rule number

-D - Deletes a rule at the specified rule number

-F - Flushes the rules in the selected chain

-L - Lists the rules in the selected chain using standard formatting

-S - Lists the rules in the selected chain without standard formatting

-P - Sets the default policy for the selected chain

-n - Disables inverse lookups when listing rules

--line-numbers - Prints the rule number when listing rules

-p - Specifies the protocol

-i - Specifies the input interface

-o - Specifies the output interface

--sport - Specifies the source port

--dport - Specifies the destination port

-s - Specifies the source IP

-d - Specifies the destination IP

-j - Specifies the jump target action

## IPTABLES SYNTAX
iptables -t [table] -A [chain] [rules] -j [action]
Table: filter*, nat, mangle

Chain: INPUT, OUTPUT, PREROUTING, POSTROUTING, FORWARD

## IPTABLES RULES SYNTAX
-i [ iface ]

-o [ iface ]

-s [ ip.add | network/CIDR ]

-d [ ip.add | network/CIDR ]

-p icmp [ --icmp-type type# { /code# } ]

-p tcp [ --sport | --dport { port1 |  port1:port2 } ]

-p tcp [ --tcp-flags SYN,ACK,PSH,RST,FIN,URG,ALL,NONE ]

-p udp [ --sport | --dport { port1 | port1:port2 } ]

-m to enable iptables extensions:

-m state --state NEW,ESTABLISHED,RELATED,UNTRACKED,INVALID

-m mac [ --mac-source | --mac-destination ] [mac]

-p [tcp|udp] -m multiport [ --dports | --sports | --ports { port1 | port1:port15 } ]

-m bpf --bytecode [ 'bytecode' ]

-m iprange [ --src-range | --dst-range { ip1-ip2 } ]

ACCEPT - Allow the packet

REJECT - Deny the packet (send an ICMP reponse)

DROP - Deny the packet (send no response)

-j [ ACCEPT | REJECT | DROP ]

## MODIFY IPTABLES
Flush table

	iptables -t [table] -F
  
Change default policy

	iptables -t [table] -P [chain] [action]

Lists rules with rule numbers

	iptables -t [table] -L --line-numbers

Lists rules as commands interpreted by the system

	iptables -t [table] -S

Inserts rule before Rule number

	iptables -t [table] -I [chain] [rule num] [rules] -j [action]

Replaces rule at number

	iptables -t [table] -R [chain] [rule num] [rules] -j [action]

Deletes rule at number

	iptables -t [table] -D [chain] [rule num]

 # CONFIGURE NFTABLES FILTERING RULES

 ## NFTABLE ENHANCEMENTS
One table command to replace:

	iptables

	ip6tables

	arptables

	ebtables

simpler, cleaner syntax

less code duplication resulting in faster execution

simultaneous configuration of IPv4 and IPv6

## NFTABLES FAMILIES
ip - IPv4 packets

ip6 - IPv6 packets

inet - IPv4 and IPv6 packets

arp - layer 2

bridge - processing traffic/packets traversing bridges.

netdev - allows for user classification of packets - nftables passes up to the networking stack (no counterpart in iptables)

## NFTABLES HOOKS
ingress - netdev only

prerouting

input

forward

output

postrouting

## NFTABLES CHAIN-TYPES
There are three chain types:

filter - to filter packets - can be used with arp, bridge, ip, ip6, and inet families

route - to reroute packets - can be used with ip and ipv6 families only

nat - used for Network Address Translation - used with ip and ip6 table families only


## NFTABLES SYNTAX

### 1. CREATE THE TABLE

	nft add table [family] [table]

[family] = ip*, ip6, inet, arp, bridge and netdev.

[table] = user provided name for the table.


### 2. CREATE THE BASE CHAIN(Default Policy)
	nft add chain [family] [table] [chain] { type [type] hook [hook] priority [priority] \; policy [policy] \;}
* [chain] = User defined name for the chain.

* [type] =  can be filter, route or nat.

* [hook] = prerouting, ingress, input, forward, output or
         postrouting.

* [priority] = user provided integer. Lower number = higher
             priority. default = 0. Use "--" before
             negative numbers.

* ; [policy] ; = set policy for the chain. Can be
              accept (default) or drop.

 Use "\" to escape the ";" in bash

### 3. CREATE A RULE IN THE CHAIN


	nft add rule [family] [table] [chain] [matches (matches)] [statement]

* [matches] = typically protocol headers(i.e. ip, ip6, tcp,
            udp, icmp, ether, etc)

* (matches) = these are specific to the [matches] field.

* [statement] = action performed when packet is matched. Some
              examples are: log, accept, drop, reject,
              counter, nat (dnat, snat, masquerade)

## RULE MATCH OPTIONS
ip [ saddr | daddr { ip | ip1-ip2 | ip/CIDR | ip1, ip2, ip3 } ]

tcp flags { syn, ack, psh, rst, fin }

tcp [ sport | dport { port1 | port1-port2 | port1, port2, port3 } ]

udp [ sport| dport { port1 | port1-port2 | port1, port2, port3 } ]

icmp [ type | code { type# | code# } ]

## RULE MATCH OPTIONS
ct state { new, established, related, invalid, untracked }

iif [iface]

oif [iface]

## MODIFY NFTABLES
nft { list | flush } ruleset
nft { delete | list | flush } table [family] [table]
nft { delete | list | flush } chain [family] [table] [chain]

List table with handle numbers

	nft list table [family] [table] [-a]

Adds after position

	nft add rule [family] [table] [chain] [position <position>] [matches] [statement]

Inserts before position

	nft insert rule [family] [table] [chain] [position <position>] [matches] [statement]

Replaces rule at handle

	nft replace rule [family] [table] [chain] [handle <handle>] [matches] [statement]

Deletes rule at handle

	nft delete rule [family] [table] [chain] [handle <handle>]

To change the current policy

	nft add chain [family] [table] [chain] { \; policy [policy] \;}                                                                                                                                                                    


# CONFIGURE IPTABLES NAT RULES

## NAT & PAT OPERATORS & CHAINS

![T55_NAT PAT_Chains](https://github.com/user-attachments/assets/3c3f1495-024a-42f1-8bb3-0a1e5165e84d)

## SOURCE NAT



![Source_NAT_image](https://github.com/user-attachments/assets/067932ea-01bb-4aef-8282-287393c7a92a)

	iptables -t nat -A POSTROUTING -o eth0 -s 192.168.0.1 -j SNAT --to 1.1.1.1

![T16_Source_NAT_Graphic](https://github.com/user-attachments/assets/08b3834b-1de8-439b-9a6d-872e596c9cbb)

	iptables -t nat -A POSTROUTING -p tcp -o eth0 -s 192.168.0.1 -j SNAT --to 1.1.1.1:9001

## SNAT MASQUERADING
	iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE

## DESTINATION NAT
![Dest_NAT_image](https://github.com/user-attachments/assets/fbce3102-35e1-49e9-b34f-5b3808d0d611)


	iptables -t nat -A PREROUTING -i eth0 -d 8.8.8.8 -j DNAT --to 10.0.0.1

	iptables -t nat -A PREROUTING -i eth0 -d 8.8.8.8 -j DNAT --to 10.0.0.1
	
	iptables -t nat -A PREROUTING -i eth0 -p tcp --dport 22 -j DNAT --to 10.0.0.1:22
	
	iptables -t nat -A PREROUTING -i eth0 -p tcp --dport 80 -j DNAT --to 10.0.0.2:80
	
	iptables -t nat -A PREROUTING -i eth0 -p tcp --dport 443 -j DNAT --to 10.0.0.3:443
	
	iptables -t nat -A PREROUTING -i eth0 -p tcp --dport 80 -j REDIRECT --to-port 8080
	
# CONFIGURE NFTABLES NAT RULES

## CREATING NAT TABLES AND CHAINS
Create the NAT table

	nft add table ip NAT

Create the NAT chains

	nft add chain ip NAT PREROUTING { type nat hook prerouting priority 0 \; }
	nft add chain ip NAT POSTROUTING { type nat hook postrouting priority 0 \; }

## NFT SNAT
	
	nft add rule ip NAT POSTROUTING ip saddr 10.10.0.40 oif eth0 snat 144.15.60.11
	nft add rule ip NAT POSTROUTING oif eth0 masquerade

 ## NFT DNAT 

	nft add rule ip NAT PREROUTING iif eth0 ip daddr 144.15.60.11 dnat 10.10.0.40
	nft add rule ip NAT PREROUTING iif eth0 tcp dport { 80, 443 } dnat 10.1.0.3
	nft add rule ip NAT PREROUTING iif eth0 tcp dport 80 redirect to 8080

# MANGLE EXAMPLES WITH IPTABLES


	iptables -t mangle -A POSTROUTING -o eth0 -j TTL --ttl-set 128
	iptables -t mangle -A POSTROUTING -o eth0 -j DSCP --set-dscp 26


# CONFIGURE NFTABLES MANGLE RULES


	nft add table ip MANGLE
	nft add chain ip MANGLE INPUT {type filter hook input priority 0 \; policy accept \;}
	nft add chain ip MANGLE OUTPUT {type filter hook output priority 0 \; policy accept \;}
	nft add rule ip MANGLE OUTPUT oif eth0 ip ttl set 128
	nft add rule ip MANGLE OUTPUT oif eth0 ip dscp set 26


























