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


