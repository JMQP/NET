# Stages of Reconaissance
Passive External

	OSINT
 		IPs and Sub D
   		External/3rd Party
	 	People
   		Tech
	 	Content of Interest
	DNS
 		DIG
   		WHOIS
		Zone Trans
  	Historical Cotent
   	Google Searches
	SHODAN
 	p0f
  	Social Tactics
 
Active External

	Outside the org but now sending traffic, e.g. see what ports are open

Passive Internal


Active Internal

![recon](https://github.com/user-attachments/assets/25387fcc-a101-4a49-b5d4-dc834aedfbd0)


## Recon Steps

Network Footprinting

Network Scanning


Network Scanning 

Vulnerability assessment

# Network Foorprinting
Collect information relating to target

	Network

	Systems

	Organization

## Net Scanning 
Port Scanning

Network Scanning

Vulnerability Scanning

## NETWORK ENUMERATION

Network Resource and shares

Users and Groups

Routing tables

Auditing and Service settings

Machine names

Applications and banners

SNMP and DNS details

Other common services and ports

## Vulnerability

Injection

Broken Authentication

Sensitive Data Exposure

XML External Entities

Broken Access Control

Security Misconfiguration

Software/Components with Known Vulnerabilities

# Passive Recon Activities

Open-Source Intelligence (OSINT)

Publicly Available Information (PAI)

IP Addresses and Sub-domains

Identifying External/3rd Party sites

Identifying People

Identifying Technologies

Identifying Content of Interest

Identifying Vulnerabilities

## IP ADDRESSES AND SUB-DOMAINS
IP Registries:

IANA IPv4

https://www.iana.org/assignments/ipv4-address-space/ipv4-address-space.xhtml

IANA IPv6

https://www.iana.org/assignments/ipv6-unicast-address-assignments/ipv6-unicast-address-assignments.xhtml

## IP ADDRESSES AND SUB-DOMAINS
DNS Lookups:

	arin.net

	whois.domaintools.com
	
	viewdns.info

	dnsdumpster.com

	centralops.net

URL Scan:

	sitereport.netcraft.com

	web-check.xyz

	web-check.as93.net

	urlscan.io 

IP GeoLocation lookup:

	maxmind.com

	iplocation.io
	
	iplocation.net

	infosniper.net

 BGP prefixes:

	bgpview.io

	hackertarget.com
	
	bgp.he.net
	
	bgp4.as

##  IDENTIFYING EXTERNAL/3RD PARTY SITES
Parent/Subordinate organizations

Clients/Customers

Service organizations

Partners

## IDENTIFYING PEOPLE
Target website

Crawler tools like Maltego or Creepy

https://www.maltego.com/
https://www.geocreepy.com/

Search engines

https://en.wikipedia.org/wiki/List_of_search_engines

Social Media

https://en.wikipedia.org/wiki/List_of_social_networking_services

Job Portals

https://en.wikipedia.org/wiki/List_of_employment_websites

Tracking active emails

Family Tree

## IDENTIFYING TECHNOLOGIES
File extensions

https://en.wikipedia.org/wiki/List_of_filename_extensions

Server responses

https://websiteguidelines.com/guides/different-types-of-web-servers/

Job listing

Website content

https://dorik.com/blog/how-to-tell-what-website-builder-was-used

Google Hacking

https://gist.github.com/sundowndev/283efaddbcf896ab405488330d1bbc06

Shodan.io

https://www.shodan.io/

MAC OUI Lookup

https://macaddress.io/

## IDENTIFYING CONTENT OF INTEREST
/etc/passwd and /etc/shadow or SAM database

Configuration files

Log files

Backup files

Test pages

Client-side code

## IDENTIFYING VULNERABILITIES
Known Technologies

Error messages responses

Identify running services

Identify running OS

Monitor running Applications

## DIG VS WHOIS
Whois - queries DNS registrar over TCP port 43

	Information about the owner who registered the domain

 e.g.

 	whois zonetransfer.me

Dig - queries DNS server over UDP port 53

	Name to IP records

e.g.

	dig zonetransfer.me A
	dig zonetransfer.me AAAA
	dig zonetransfer.me MX
	dig zonetransfer.me TXT
	dig zonetransfer.me NS
	dig zonetransfer.me SOA

##  ZONE TRANSFER
Between Primary and Secondary DNS over TCP port 53

https://digi.ninja/projects/zonetransferme.php

	dir axfr {@soa.server} {target-site}
	dig axfr @nsztm1.digi.ninja zonetransfer.me

 ## NETCRAFT
Similar to whois but web-based

https://sitereport.netcraft.com/

## HISTORICAL CONTENT
Wayback Machine

http://archive.org/web/

## GOOGLE SEARCHES
Advanced searches.

List of filters(https://gist.github.com/sundowndev/283efaddbcf896ab405488330d1bbc06)

Dork Search(https://dorksearch.com/)

	site:*.ccboe.net

	site:*.ccboe.net "administrator"

## SHODAN
Shodan: A search engine for Internet-connected devices

https://www.shodan.io

Be aware of attribution

## PASSIVE OS FINGERPRINTER (P0F)
p0f: Passive scanning of network traffic and packet captures.

	more /etc/p0f/p0f.fp

	sudo p0f -i eth0

	sudo p0f -r test.pcap

Examine packets sent to/from target

Can guess Operating Systems and version

Can guess client/server application and version


## SOCIAL TACTICS
Social Engineering (Hack a person)

Technical based (Email/SMS/Bluetooth)

Other Types (Dumpster Diving/Shoulder Surf)


# ACTIVE EXTERNAL

## SCANNING NATURE
Active

Passive

## SCANNING STRATEGY
Remote to Local (Attacking/Pentesting)

Local to Remote (Grey Area)

Local to Local (Net Admins)

Remote to Remote (Cloud VM scanning other Cloud VM)

## SCANNING APPROACH
Aim

	Wide range target scan

	Target specific scan

Method

	Single source scan

		1-to-1 or 1-to-many

Distributed scan

	many-to-one or many-to-many

## VERTICAL SCAN
Scan some (or all ports) on a single target

![verticalscan](https://github.com/user-attachments/assets/430db068-1293-4134-9f70-dc4fd591ae31)

## HORIZONTAL SCAN
Scan a single (or set) port(s) on a range of targets.

![horizontalscan1](https://github.com/user-attachments/assets/9c4d23d9-341b-43d5-8217-1fa36e557f17)

## STROBE SCAN
Scan a predefined subset of ports on a range of targets.
![horizontalscan2](https://github.com/user-attachments/assets/07c1d1f4-cfd8-4297-9dcc-ebda17ea4aa5)

## BLOCK SCAN
Scan all (or a range) ports on a range of targets.
![horizontalscan3](https://github.com/user-attachments/assets/4998a7e7-408a-41fd-bb87-f54e31a08fc0)

## ISTRIBUTED SCAN - BLOCK

![distributedscan1](https://github.com/user-attachments/assets/4dd5f8c8-e0c2-460c-9306-917d728dbb32)

## DISTRIBUTED SCAN - STROBE
![distributedscan2](https://github.com/user-attachments/assets/b02a42ee-635c-4c16-a7a2-1fb60608005d)

## PING
Ping one IP:

	ping 172.16.82.106 -c 1
Ping a range:

	for i in {1..254}; do (ping -c 1 172.16.82.$i | grep "bytes from" &) ; done
 
## NMAP DEFAULTS
Default Scan:

	User: TCP Full Connect Scan (-sT)

	Root: TCP SYN Scan (-sS)

Default Ports scanned: 1000 most commonly used TCP or UDP ports

## NMAP PORT STATES
open

closed

filtered

unfiltered

open|filtered

closed|filtered

### nmap Options List 

https://nmap.org/book/man-briefoptions.html

## NMAP SCAN TYPES
Broadcast Ping/Ping sweep (-sP, -PE)

SYN scan (-sS)

Full connect scan (-sT)

Null scan (-sN)

FIN scan (-sF)

XMAS tree scan (-sX)

UDP scan (-sU)

Idle scan (-sI)

Decoy scan (-D)

ACK/Window scan (-sA)

RPC scan (-sR)

FTP scan (-b)

OS fingerprinting scan (-O)

Version scan (-sV) ***

Discovery probes

### NMAP - OTHER OPTIONS
-PE - ICMP Ping

-Pn - No Ping

### NMAP - TIME-OUT
-T0 - Paranoid - 300 Sec

-T1 - Sneaky - 15 Sec

-T2 - Polite - 1 Sec

-T3 - Normal - 1 Sec

-T4 - Aggresive - 500 ms

-T5 - Insane - 250 ms

### NMAP - DELAY
--scan-delay <time> - Minimum delay between probes

--max-scan-delay <time> - Max delay between probes

### NMAP - RATE LIMIT
--min-rate <number> - Minimum packets per second

--max-rate <number> - Max packets per second

## TRACEROUTE - FIREWALKING
	traceroute 172.16.82.106

	traceroute 172.16.82.106 -p 123
 
	sudo traceroute 172.16.82.106 -I
 
	sudo traceroute 172.16.82.106 -T
 
	sudo traceroute 172.16.82.106 -T -p 443

## NETCAT - SCANNING
nc [Options] [Target IP] [Target Port(s)]
-z : Port scanning mode i.e. zero I/O mode

-v : Be verbose [use twice -vv to be more verbose]

-n : do not resolve ip addresses

-w1 : Set time out value to 1

-u : To switch to UDP

e.g.

	nc -zvnw1 <IP> <port> <port> <port>
## NETCAT - HORIZONTAL SCANNING
Range of IPs for specific ports

TCP

	for i in {1..254}; do nc -nvzw1 172.16.82.$i 20-23 80 2>&1 & done | grep -E 'succ|open'
UDP

	for i in {1..254}; do nc -nuvzw1 172.16.82.$i 1000-2000 2>&1 & d

## NETCAT - VERTICAL SCANNING
Range of ports on specific IP

TCP

	nc -nzvw1 172.16.82.106 21-23 80 2>&1 | grep -E 'succ|open'
UDP

	nc -nuzvw1 172.16.82.106 1000-2000 2>&1 | grep -E 'succ|open'

## NETCAT - TCP SCAN SCRIPT
```
#!/bin/bash
echo "Enter network address (e.g. 192.168.0): "
read net
echo "Enter starting host range (e.g. 1): "
read start
echo "Enter ending host range (e.g. 254): "
read end
echo "Enter ports space-delimited (e.g. 21-23 80): "
read ports
for ((i=$start; $i<=$end; i++))
do
    nc -nvzw1 $net.$i $ports 2>&1 | grep -E 'succ|open'
done
```
## NETCAT - UDP SCAN SCRIPT
```
#!/bin/bash
echo "Enter network address (e.g. 192.168.0): "
read net
echo "Enter starting host range (e.g. 1): "
read start
echo "Enter ending host range (e.g. 254): "
read end
echo "Enter ports space-delimited (e.g. 21-23 80): "
read ports
for ((i=$start; $i<=$end; i++))
do
    nc -nuvzw1 $net.$i $ports 2>&1 | grep -E 'succ|open'
done
```
## NETCAT - BANNER GRABBING
Find what is running on a particular port

	nc [Target IP] [Target Port]
	nc 172.16.82.106 22
	nc -u 172.16.82.106 53
	-u : To switch to UDP
## CURL AND WGET
Both can be used to interact with the HTTP, HTTPS and FTP protocols.

Curl - Displays ASCII

	curl http://172.16.82.106
	curl ftp://172.16.82.106
 	curl 172.16.82.106:80
Wget - Downloads (-r recursive) (uses http by default)

	wget -r http://172.16.82.106
	wget -r ftp://172.16.82.106
	wget 172.16.82.106:21
 
# Passive Internal 

## PACKET SNIFFERS
Wireshark

Tcpdump

p0f

Limited to traffic in same local area of the network


## IP CONFIGURATION
Windows: ipconfig /all

Linux: ip address (ifconfig depreciated)

VyOS: show interface


## DNS CONFIGURATION

Windows: ipconfig /displaydns

Linux: cat /etc/resolv.conf














# DNS CONFIGURATION
Windows: ipconfig /displaydns
Linux: cat /etc/resolv.conf
ARP CACHE
Windows: arp -a
Linux: ip neighbor (arp -a depreciated)
NETWORK CONNECTIONS
Windows: netstat
Linux: ss (netstat depreciated)

Example options useful for both netstat and ss: -antp
a = Displays all active connections and ports.
n = No determination of protocol names. Shows 22 not SSH.
t = Display only TCP connections.
u = Display only UDP connections.
p = Shows which processes are using which sockets.
DEV TCP BANNER GRAB
exec 3<>/dev/tcp/172.16.82.106/22; echo -e "" >&3; cat <&3
￼
￼
￼
￼









 
